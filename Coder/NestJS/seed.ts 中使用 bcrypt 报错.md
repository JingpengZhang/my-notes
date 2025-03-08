在 `prisma/seed.ts` 文件中使用到了 `bcrypt` 依赖后，在使用 `npx prisma db seek` 命令向数据库填充初始数据时，报如下错误：

```shell
Environment variables loaded from .env
Running seed command `ts-node --compiler-options {"module":"CommonJS"} prisma/seed.ts` ...
Error: Cannot find module '/Users/jingpengzhang/Projects/Peng/poccur_server/node_modules/.pnpm/bcrypt@5.1.1/node_modules/bcrypt/lib/binding/napi-v3/bcrypt_lib.node'
Require stack:
- /Users/jingpengzhang/Projects/Peng/poccur_server/node_modules/.pnpm/bcrypt@5.1.1/node_modules/bcrypt/bcrypt.js
- /Users/jingpengzhang/Projects/Peng/poccur_server/prisma/seed.ts
    at Function.<anonymous> (node:internal/modules/cjs/loader:1405:15)
    at Function.Module._resolveFilename.sharedData.moduleResolveFilenameHook.installedValue [as _resolveFilename] (/Users/jingpengzhang/Projects/Peng/poccur_server/node_modules/.pnpm/@cspotcode+source-map-support@0.8.1/node_modules/@cspotcode/source-map-support/source-map-support.js:811:30)
    at defaultResolveImpl (node:internal/modules/cjs/loader:1061:19)
    at resolveForCJSWithHooks (node:internal/modules/cjs/loader:1066:22)
    at Function._load (node:internal/modules/cjs/loader:1215:37)
    at TracingChannel.traceSync (node:diagnostics_channel:322:14)
    at wrapModuleLoad (node:internal/modules/cjs/loader:235:24)
    at Module.require (node:internal/modules/cjs/loader:1491:12)
    at require (node:internal/modules/helpers:135:16)
    at Object.<anonymous> (/Users/jingpengzhang/Projects/Peng/poccur_server/node_modules/.pnpm/bcrypt@5.1.1/node_modules/bcrypt/bcrypt.js:6:16) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [
    '/Users/jingpengzhang/Projects/Peng/poccur_server/node_modules/.pnpm/bcrypt@5.1.1/node_modules/bcrypt/bcrypt.js',
    '/Users/jingpengzhang/Projects/Peng/poccur_server/prisma/seed.ts'
  ]
}

An error occurred while running the seed command:
Error: Command failed with exit code 1: ts-node --compiler-options {"module":"CommonJS"} prisma/seed.ts
```

#### 解决办法

进入  `/Users/jingpengzhang/Projects/Peng/poccur_server/node_modules/.pnpm/bcrypt@5.1.1/node_modules/bcrypt/` 目录，运行如下命令编译 `bcrypt`：

```shell
node-pre-gyp install --fallback-to-build
```


#### 参考

https://github.com/kelektiv/node.bcrypt.js/issues/800