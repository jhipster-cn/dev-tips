##  这里用来记录大家日常开发 JHipster 的一些经验，或者已经踩到的坑。欢迎大家补充

###  如何解决国内安装前端依赖库缓慢、失败的问题？

设置淘宝镜像源，以及 sass_binary_site 和 phantomjs_cdnurl 等二进制包下载地址
```
yarn config set  registry https://registry.npm.taobao.org
yarn config set  sass_binary_site https://npm.taobao.org/mirrors/node-sass/
yarn config set  phantomjs_cdnurl https://cdn.npm.taobao.org/dist/phantomjs
yarn config set  electron_mirror http://cdn.npm.taobao.org/dist/electron/ 
```

如果是 npm ,则使用  `npm  config` 替换上面的 `yarn config`   。

由于 cnpm 对 npm 的兼容不是很好，并不推荐 cnpm 。比如用  cnpm 安装依赖后，使用 `npm ls -g --depth=0` 命令会报错。

更多二进制包下载地址，参见 [淘宝 npm 镜像站](https://npm.taobao.org/mirrors)

---

### 当修改完 generator-jhipster 源码之后，如何使用自己的生成器，而不是已经安装在全局的 generator-jhipster？

假设你已经 `clone generator-jhipster` 的源码到 `~/my-generator-jhipster ` 目录下，并且修改了代码。

你可以在该目录下，使用 `yarn link` 或者  `npm link` 命令，该命令会在你的全局 node_modules 目录下建立一个软链。

比如`/home/your-name/.nvm/versions/node/v7.5.0/lib/node_modules/generator-jhipster -> ~/my-generator-jhipster`。

当你新建一个项目 my-project ,在 my-project 的目录下，使用`npm link generator-jhipster`。这样，当你在运行 `yo jhipster` 的时候，就会使用你的代码了。

其实这一点在 [CONTRIBUTING.MD](https://github.com/jhipster/generator-jhipster/blob/master/CONTRIBUTING.md) 有说到。


---

###  每次创建项目都要回答10多个问题，有没有快速一点的办法创建项目？

当然可以，当你用 JHipster 创建一个项目之后，在你创建的项目目录下，会有一个`.yo-rc.json` 的文件，这里记录了你在创建该项目时所回答的全部问题。

你可以通过 cp 一份这样的文件到一个新项目的目录下，然后运行 `yo jhipster`，你就可以快速的生成新的项目。

---

### 如何生成一个只有中文的项目？

JHipster 在生成项目的时候会询问你是否需要支持国际化：
```
? (11/15) Would you like to enable internationalization support? Yes                        
? Please choose the native language of the application? Chinese (Simplified)                            
? Please choose additional languages to install ?    这里不要按空格，直接 enter 键跳过
```

或者你可以直接修改 `.yo-rc.json` 实现的，让 languages
```
"languages": [                                                                                       
      "zh-cn"                                                                                           
    ],
```

### 如何只生成一个包含前端、服务端的项目？

运行 `yo jhipster:client`  或者 `yo jhipster --skip-client`。

更多参数，参见 `yo jhipster --help`。

参见官方文档 [创建一个应用](https://jhipster.github.io/creating-an-app/#4)

---

###  升级 generator-jhipster  不成功？

目前官方推荐 `yarn global upgrade generator-jhipster` 来升级，但有时候运行之后，使用 `yo jhipster` 还是会显示旧的版本。

这个时候可以尝试一下 `npm install -g generator-jhipster`。

如果还是不行，可以尝试用  `npm uninstall -g  generator-jhipster` 卸载，然后重装。