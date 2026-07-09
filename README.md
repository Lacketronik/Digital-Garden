# Digital-Garden

A "Digital Garden" is a space for learning in public, documenting experiments, and archiving thoughts. This project automates that process, turning a casual Slack conversation into a permanent, structured, and browsable web feed.

---

### The Architecture
This project uses a decoupled, serverless pipeline to move your content from a quick thought in Slack to a rendered post on your website.



* **Slack (The Input):** Your interface for capturing raw thoughts, notes, and media.
* **Pipedream (The Engine):** A serverless orchestration layer that manages image processing, API interactions, and workflow chaining.
* **Notion (The Database):** A centralized dashboard for managing your content, maintaining metadata, and archiving older posts automatically.
* **GitHub (The Storage & CDN):** Stores your image assets and the `digital_garden.json` file, which serves as the data source for your frontend.

### How it Works
1.  **Capture:** A message or image is sent to a dedicated Slack channel.
2.  **Process:** Pipedream captures the event, optimizes the binary data, and uploads assets to GitHub.
3.  **Sync:** The workflow updates your Notion database and rebuilds the `digital_garden.json` file.
4.  **Cleanup:** A chained, secondary Pipedream workflow periodically archives entries from Notion to keep the feed curated.
5.  **Display:** Your frontend website fetches the `digital_garden.json` to render the live feed.

---

### Key Technical Features
* **Automatic Archiving:** Uses chained HTTP triggers to maintain a lean database, ensuring the feed never grows beyond a specific limit.
* **Seamless CDN Delivery:** Automatically converts GitHub `blob` URLs into `raw` CDN links for instant rendering.
