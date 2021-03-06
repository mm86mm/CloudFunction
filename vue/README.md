# BmobJava云函数-Vue

*只需要云函数服务，就可以一键部署你的Vue项目*

*请注意，该功能的目的并非专用于Vue项目，而是对延伸Java云函数功能的一种展示。更多的是希望帮助开发者理解Java云函数的使用。工作原理可以参考[NotFound示例](//github.com/bmob/CloudFunction/tree/master/vue/NotFound.java)的源码*

[示例网站](//javacloud.bmob.cn/f7693b7e98a35ed6)

## 发布步骤

*以下指令操作是基于Linux、Mac系统，windows系统请自行修改文件分隔符*


1. 编写Vue项目

2. 修改 `config/index.js` 的 `assetsPublicPath` 为 `./` （默认为 `/`）

3. `npm run build`

4. 修改 `./dist/index.html`，加入 `<-- VERSION[1] -->`

5. 在Vue项目根目录调用 `python tools/gzip_bmobjavacloud.py ./dist` 进行Gzip预处理，降低流量，增加响应速度

6. 在dist目录下压缩项目，调用 `zip -r dist.zip ./`

7. 登陆bmob官网后台，创建一个云函数，语言为**Java**，函数名为`NotFound`（大小写不敏感）

8. 将 [NotFound示例](//github.com/bmob/CloudFunction/tree/master/vue/NotFound.java) 内的内容复制进去，点击保存

9. 在Bmob数据库创建表，名为`WebProject`，并新建字段`version`(Number类型)、`project`(File类型)

10. 新增一行WebProject数据，`version`为1，`project`点击上传步骤6生成的zip文件

11. 打开 `https://javacloud.bmob.cn/[secret key]` 即可看到你的Vue项目(secret key从bmob后台查看)

## 注意事项

- 请勿在项目内放置大文件例如高清图片等，云函数有一些限制
- 如果对目录结构、更新文件有兴趣，请详细阅读[NotFound示例](//github.com/bmob/CloudFunction/tree/master/vue/NotFound.java)中的代码
- 如果Vue项目较为大型，可联系客服升级云函数配置
- Vue示例代码来自[PanJiaChen/vue-admin-template](//github.com/PanJiaChen/vue-admin-template)，感谢作者的无私奉献
- 该功能尚在测试阶段，如果需要正式上线或用自己的域名，请联系客服
