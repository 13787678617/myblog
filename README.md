# 修复

- 修复前台显示草稿内容的bug
- 修复博客详情页面，手机扫码阅读博客功能不能跳到指定博客的bug
- 修复archives归档页面，博客超出一定数量(大于15)时，页面显示错乱，只显示15篇博客，后面的博客显示不全的bug
- 修复archives归档页面，根据年份归档，当存在三个年份归档，如分别存在2018年 2019年 2020年份的博客，实际排序为2019 2018 2020，顺序排序错误的bug
- 修复index页面，最新动态未按发布博客时间最近排序的bug
- 修复博客评论区，子评论在第三层时，此时回复会追加第二层的回复的bug
- 修复博客后台，markdown编辑器内图片上传框显示问题
# 新增

- 前端博客美化效果：雪花效果，动态背景线条效果，点击显示文字效果

  - 雪花效果相关配置：
    - resources/static/js/snow.js文件内，有详细注释说明
    - 可配置雪花颜色，大小，密集程度

  - 动态背景线条相关配置：
    - _fragments.html第232行
    - 可配置颜色，透明度

  - 点击显示文字效果相关配置：
    - resources/static/js/click_show_text.js文件内，可自定义随机显示的文字

- 引入天气插件，固定在页面左上角。

- 引入网易云音乐插件，固定在右下角。在_fragments.html文件的id="netEasy-music"元素内可自行替换歌单(已去除)

- 引入APlayer音乐播放器

- 引入Live-2D模型，\lib\live2d-widget\waifu-tips.js文件内第160行可修改默认显示的模型样式

- 适配移动端，以上博客美化样式，天气插件与Live-2D在手机端不显示

- 底部footer网站运行计时，在_fragments.html文件createtime( ) JS方法内自行替换建站时间

- 博客分享功能，支持携带首图，博客标题分享，并自定义分享描述

  - 支持微信，微博，QQ好友，QQ空间分享。
  - 相关配置在blog.html内的shareQQ()，shareQQZone()，shareWeiXin()，sinaWeiBo()方法内。

- 博客评论新加表情支持，后续会加入b站相关表情

- 新增博客留言页面

- 留言页面支持邮件回复通知，开启后评论，当评论被回复后会收到一封邮件，邮件支持表情显示

  ![1585082833194](http://cdn.xiongsihao.com/1585082833194.png)

  ![1585083340531](http://cdn.xiongsihao.com/1585083340531.png)

**注：邮件回复功能需先开启邮箱POP3/SMTP服务**

支持163邮箱和QQ邮箱，application.yml文件内有详细注释自行替换

**test包下有相关邮件的测试类，自行调试；测完记得注释上，否则打包时可能会报错**

- 留言页面有发送手机验证码的demo，此功能可以了解一下；因为觉得博客登录验证手机号有点多此一举，就没有做手机号的相关流程

  **注：如需使用发送验证码功能，需先[进入阿里云](https://account.aliyun.com/login/login.htm)，开通短信平台服务，申请短信模板与签名，开通成功后会获得四个参数：Id，Secret，签名名称，模板名称，填入application.yml配置文件sms内就可以使用验证码了**

目前写死了短信发送验证码为2333333，如需修改可进入java/customer/SmsCustomer文件内第44行修改；如需随机6位验证码，则将43行取消注释，将44行注释上。

![img](http://cdn.xiongsihao.com/AFC7CAFD8B562908EAAC5192A201E133.jpg)

- 新增第三方登录——QQ登录方式

  如需此功能，需先申请QQ互联开发者，申请通过后会得到三个参数：appid，appkey，回调地址。

  自行替换application.yml配置文件内的QQ登录相关参数，更多详细步骤请[点击此处](http://xiongsihao.com/blog/37)。

  登录后预览：

  ![1585084340317](http://cdn.xiongsihao.com/1585084340317.png)

- 新增第三方登录——Github登录方式

  如需此功能，需先进入github账号，点击右上角头像选择setting，进入后选择底部Developer settings再点击New GitHub App,填写相关资料后无需审核就能直接使用；如果不知道怎么填可以留言或者百度。

  登录后预览：

  ![1585084719802](http://cdn.xiongsihao.com/1585084719802.png)

说明：因为github是外网，登录时，可能会请求登录连接超时，此为正常情况；

登录后大概率会加载不出github用户原有头像(同样因为外网，网速慢的原因)；所以我保存了20张github头像，通过github方式登录后会随机从20张图片内选一张作为头像。

- 新增QQ与github账号头像替换功能

  因为图片存储使用的是七牛云第三方云存储图片，所以使用此功能需要到[七牛云官网](https://portal.qiniu.com/)注册好账号并建好图片存储仓库，免费10个G，申请好之后同样会获得四个参数：accessKey，secretKey，bucket，path

  自行替换到application.yml文件内

  选择上传图片界面：

  ![1585085577871](http://cdn.xiongsihao.com/1585085577871.png)

  修改头像成功后：

  ![1585085632274](http://cdn.xiongsihao.com/1585085632274.png)

点击确定既刷新头像，此时显示的为新换头像

- **新增评论称号**

  在原版的是否为管理员评论基础上，修改并增加了游客，访客，博主，gayhub四个称号;

  - 游客：无登录状态的评论，头像为默认头像
  - 访客：使用QQ账号登录并评论，头像为QQ头像，名字为QQ昵称
  - gayhub：使用github账号登录并评论，头像为github账号，名字为github昵称
  - 博主：根据application.yml配置文件内admin.openid识别博主是谁，参数为QQ登录后的openid

  **可以用类似博主称号的方法，为指定人赋予指定评论称号**

- 记录QQ与Github账号登录状态，既登录后关闭浏览器再打开时还是登录状态；此处设置了cookie过期时间为10天(10天不操作自动退出登录)，如需修改时长，则修改application.yml配置文件内cookie.time参数

  

- rabbitmq监听验证码发送情况，并使用redis保存验证码与发送手机号，五分钟内过期；虽然手机验证码功能目前没有具体使用，但也可以了解一下。

- 限制手机验证码发送情况：当前限制为同一个手机号一小时内只能发一条短信，如需解除限制，则将message_board.html文件的$('#btn_ok3').click(function()里面的第一个if判断语句注释上

- 博客管理后台，blog-input.html页面实现图片上传回显功能

  ![](http://cdn.xiongsihao.com/202005252121_78.png)

# 部署

- 修改jdbc连接参数
- 修改application.yml内的baseUploadUrl参数，详情见yml文件注释
- 使用qq登录，github登录，图片上传，验证码发送功能，需申请对应账号并填入yml配置文件
- 数据库，为防止字段冲突，最好新建一个空数据库部署此项目(当然也可以直接update)

如出现任何问题，欢迎[点击此处](http://xiongsihao.com/Messages)留言

--------------------------------------------------------------最后...如果你觉得对你有帮助，求star