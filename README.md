# QR Cat
WebExtensions extension written in svelte to display the QR code of the current URL.
The implementation generates a level "H" QR but superimposes a cat image on the code, which covers around 15% of the code. Thus the QR code is effectively a level "M" instead since no more than approximately 15% error is allowable before the code is unreadable.

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
sh package. sh
```
