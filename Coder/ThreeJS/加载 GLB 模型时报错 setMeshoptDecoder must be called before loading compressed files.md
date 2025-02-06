在加载使用 Meshopt 压缩的 GLTF/GLB 模型时，需要正确配置 `GLTFLoader` 来使用网格优化解码器。
```js
import { MeshoptDecoder } from 'three/examples/jsm/libs/meshopt_decoder.module.js';

// 设置 Meshopt 解码器
loader.setMeshoptDecoder(MeshoptDecoder);
```