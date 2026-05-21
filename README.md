Block Telemetry
This extension intercepts outbound statistics requests to https://api.paymenter.org/statistics at the HTTP layer before they leave the browser.
How it works
When Block Telemetry is enabled, the extension registers a webRequest listener that intercepts any outbound request matching https://api.paymenter.org/statistics and cancels it. The request never reaches the remote server — no data is transmitted.
When disabled, requests are passed through normally.
Configuration
SettingLocationDefaultBlock TelemetryExtension configuration page → Block Telemetry toggleOff
Navigate to the extension's configuration page and toggle Block Telemetry on or off. The change takes effect immediately for all subsequent requests — no restart required.
Technical details

Interception layer: chrome.webRequest.onBeforeRequest (Manifest V2) / chrome.declarativeNetRequest rule (Manifest V3)
Scope: Matches https://api.paymenter.org/statistics exactly
Method: Request is cancelled (cancel: true) before any data is sent
Persistence: The toggle state is stored in chrome.storage.sync and restored on browser startup

Permissions
The following permissions are required for this feature:
json"permissions": [
  "webRequest",
  "webRequestBlocking",
  "storage"
],
"host_permissions": [
  "https://api.paymenter.org/*"
]

Note: webRequestBlocking is only required on Manifest V2. On Manifest V3 the extension uses declarativeNetRequest instead, which does not require this permission.

Privacy
Enabling Block Telemetry prevents Paymenter from collecting usage statistics from your browser session. No data about this block is logged or reported anywhere by this extension.
