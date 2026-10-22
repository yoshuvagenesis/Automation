# SMS providers

The `Failure SMS Alert` workflow runs whenever another workflow fails. Open its
**Config (edit me)** node and set:

| Field | Meaning |
| --- | --- |
| `provider` | `routeros` or `android` |
| `to` | Destination number, international format (`+10000000000`) |
| `routeros_url`, `routeros_port` | Used only when provider is `routeros` |
| `android_url` | Used only when provider is `android` |

Then link a **Basic Auth** credential to whichever HTTP Request node you use.

To use the alert, open the main workflow's settings and set **Error workflow**
to `Failure SMS Alert`.

## Option 1: MikroTik modem (`routeros`)

1. Use a RouterOS device with a SIM and LTE/5G interface (this project used a
   MikroTik ATL 5G R16).
2. Enable the REST API (`www` service) and create a user allowed to use the
   SMS tool.
3. Set `routeros_url` to `http://<router-ip>/rest/tool/sms/send` and
   `routeros_port` to the LTE interface name (for example `lte1`).
4. Basic Auth credential: that RouterOS user and password.

## Option 2: Spare Android phone (`android`)

Any Android phone with a SIM can act as the SMS sender. This was built around
the open-source *SMS Gateway for Android* app in local server mode.

1. Install the app and enable the local server. It shows a username, password,
   and the phone's address and port.
2. Give the phone a fixed IP or DHCP reservation so the address does not change.
3. Set `android_url` to `http://<phone-ip>:<port>/message`.
4. Basic Auth credential: the username and password from the app.

The request body follows the app's current format
(`{"textMessage": {"text": ...}, "phoneNumbers": [...]}`). Check the app's own
API docs if your version differs.

## Adding another provider

1. Add a value to the Switch in **Pick provider**.
2. Add an HTTP Request node for that provider and connect it.
3. Add any extra settings to the Config node.
