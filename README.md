# ElectronCourse
- 使用Electron将Vue项目打包成桌面应用

- Electron 可以让你使用纯 JavaScript 调用丰富的原生 APIs 来创造桌面应用。你可以把它看作是专注于桌面应用而不是 web 服务器的，io.js 的一个变体。
这不意味着 Electron 是绑定了 GUI 库的 JavaScript。相反，Electron 使用 web 页面作为它的 GUI，所以你能把它看作成一个被 JavaScript 控制的，精简版的 Chromium 浏览器

## 文档

- [Electron官网](https://electronjs.org/)
- [API使用文档](https://electronjs.org/docs)

## 快速学习

### 一、 Hello World

```
git clone https://github.com/electron/electron-quick-start //下载electron-quick-start

cd electron-quick-start //进入electron-quick-start目录

yarn install //安装依赖

//如果install失败可以全局安装electron、electron-prebuilt
yarn install -g electron
yarn install -g electron-prebuilt

yarn start //运行
```

目录结构

```
your-app/
├── package.json      ——配置文件
├── main.js           ——入口文件
└── index.html        ——需要展示文件
```

### 二、 运行自己的Vue项目

1、打包Vue项目（别忘了打包前的配置）
2、将打包文件拷贝到electron-quick-start并覆盖其中的index.html
3、运行yarn run start

### 三、 在Vue项目中使用Electron

#### 1、安装依赖

```
cd 到自己的项目目录
yarn install electron --save-dev 
yarn install electron-packager --save-dev
```

#### 2、配置文件的准备
- 拷贝electron-quick-start中的main.js到Vue项目中的build文件夹下并修改名字为electron.js
- 修改文件目录：打开electron.js修改引用地址如下
```
mainWindow.loadURL(url.format({
    pathname: path.join(__dirname, '../dist/index.html'),
    protocol: 'file:',
    slashes: true
  }))
```

- 修改package.json：在scripts中新增如下命令

```
	"electron_dev": "npm run build && electron build/electron.js",
	"electron_build": "electron-packager ./dist/ --platform=win32 --arch=x64 --icon=./src/assets/favicon.ico --overwrite"
```
electron_dev：预览启动命令
electron_build：打包exe启动命令

- 启动命令说明：
```
"electron_build": electron-packager <location of project> <name of project> <platform> <architecture> <electron version> <optional options>

//栗子：
"electron_build": "electron-packager ./dist/ HelloWorld --platform=win32 --arch=x64 --icon=./src/assets/favicon.ico --overwrite"
```
- location of project：表示项目所在路径
	
- name of project：打包的项目名字
	
- platform：确定了你要构建哪个平台的应用（Windows、Mac 还是 Linux）
	
- architecture：决定了使用 x86 还是 x64 还是两个架构都用
	
- electron version：electron 的版本
	
- optional options：可选选项

注意：字段里的 项目名字，version，icon路径要改成对应项目的

#### 3、运行yarn run electron_dev即可预览Vue项目

#### 4、打包exe文件
- 运行yarn run build
- 拷贝electron-quick-start中的main.js和package.json文件到dist文件夹下（注意修改js和package.json文件中的信息为自己项目的信息）
- 运行yarn run electron_build
- 找到打包后的文件夹找到其中的 .exe 文件，双击即可查看效果

#### 其他说明
- 个人开源的Vue播放器打包的桌面应用
- [mmPlayer下载](http://img.mtnhao.com/mmPlayer.zip)
