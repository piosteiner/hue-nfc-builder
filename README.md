# Hue NFC Command Builder

**Use it: [hue.piogino.ch](https://hue.piogino.ch)**

Tap your phone on an NFC tag and your Philips Hue lights do something: turn on the living room at 40 %, switch the
desk lamp to a warm white, fade the bedroom out. This page builds the requests for that. You pick lights or rooms,
choose what should happen, see a preview, and copy the request into an automation app like
[MacroDroid](https://www.macrodroid.com/) or Tasker.

- **Pick** rooms, groups or single lights, loaded from your bridge or pasted as JSON.
- **Choose** on or off, brightness, a white tone or a colour, and a fade.
- **Preview** how every affected light will look, before and after, with the fade played back. The preview knows what
  each bulb can do: a white bulb ignores a colour, a white-ambiance bulb stays within its white range, and a colour
  bulb shows the closest colour its hardware can actually make.
- **Copy** the URL and body into MacroDroid or Tasker. A recipe for a single tag that toggles on and off is included.
- **Tidy up**: several lights can be saved as one group on the bridge, so one request controls them all.

## Is it safe?

Yes, and you don't have to take my word for it: the whole tool is the one file [`index.html`](index.html) in this
repository, and GitHub Pages serves exactly that file at hue.piogino.ch.

- **No server, no account.** Everything runs in your browser. There is no backend that could receive anything.
- **Nothing is sent anywhere** except the requests you trigger yourself ("Load from bridge", "Send now", "Create
  group"), and those go straight from your browser to the bridge address you typed in.
- **Nothing is loaded from elsewhere.** No analytics, no tracking, no fonts or scripts from other sites. A
  Content-Security-Policy in the page enforces this: the browser refuses to load anything that isn't in the file.
- **What's stored, and where:** your bridge IP, the username (API key) and the list of your lights are kept in your
  browser's localStorage, so you don't have to enter them again. They never leave your device. "Clear loaded data"
  removes the light list; clearing the site data in your browser removes everything.

About the username: it's the key the bridge gives an app when you press its button. Anyone on your home network who
has it can control your lights, so treat it like a password. It only works inside your home network.

## Hosted page or downloaded file?

Your bridge talks plain `http://` on your home network, and secure (`https://`) websites usually aren't allowed to
reach it. So:

- **On hue.piogino.ch** you can always build requests by pasting the JSON from the bridge's CLIP debugger (the page
  explains how). Recent versions of Chrome may ask whether the page may access devices on your local network; if you
  allow it, the live buttons ("Load from bridge", "Send now") work there too.
- **Download the page** (link at the bottom of it) and open the file on a computer or phone on your home Wi-Fi:
  then the live buttons work in any browser.

## Getting a username

1. Open `http://<bridge-ip>/debug/clip.html` on your home Wi-Fi (the bridge IP is in the Hue app under Settings →
   Bridges).
2. URL `/api`, body `{"devicetype":"nfc_tags#phone"}`.
3. Press the round button on the bridge, then click **POST** within 30 seconds.
4. The response contains `"username": "…"`. That's it.

## Notes

- It uses the bridge's v1 API (`/api/<username>/…`), which every Hue bridge supports.
- Colours on a screen are a close guide, not an exact match for light from a bulb.
- Not affiliated with Philips or Signify. "Hue" is a trademark of Signify.

## Licence

MIT, see [LICENSE](LICENSE).
