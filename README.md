# 一、概述

Hexo 是一个快速、简洁且高效的博客框架。 Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他标记语言）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

该项目为官方是入门示例，启动成功后将展示欢迎页。

**预装环境：** `node v18.13.0` `create-react-app`  `pnpm`  `yarn`  `node-gyp`  `git` 等。

注：npm & yarn默认配置了腾讯云仓库。

## 二、快速开始

使用如下命令，快速运行一个 Hexo 程序：

```
// 安装依赖包
yarn install
// 运行示例程序
yarn run server
```

**输出结果：**

<img title="" src="img\output.png" alt="" width="194">

### 三.  文件结构

```
workspace/
├── _config.landscape.yml        // 特定布局主题配置
├── _config.yml        // 主配置文件 
├── package.json             // 依赖包引用
├── README.md                // 项目说明文档
├── scaffolds        //模板文件夹。新建文章时，Hexo 会根据 scaffold 来建立文件
│   ├── draft.md
│   ├── page.md
│   └── post.md
├── source            //资源文件夹。 是存放用户资源的地方。
│   └── _posts
│       └── hello-world.md    // 初始欢迎页
├── themes            // 主题文件夹。 Hexo 会根据主题来生成静态页面。
│   └── .gitkeep   
└── yarn.lock
```

### 2.  Hexo 官方文档与资源

[文档 | Hexo](https://hexo.io/zh-cn/docs/index.html)

[故障排除 | Hexo](https://hexo.io/zh-cn/docs/troubleshooting.html)

[配置 | Hexo](https://hexo.io/zh-cn/docs/configuration)

[markdown 帮助文档](https://https://markdown.com.cn/basic-syntax/.com.cn/basic-syntax/)

[GitHub · hexo issues](https://github.com/hexojs/hexo/issues)

[npm官网](https://www.npmjs.com/)

[yarn官网](https://www.yarnpkg.cn/)

## 三、  常见问题

[Cloud Studio（云端 IDE） 常见问题-文档中心-腾讯云](https://cloud.tencent.com/document/product/1039/33505)

[Cloud Studio 轻量版 帮助文档](https://docs.qq.com/aio/DRUFZcHVvZlJuY3l2?p=1QOiTiIR9g0KMJneBDyfgM)

[Cloud Studio（云端 IDE） | Cloud Studio](https://ide.cloud.tencent.com/docs/)

## 帮助和支持

##### 欢迎加入Cloud Studio用户反馈群

当您遇到问题需要处理时，您可以直接通过到扫码进入Cloud Studio用户群进行提问.

- 腾讯云工程师实时群内答疑

- 扫码入群可先享受产品上新功能

- 更多精彩活动群内优享

<img title="" src="img/qr-code.png" alt="qr-code.png" width="270">
