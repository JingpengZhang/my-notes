```ts
// 网页分辨率
const resolution = {
	x: 1920,
	y: 1080
}

// 物体尺寸
const width = 19.2;
const height = 10.8;

const wrapper = document.createElement('div');

// 设置 dom 容器尺寸为分辨率数值
wrapper.style.width = resolution.x + 'px';
wrapper.style.height = resolution.y + 'px';
      
wrapper.style.backgroundColor = 'white'

const iframe = document.createElement('iframe');

iframe.src = 'https://www.showinfo.com.cn/'
iframe.style.height = '100%'
iframe.style.width = '100%'

wrapper.appendChild(iframe);

const css3d = new CSS3DObject(wrapper);

// 调整物体到指定尺寸，先除以分辨率，将尺寸恢复到 1 个单位
css3d.scale.setX(1 / resolution.x * width);
css3d.scale.setY(1 / resolution.y * height)
```