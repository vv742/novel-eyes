# 新建工程
> vite 是一个前端脚手架

* 我们需要用 vite + ts + react 来创建一个项目 
* 我们可以进入[官网](https://vitejs.cn/vite3-cn/guide/#browser-support)查看其信息

> pnpm 和 npm 一样是包管理工具, 而 pnpm 比 npm 快了近 2 倍

* `pnpm create vite`
    * 进入交互界面之后 输入:
        * 项目名 (name) novel-eye
        * 框架 (framework) react
        * 语言选择 (variant) typescript
* 执行一下指令
```bash
cd novel-eyes
pnpm install
pnpm run dev
```
> 执行后可以看到它给我们装了这么些个依赖:
```diff
PS D:\_temp\novel-eyes> pnpm install
   ╭──────────────────────────────────────────────────────────────────╮
   │                                                                  │
   │                Update available! 9.12.0 → 9.12.1.                │
   │   Changelog: https://github.com/pnpm/pnpm/releases/tag/v9.12.1   │
   │                Run "pnpm self-update" to update.                 │
   │                                                                  │
   │         Follow @pnpmjs for updates: https://x.com/pnpmjs         │
   │                                                                  │
   ╰──────────────────────────────────────────────────────────────────╯

Packages: +191
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Progress: resolved 229, reused 104, downloaded 87, added 191, done
node_modules/.pnpm/esbuild@0.21.5/node_modules/esbuild: Running postinstall script, done in 491ms
dependencies:
+ react 18.3.1
+ react-dom 18.3.1

devDependencies:
+ @eslint/js 9.12.0
+ @types/react 18.3.11
+ @types/react-dom 18.3.0
+ @vitejs/plugin-react 4.3.2
+ eslint 9.12.0
+ eslint-plugin-react-hooks 5.1.0-rc-fb9a90fa48-20240614
+ eslint-plugin-react-refresh 0.4.12
+ globals 15.11.0
+ typescript 5.6.3
+ typescript-eslint 8.8.1
+ vite 5.4.8
```

其中:

| 依赖项 | 功能 |
|-----|-----|
| react 18.3.1 | [Hook](https://zh-hans.react.dev/reference/react/hooks) [组件](https://zh-hans.react.dev/reference/react/components) [api](https://zh-hans.react.dev/reference/react/apis) [指示符](https://zh-hans.react.dev/reference/rsc/directives) |
| react-dom 18.3.1 | [Hook](https://zh-hans.react.dev/reference/react-dom/hooks) [组件](https://zh-hans.react.dev/reference/react-dom/components) [API](https://zh-hans.react.dev/reference/react-dom) [客户端API](https://zh-hans.react.dev/reference/react-dom/client) [服务端API](https://zh-hans.react.dev/reference/react-dom/server) |
| @eslint/js 9.12.0 | Javascript 的代码检查工具 |
| @types/react 18.3.11 | react 对 typescript 的支持 |
| @types/react-dom 18.3.0 | react-dom 对 typescript 的支持 |
| @vitejs/plugin-react 4.3.2 | 使用 esbuild 和 Babel，使用一个微小体积的包脚注可以实现极速的 HMR，同时提升灵活性，能够使用 Babel 的转换管线。在构建时没有使用额外的 Babel 插件，只使用了 esbuild。 |
| eslint 9.12.0 | eslint 代码检查 |
| eslint-plugin-react-hooks 5.1.0-rc-fb9a90fa48-20240614 | eslint react-hook 代码检查 |
| eslint-plugin-react-refresh 0.4.12 | react 热更新插件 |
| globals 15.11.0 | 全局变量库 |
| typescript 5.6.3 | typescript |
| typescript-eslint 8.8.1 | typescript 语言检测 |
| vite 5.4.8 | 项目脚手架 |

之后的步骤 [参考] https://www.viterc.cn/en/vite-chrome-extension.html

# 添加依赖
> 新建了工程之后我们需要安装我们自己需要的依赖以让项目具备相应的功能。

```bash
npm install @types/chrome -D
npm install @types/node -D
npm install rollup-plugin-copy -D
```

# 修改初版
## 修改 3 个配置文件
tsconfig.json
```json
{
  "compilerOptions": {
    "baseUrl": "./",
    "target": "ESNext",
    "useDefineForClassFields": true,
    "lib": ["DOM", "DOM.Iterable", "ESNext"],
    "allowJs": false,
    "skipLibCheck": false,
    "esModuleInterop": false,
    "allowSyntheticDefaultImports": true,
    "allowImportingTsExtensions": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "resolveJsonModule": true,
    "noEmit": true,
    "paths": {
      "@/*": ["src/*"],
    },
    "jsx": "react-jsx",
    "types": [
      "@types/chrome",
    ],
  },
  "include": ["./src"]
}
```
tsconfig.node.json
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["ES2023"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "isolatedModules": true,
    "moduleDetection": "force",
    "noEmit": false,
    "emitDeclarationOnly":true,
    "composite": true,

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["vite.config.ts"]
}
```
tsconfig.app.json
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "composite": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "isolatedModules": true,
    "moduleDetection": "force",
    "noEmit": false,
    "emitDeclarationOnly":true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "types": [
      "@types/chrome",
    ]
  },
  "include": ["src"]
}
```

## 添加 2 个 ts 文件