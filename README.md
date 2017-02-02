## NodePress V1.0.0 开发文档

----------

> Author By Surmon Surmon@foxmail.com
>
> Site: http://surmon.me
>
> 前端前台PC端：[vue-blog](https://github.com/surmon-china/vue-blog) By Vue2 + Vuex
>
> 前端后台：[angular-admin](https://github.com/surmon-china/angular-admin) By Angular2
>

----------

# Todos & Issues
- 加入网站地图接口，同时驱动ping  https://github.com/ekalinin/sitemap.js
- 文章发布后自动ping给搜索引擎xml
- 对接百度统计开放平台api
- 密码存储需要使用加密机制


```bash
# 启动开发模式
nodemon --exec \"npm start\"
# 生产模式
pm2
```

## 接口

  - 处理流程

    ```
    首页路由 => 控制器 => 对应数据模型
    ```

----------

## 文件目录

  - 入口文件

    ```
    index.js -> 主程序入口

    启动Express程序，启动并连接数据库，路由分发，引入配置

    TODO: 配置检测，程序安装检测，数据库检测，待完善
    ```

  - 配置文件

    ```
    np-config.js -> 主程序配置

    数据库配置（程序内部），全局使用（程序内部），基本信息，其他配置

    TODO: 配置检测，程序安装检测，待完善
    ```

  - 数据库

    ```
    np-mongo.js -> 数据库连接启动

    连接并启动数据库

    TODO: 连接失败时前台应该可以得到提示
    ```

  - 公共封装函数

    ```
    np-common.js -> api/ctrl/model公共函数

    commonApiMethod -> API类型识别器

    commonCtrlPromise -> 控制器请求器

    commonModelPromise -> 数据层请求器

    TODO: 数据层请求器会导致控制器方法语义不清晰
    ```

  - 路由

    ```
    np-route/***.api.js -> 各功能API

    ```

  - 控制器

    ```
    np-controller -> 控制器文件夹

    ***.controller.js -> 各功能控制器

    ```

  - 数据模型

    ```
    np-model -> 数据模型文件夹

    ***.model.js -> 各功能数据模型，映射Mongoose对应的模型方法

    ```

  - 静态文件

    ```
    np-plugin -> 程序插件目录

    ```


----------

## 全站接口

  - 文章分类

    * 获取分类列表：

    ```
    API: /api/category  GET
    REMARK: 数组形式返回，需客户端自己组装嵌套数据
    ```

    * 添加分类：

    ```
    API: /api/category  POST
    DATA: {
        name: '分类名称',
        slug: 'cate_slug',
        pid: 'objectID' || null,
        description: '分类描述'
    }
    REMARK: pid和描述非必填项
    TODU: slug需具备唯一性，缺乏验证限制
    ```

    * 批量删除分类：

    ```
    API: /api/category  DELETE
    DATA: {
        categories: 'objectID,objectID,objectID,...'
    }
    ```

    * 获取单个分类（以及此分类上级关系）：

    ```
    API: /api/category/:category_id  GET
    PATH: {
        category_id: 'objectID'
    }
    REMARK: 数组形式返回，从前到后，分别是此分类的最高父级至自身
    ```

    * 修改单个分类：

    ```
    API: /api/category/:category_id  PUT
    DATA: {
        name: '分类名称',
        slug: 'cate_slug',
        pid: 'objectID' || null,
        description: '分类描述'
    }
    REMARK: 修改后返回最新数据，pid非必填，pid值应为objID || 0 || false || null
    TODU: slug需具备唯一性，缺乏验证限制
    ```

    * 删除单个分类：

    ```
    API: /api/category/:category_id  DELETE
    PATH: {
        category_id: 'objectID'
    }
    REMARK: 删除一个分类后，如果此分类包含子分类，则会将自己的子分类的pid自动更正为自己之前的pid或者NULL
    ```

----------

## 程序架构

  - 服务端

    * [Express](http://www.expressjs.com.cn/ )

    * [Express Generator](https://www.npmjs.com/package/express-generator) 中间件

    * [node-jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) JWT Json Web Token

  - 后台

    * [ng2-admin](https://akveo.github.io/ng2-admin/) [Angular 2](https://angular.cn/) MVVM

    * [Bootstrap 4](http://v4.bootcss.com/) UI

    * JQuery

    * 富文本编辑器 ---

    * [Simditor](http://simditor.tower.im/) Simditor

    * [Quill](http://quilljs.com/) Quill

    * [Draft.js](http://facebook.github.io/draft-js/) Draft for React

    * [bootstrap-wysiwyg](http://www.bootcss.com/p/bootstrap-wysiwyg/) bootstrap-wysiwyg

    * [wangEditor](http://www.wangeditor.com/) wangEditor

    * MarkDown ---

    * [Editor.md](http://pandao.github.io/editor.md/) MarkDown编辑器 - Editor

    * [MarkdownEditor](https://github.com/alecgorge/MarkdownEditor) 简单的MarkDown编辑器 - MarkdownEditor

    * WebIDE ---

    * [Codiad](https://github.com/Codiad/Codiad) WebIDE

    * [CodeMirror](http://codemirror.net/) CodeMirror WebIDE

    * Other ---

    * [谷歌云输入法]() 云输入法

    * [Web Audio Editor](http://audiee.io/) 音频处理（剪切处理）

    * [webgl-filter](https://github.com/evanw/webgl-filter) WebGL 图片处理 - webgl-filter

    * [h5slides](https://github.com/Jinjiang/h5slides) h5slides 幻灯放映

    * [H5lock](https://github.com/lvming6816077/H5lock) H5手势解锁

    * [favico.js](http://lab.ejci.net/favico.js/) 网站通知徽标

    * [OS.js](https://github.com/os-js/OS.js) OS.js Web OS

    * [Antiscroll](https://github.com/Automattic/antiscroll) Dom代替原生滚动条

    * [APlayer](https://github.com/DIYgod/APlayer) APlayer音频播放器

    * [CommentCoreLibrary](https://github.com/jabbany/CommentCoreLibrary) JS栈弹幕解决方案

    * [CommentCoreLibrary](https://github.com/jabbany/CommentCoreLibrary) JS栈弹幕解决方案

  - 搜索引擎

    * [Prerender.io](https://prerender.io/) SEO

    * [Handlebars](http://handlebarsjs.com/) HTML 渲染

    * [Vue服务端渲染](https://vuefe.cn/guide/ssr.html)

  - 前台PC端

    * [Vue2](http://cn.vuejs.org/) MVVM

    * [SOCKET.IO](http://socket.io/) 实时通讯

    * [HOWLER.JS](https://howlerjs.com/) 音频库

    * [Video.js](http://videojs.com/) 播放器

    * [vue-awesome-swiper](https://github.com/surmon-china/vue-awesome-swiper) 跑马灯

  - 前台WAP端

    * [Vue2](http://cn.vuejs.org/) MVVM

    * [Vux](https://github.com/airyland/vux) UI

  - Android/IOS客户端

    * [Weex](https://alibaba.github.io/weex/)

    * [NativeScript 2.0](https://www.nativescript.org/)

    * [React Native](http://reactnative.cn/)

----------

## 数据结构

  - 通用
    * extend 通用扩展
    ···

  - 分类 CRUD
    * name         - 分类名称 required
    * slug         - 分类名称 required onlyone 唯一!
    * description  - 分类名称
    * pid          - 父分类ID false || null || 0 || ObjectID
    ···

  - 文章 CRUD
    * title        - 文章标题
    * content      - 文章内容
    * description  - 文章描述
    * status       - 文章发布状态 => -1已删除，0草稿，1发布
    * public       - 文章公开状态 =>  0非公开，1公开
    * password     - 文章密码 => 非公开状态生效
    * date         - 发布日期
    * tag          - 文章标签 数组 ObjID
    * category     - 文章分类 数组 ObjID
    * comment      - 数组（对象）
    * sidebar      - 边栏展示 -> 0不显示，1left，2right
    * meta         - 元数据 views: Number, favs:  Number
    ···

----------

## 插件机制

----------

