# CivilService Zone — PWA package

ऐप का नाम: CivilService Zone

## GitHub / Render पर अपडेट
1. ZIP extract करें।
2. सभी फाइलें repository के उसी root में upload करें जहाँ `server.js`, `package.json` और `index.html` हैं।
3. Existing files replace करें, नई `manifest.json`, `service-worker.js`, `icons/` और यह README जोड़ें।
4. Commit changes करें और Render deploy पूरा होने दें।
5. `https://YOUR-DOMAIN/manifest.json`, `/service-worker.js`, `/icons/icon-192.png` और `/icons/icon-512.png` खोलकर जाँचें कि ये फाइलें खुलती हैं।
6. Android Chrome में वेबसाइट खोलें → ⋮ → Install app / Add to Home screen।

## जरूरी नोट
- यह PWA setup मौजूदा Node server और API को बनाए रखता है।
- Service worker जानबूझकर authenticated pages/API/data cache नहीं करता।
- Render Free local filesystem स्थायी database नहीं है; मौजूदा README के अनुसार स्थायी data के लिए PostgreSQL `DATABASE_URL` सेट करें।
- यह package ऐप को PWA के रूप में installable बनाने के लिए है; deployment के बाद live test करना अभी भी जरूरी है।


## CivilService Zone requested update
- `icons/icon-192.png` and `icons/icon-512.png` use the supplied logo; manifest app name is CivilService Zone.
- `help-video.mp4` is the supplied help video, served at `/help-video.mp4`.
- Registration/login UI now requires the same 4-digit password and role, rejects duplicate mobile registration, supports referral IDs and remembers a local session until logout.
- The top-right ⋮ menu provides app sharing, install, call/WhatsApp help, video, AI help, and theme cycling.

Important: authentication and referral rewards in this UI patch are stored in this browser's localStorage. For secure multi-device accounts and server-wide coupon balances, the server API must also be upgraded and tested with PostgreSQL before production use. Location access requires the user to grant browser permission; location links are not continuous GPS tracking.
