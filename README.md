# QR Cat
WebExtensions extention written in svelte to display qr code of current url.
The implementaion generates a level "H" QR but superimposes a cat image on the code which covers around 15% of the code. Thus the QR code is effecticly a level "M" instead since no more than approxiamly 15% error is allowable before the code in unreadable.

### Get started
```bash
npm install
npm run dev
```

### Building and running in production mode
```bash
npm run build
npm run start
```

### Packaging to a zip file
```bash
sh package.sh
```