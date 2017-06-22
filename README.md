## 说明

基于gulp任务流的模板和静态资源版本化、combo工具

## 更新

* 2017.06.22 支持ywork.config.json中直接配置hash开关
* 2017.06.15 增加--hash参数,支持生成纯hash版本
* 2017.06.14 增加--skip参数,支持不升级版本号发布
* 2017.06.01 publish默认清理源css中的sourcemap以防冲突

## 安装

安装`npm install -g Yworkcli del-cli`

采用的是全局安装,命令行调用。

## 基础配置

在项目中新建`ywork.config.json`配置文件


```
{
    "static":{
        "path":"build/activity", //生成的项目资源路径
        "gtimgName":"activity", //对应的gtimg地址资源路径
        "output":"_prelease" //本地输出的编译后路径
    },
    "views":{
        "path":"src/views", //匹配的模板文件路径
        "output":"_previews"//最终生成的目录文件路劲
    },
    "configs":{
        "path":"src/node--config",//框架机config路径
        "output":"_prelease"//框架集config发布路径
    },
    "combo": {
        "force": true,//是否开启combo
        "gtimgTag":"<%= staticConf.domains.static %>",// 静态资源环境配置
        "gtimgNamePrepend":"readnovel", // combo串单独资源路由前置路径
        "uri":"<%= staticConf.domains.static %>/c/=",//combo的线上URL接口
        "logicCondition": "envType == \"pro\" || envType == \"oa\"" //开启combo的条件,注意需要转义双引号
    },
}

```

## 基础使用方法

由于`yworkcli`将核心构建任务完全配置化。可以理解成，通过上面的`ywork.config.json`配置静态资源和views的入口和出口。

项目路径执行`yworkcli --init`会初始化一个配置文件,大家务必按照自己的项目需求来配置。


不再强制约束文件夹格式，适用性更广。只需要保证保证框架机核心`config`配置，静态资源和模板自由度路径自由度更高。


#### 发布

在项目目录下(有`ywork.config.json`)，执行`yworkcli --publish --log './ywork.log'`

`--log {日志相对路径}`可以自定义日志，方便调试。

#### 不升版本发布

执行`yworkcli --publish --skip`，即可强制不生版本发布。

#### 生成HASH资源版本

执行`yworkcli --publish --hash`，即可生成hash版本,默认hash长度为5位。
