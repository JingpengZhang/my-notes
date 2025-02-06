```js
const fs = require('fs')

/**
 * 删除指定目录下所有子文件
 * @param {*} path 
 */
 function emptyDir(path) {
  const files = fs.readdirSync(path);
  files.forEach(file => {
      const filePath = `${path}/${file}`;
      const stats = fs.statSync(filePath);
      if (stats.isDirectory()) {
          emptyDir(filePath);
      } else {
          fs.unlinkSync(filePath);
      }
  });
}

// 打包文件输出文件夹
const outputDir = './dist'

// 输出提示
console.log('\x1B[33m\udb81\udd41  正在将打包文件复制到 ' + outputDir +' 文件夹 \x1B[0m');

// 检查目标文件夹是否存在
if(fs.existsSync(outputDir)){
  // 存在，则清空所有文件和文件夹
  emptyDir(outputDir)
}else{
  // 不存在，创建
 fs.mkdirSync(outputDir)
}

// 复制打包后的必要文件到输出文件夹中
fs.cpSync('./.next/standalone',outputDir,{
  recursive:true,
  filter:(file)=>{
    return file.indexOf('node_modules') === -1;
  }
})

// 复制 public 文件夹 和 ./.next/static 文件夹
// NextJS 官方建议这两个文件夹应该由CDN处理
fs.cpSync('./public',outputDir + '/.next/public',{recursive:true})
fs.cpSync('./.next/static',outputDir + '/.next/static',{recursive:true})

// 输出提示
console.log('\x1B[32m\udb83\ude29  已复制到 ' + outputDir +' 文件夹 \x1B[0m');
```