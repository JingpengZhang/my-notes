### PDFMaker.js

选用 `PDFMaker` 库，可支持中文字体，[PDFMaker 官网](http://pdfmake.org/)

### 支持中文字体

下载中文字体文件 `xxx.ttf`，例如 `FangZhengShuSong-GBK-1.ttf` （下载地址：[方正书宋GBK](https://fileres.fonts.net.cn/font-31610.zip?response-content-disposition=attachment%3Bfilename%3D%22FangZhengShuSong-GBK.zip%22&auth_key=1740965396-67c505d827f912x02471128-0-c94a47277173e39672c10853f30409ba)）；

下载 PDFMaker.js 源码（从[GitHub仓库](https://github.com/bpampuch/pdfmake)克隆）；

将下载的字体文件放入 `example/fonts` 文件夹中， 如果不需要默认的字体支持，可以先清空这个文件夹。

在源码根目录运行脚本：

```bash
node build-vfs.js ./examples/fonts
```

将会生成 `./build/vfs_fonts.js` 文件。


### 使用

将 `build` 文件夹中的 `pdfmake.min.js`  以及 `vfs_fonts.js` 这两个文件拷贝到项目中即可使用，这里以 'vue2' 项目举例。

```vue
<script>
export default {
	methods:{
	   // 处理导出
	    async handleExport() {
	      this.pdfMake = require("../../../plugins/pdfmake.min.js");
	      console.log(this.pdfMake, this.pdfMake.vfs);

	      if (this.pdfMake.vfs === undefined) {
	        const fonts = require("../../../plugins/vfs_fonts.js");
	        console.log(fonts);
	        this.pdfMake.vfs = fonts;
	      }

	      pdfMake.fonts = {
			// 如果不确定打包的
	        FZFS: {
	          normal: "FangZhengShuSong-GBK-1.ttf",
	          bold: "FangZhengShuSong-GBK-1.ttf",
	          italics: "FangZhengShuSong-GBK-1.ttf",
	          bolditalics: "FangZhengShuSong-GBK-1.ttf",
	        },
	      };
	      
	      const docDefinition = {
	        content: "测试,Hellow",
	        defaultStyle: { font: "FZFS" },
	      };
	      this.pdfMake.createPdf(docDefinition).download("测试.pdf");
    },
  }
}
</script>
```

