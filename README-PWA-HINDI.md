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
