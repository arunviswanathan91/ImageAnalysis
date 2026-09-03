# Colab completion alerts with ntfy

Long-running segmentation and image-analysis jobs can take several minutes or hours. This optional setup sends a notification to your phone or browser when a Google Colab cell finishes.

Notifications are optional and do not affect the analysis. Always save masks, tables, and figures before sending the notification.

## Simple setup

1. Install the [ntfy app](https://ntfy.sh/) or open the ntfy web interface.
2. Subscribe to a long, private topic name, for example `cycif-a8f2c91e-analysis`.
3. Add this at the end of a long-running Colab cell:

```python
import requests

NTFY_TOPIC = "cycif-a8f2c91e-analysis"  # Replace with your topic

requests.post(
    f"https://ntfy.sh/{NTFY_TOPIC}",
    data="Colab analysis completed.",
    timeout=15,
)
```

Use the same topic name in the ntfy app and in the notebook.

## Recommended setup with Colab Secrets

This keeps the topic name out of a shared notebook.

### 1. Save the topic in Colab

1. Open the **Secrets** panel using the key icon in Colab.
2. Add a secret named `NTFY_TOPIC`.
3. Enter your private topic name as its value.
4. Enable notebook access for the secret.

### 2. Add the notification helper

Run this setup cell once:

```python
import requests
from google.colab import userdata


def notify(message, title="Colab analysis"):
    """Send an ntfy alert without stopping the analysis if delivery fails."""
    try:
        topic = userdata.get("NTFY_TOPIC")
        response = requests.post(
            f"https://ntfy.sh/{topic}",
            data=message,
            headers={"Title": title},
            timeout=15,
        )
        response.raise_for_status()
        print("ntfy alert sent.")
    except Exception as error:
        print("ntfy alert skipped:", error)
```

### 3. Send an alert after saving results

Place this at the end of the segmentation or quantification cell:

```python
# Save outputs first.
np.save(MASK_NPY, masks)

notify(
    "Cellpose segmentation completed and the mask was saved.",
    title="Segmentation complete",
)
```

### 4. Optional failure alert

Use `try` and `except` when both completion and failure notifications are useful:

```python
try:
    result = run_analysis()
    save_results(result)
    notify("Analysis completed and results were saved.")
except Exception as error:
    notify(
        f"Analysis failed: {type(error).__name__}",
        title="Colab analysis failed",
    )
    raise
```

The final `raise` preserves the original error so Colab still displays the traceback.

## Test the connection

```python
notify("Test message from Google Colab.", title="ntfy test")
```

If the message does not arrive, check that:

- the ntfy app is subscribed to exactly the same topic;
- the `NTFY_TOPIC` secret has notebook access enabled;
- the Colab runtime has internet access; and
- phone or browser notifications are enabled.

## Privacy and security

An ntfy topic effectively acts as an access key. Use a long, unguessable topic and do not commit it to a public repository. Do not include patient identifiers, credentials, sensitive filenames, or unpublished numerical results in notification messages.

For advanced authentication or a self-hosted server, consult the official [ntfy publishing documentation](https://docs.ntfy.sh/publish/).

