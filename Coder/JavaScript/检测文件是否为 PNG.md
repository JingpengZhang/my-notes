```js
const file = this.fileList[0].file;

const buffers = await file.arrayBuffer();
const uint8Array = new Uint8Array(buffers);
const pngHeader = [0x89, 0x50, 0x4e, 0x47, 0x0d, 0x0a, 0x1a, 0x0a];
const isPng = pngHeader.every(
   (byte, index) => uint8Array[index] === byte
);

console.log(isPng);
```