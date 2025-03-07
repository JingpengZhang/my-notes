> CSS3DRenderer 可用于通过 CSS3 transform 属性将分层 3D 转换应用于 DOM 元素。如果您想将 3D 效果应用于没有基于画布的渲染的网站，此渲染器特别有趣。它也可以用于将 DOM 元素与 WebGL 内容相结合。 -- ThreeJS 官方文档

### 问题
在使用 CSS3DRender 渲染 iframe 时,可能会出现在某些角度下(使用 OrbitControls 旋转场景),鼠标无法与 iframe 中的元素交互的问题:
```js
// * 创建 iframe 元素
const iframe = document.createElement("iframe");
iframe.style.width = "1920px";
iframe.style.height = "1080px";
iframe.src = "https://www.youtube.com/embed/SJOz3qjfQXU?rel=0";

// * 构造 CSS3DObject 对象
const iframe3DObj = new CSS3DObject(iframe);
iframe3DObj.scale.set(0.005, 0.005, 0.005);
iframe3DObj.position.setY(2);
scene.add(iframe3DObj);
```

### 解决方案
在 iframe 元素的外面套一个容器元素即可解决该问题,具体原因未知.
```js
// * 创建 iframe 容器元素
const iframeWraper = document.createElement("div");
iframeWraper.style.width = "1920px";
iframeWraper.style.height = "1080px";
iframeWraper.style.backgroundColor = "#000";

// * 创建 iframe 元素
const iframe = document.createElement("iframe");
iframe.style.width = "1920px";
iframe.style.height = "1080px";
iframe.src = "https://www.youtube.com/embed/SJOz3qjfQXU?rel=0";

// * 将 iframe 元素添加到 iframe 容器元素
iframeWraper.appendChild(iframe);

// * 构造 CSS3DObject 对象 (使用 iframe 容器元素构造)
const iframe3DObj = new CSS3DObject(iframeWraper);
iframe3DObj.scale.set(0.005, 0.005, 0.005);
iframe3DObj.position.setY(2);
scene.add(iframe3DObj);
```
