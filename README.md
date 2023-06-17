# QR Cat
WebExtensions extention written in svelte to display qr code of current url.
The implementaion generates a level "H" QR but superimposes a cat image on the code which covers around 15% of the code. Thus the QR code is effecticly a level "M" instead since no more than approxiamly 15% error is allowable before the code in unreadable.

![image](https://github.com/amar-b/qr-cat/assets/32601358/3ce121e5-2a28-44be-883c-4bb119dbf630)

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
