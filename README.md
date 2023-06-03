# AGA

## 准备工作

1. **数据库 Schema** - 简单，记为A

    > 根据数据库设计，写好所有表的Schema，目前的表只是参考，后续开发过程如果遇到问题，可以修改Schema来适应功能

2. **JWT 中间件，axios请求发送，redux保存** - 困难，记为B

    > 开发后端 JWT 的auth中间件，中间件被添加进router表示此router需要登陆才能继续。redux保存JWT和userid。前端对Axios进行包装，检查redux是否有用户的JWT，如果有自动加在请求头里，如果JWT过期自动登出清空redux并提示。

3. **邮件服务** - 简单，参考[文档](https://docs.sendgrid.com/for-developers/sending-email/quickstart-nodejs)，记为C

    > 看文档，申请sendgrid账号，在后端实现：调用一个utils函数即可向一个指定邮箱发送一段指定内容

4. **文件服务** - 困难，记为D

    > AWS S3 文件上传，公有访问和**预签名 URL**访问

5. **拍照功能** - 困难，记为L

## 显示平台简介

1. **home前端** - 简单，参考[页面](https://prossliu.wixsite.com/crankbit)

    > 仅前端静态开发，组件放在component文件夹内，页面调用这些component并传参

2. **contact us前端** - 简单，参考[页面](https://prossliu.wixsite.com/crankbit/blank-2)

    > 同上

3. **about前端** - 简单，参考[页面](https://prossliu.wixsite.com/crankbit/blank-4)

    > 同上，收集组内人员信息

4. **C - 联系邮件发送** - 简单

    > 前置C，需要等待C完成，用户可以通过这个功能**匿名**发送反馈或者咨询给所有管理员用户的邮箱

## 登陆注册 与 用户管理

1. **登录注册前端页面** - 中等，参考[登陆页面](https://zone-ui.vercel.app/auth/login-cover/)，[注册页面](https://zone-ui.vercel.app/auth/register-cover/)

    > 用户可以注册账户和登录到平台的页面，需要验证用户输入的内容

2. **连接前端后端（邮箱验证）** - 困难，记为E

    > 连接前端后端，让注册登陆变的可用（可选通过邮箱验证，前置C），还可以在NavBar上登出

3. **E - 用户角色管理** - 困难，参考[List页面](https://material-kit-pro-react.devias.io/dashboard/customers)

    > 展示所有用户，设置用户角色，禁用用户（可选查看用户邮箱验证状态），点击可以查看用户信息（H - 查看机械师信息）（M - 查看用户车辆信息）

4. **E - Google登录** - 中等，参考[视频](https://www.youtube.com/watch?v=LKlO8vLvUao&ab_channel=JavaScriptMastery)

    > 提供用户通过Google账户登录的功能，google账户和数据库的user一一对应

## 个人中心

1. **tabs前端** - 简单，记为F，参考[Tab页面](https://prossliu.wixsite.com/crankbit/account/my-account)

    > 只做tab，My Account（All），My Appointment（User），My Information（Mechanic），View Mechanic List（User），View Mechanic Application（Admin），My Vehicle（All），Manage Appointment（Admin）根据不同角色展示

2. **DE - My Account修改用户个人信息** - 中等

    > My Account tab 用户修改姓名密码头像（可选修改密码需要邮件验证）

3. **DEL - 升级为机械师** - 困难，记为G

    > 在My Account tab上有一个按钮可以申请成为机械师账号，需要上传一些内容（Tom来设计），设置可用服务项目和价格，设定可选时间

4. **FG - My Information 修改机械师信息并展示View Mechanic List** - 复杂，记为H，参考[机械师列表页面](https://material-kit-pro-react.devias.io/dashboard/blog)，参考[机械师详情页面](https://material-kit-pro-react.devias.io/dashboard/jobs/companies/:companyId)

    > 展示机械师上传的信息，通过一个Edit button可以将页面变成edit mode，未通过审核的只能自己查看。如果通过审核，用户可以在View Mechanic List tab看到其头像和名称简介，点进去可以查看view mode only。

5. **CH - View Machinist Application** - 中等

    > 使用View Mechanic List tab的组件，但只展示需要Approve的Mechanic， view mode only但是多了一个Approve button和一个Decline reason输入框，当申请被拒绝后，机械师将受到被拒绝的邮件和reason，机械师可以重新申请。成功也发送邮件提醒。

6. **CE - Contact Admin** - 简单

    > contact us的复制，发送邮件，但是不再匿名（在邮件中附User的信息）

7. **DEL - My Vehicle** - 复杂，记为M，参考[步骤进度条页面](https://material-kit-pro-react.devias.io/dashboard/academy/courses/:courseId)，参考[每个步骤的数据录入页面](https://material-kit-pro-react.devias.io/dashboard/products/create)

    > 只能录入一辆车（Tom来设计）同样具有View mode和Edit mode

## 预约与服务

1. **H - 发送预约和服务详情页面** - 中等，记为I，参考[My Appointment tab页面](https://material-kit-pro-react.devias.io/dashboard/invoices)，[服务详情页面](https://material-kit-pro-react.devias.io/dashboard/orders/:orderId)

    > 用户在其他机械师的view mode页面有一个申请服务的按钮，点击弹出一个选择服务和时间的popup，确定发送预约，之后可以在My Appointment tab看到这个服务的状态和详情，可以筛选。

2. **I - 机械师进行服务** - 困难，记为J，参考[开始服务页面](https://material-kit-pro-react.devias.io/dashboard/blog/create)

    > 机械师在My Appointment tab看到其他人对自己申请的服务，在服务详情页面有开始服务按钮和拒绝按钮，开始或拒绝都将发送邮件。点击开始服务后跳转至服务页面。在开始服务页面有一个Section可以上传一张图片和一段注释，在下面有再添加一个Section的按钮，还有一个完成button和一个，此页面会自动及时保存。

3. **IM - 机械师查看车辆** - 简单

    > 机械师在My Appointment tab看到其他人对自己申请的服务，在服务详情页面有一个查看申请服务的用户的车辆的按钮。点击此按钮可以查看申请服务的用户的车辆信息view mode only，跳转过去就可以，需要鉴权。

4. **DJ - 完成服务并生成报告** - 困难，记为K，参考[报告参考](https://material-kit-pro-react.devias.io/dashboard/invoices/:orderId)

    > 点击完成后，给user发送邮件。在后端有一个api可以拿到所有的信息，然后前端根据这些信息生成参考链接的页面，这个页面可以下载为pdf。

5. **DK - 查看报告**，简单

    > 用户在自己的My Appointment tab服务详情，一旦服务完成，可以看到下载报告按钮，点击后跳转

6. **IM - 管理员查看各种信息** - 中等

    > 管理员在Manage Appointment可以看到所有的服务，可以按条件搜索，取消服务
