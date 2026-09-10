# sensmos_store

File crypto and the relay client for [Sensmos](https://sensmos.com) Store — shared by the phone
app and the desktop app so that X25519, HKDF and AES-GCM exist in **one** place.

Two copies of the same crypto drift apart within a year, and the drift shows up only when
somebody's file will not open. That is the whole reason this package exists.

## What is in here

| File | What it does |
| --- | --- |
| `lib/store_crypto.dart` | per-file random key, wrapped to the owner's box (X25519 + HKDF); file names and folder hashes; block hashes for the proofs |
| `lib/store_relay.dart` | the WebSocket client for `/v1/store` — package, upload, download, list, delete |
| `lib/upnp.dart` | opening a port on the router, for transfers that go straight between the two ends |
| `lib/logo.dart` | the Sensmos mark, so both apps draw the same one |

The owner's key comes from a signature made by their wallet, on their own device. It never leaves
it and is never sent anywhere — the backend relays ciphertext with a random identifier and cannot
decrypt it, and neither can the person hosting it.

## Using it

Not published to pub.dev. Both apps take it as a path dependency:

```yaml
dependencies:
  sensmos_store:
    path: ../SHARED/sensmos_store
```

## Where it is used

- [sensmos-app](https://github.com/Galusz/sensmos-app) — the phone app, which holds the wallet
- [sensmos-store-desktop](https://github.com/Galusz/sensmos-store-desktop) — Windows, Linux, macOS

Comments in the source are in Polish; everything a user sees is translated in the apps.
