#### 1. 创建 vue3 + ts 项目
```bash
npx degit dcloudio/uni-preset-vue#vite-ts 项目名
```

### 2. 安装类型声明文件（TypeScript）
```shell
pnpm i -D @types/wechat-miniprogram @uni-helper/uni-app-types
```

### 3. 配置 tsconfig.json
```json
{

"extends": "@vue/tsconfig/tsconfig.json",

"compilerOptions": {

"sourceMap": true,

"baseUrl": ".",

"paths": {

"@/*": ["./src/*"]

},

"lib": ["esnext", "dom"],

"types": [

"@dcloudio/types",

"@types/wechat-miniprogram", // ++

"@uni-helper/uni-app-types" // ++

]

},

"vueCompilerOptions": { // ++

"nativeTags": ["div", "img", "..."] // ++

}, // ++

"include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"]

}
```