# Mock 神器 Apifox

大家好呀，我是一名苦逼的前端开发工程师，为啥苦逼呢，这不，项目下周就要上线了，但是后端还没给我接口，没有接口我就无法调试，工作停滞不前，我也只能坐着干着急。

我报告给了我的老板狐哥: **老板，这后端不靠谱啊，都快上线了，接口还没出来**。

狐哥回道，**别着急呀，这不有 Mock 吗**？

**Mock，什么是 Mock 啊？**我一脸狐疑，问向狐哥。

狐哥慢条斯理说，就是**前端自己启动一个 HTTP 服务，模拟后端接口的数据，这样就无需等待后端接口开发完成了，不会因为后端开发延误而阻塞你的工作进程了**。

嗯，真是个不错的注意，我仿佛发现了新大陆！以后再也不用受后端拖累了，心里暗暗开心，但转念一想不对啊，时间不够啊！

我又沮丧了下来，转头向狐哥说道: **Mock 好是好，但是时间不够了啊，我重新启动一个 Mock HTTP Server，也要花不少时间呀**。

狐哥见我开了窍，又忙不迭地说: **咱们团队不是用的 Apifox 管理 API 吗，只需要点下按钮，就可以自动 Mock！**

一键 Mock 数据，这么简单，那应该怎么使用 Apifox 自动 Mock 呢？

狐哥接下来，缓缓道来。

## 使用 Apifox 智能 Mock

Apifox，API 文档、API 调试、API Mock、API 自动化测试集成于一体的强大工具，可以在 [Apifox官网](https://www.apifox.cn/?utm_source=shanyue-question) 直接下载，在 Windows、Linux、Mac 下都可以使用。

![](https://files.mdnice.com/user/5840/2dea171d-ab32-42c2-89a9-ddac0993a046.png)

下载成功后，可打开其中的**示例项目**，是一个关于宠物店的项目。打开宠物店的项目，可以在每个标签页看到四个标签: 文档、修改文档、运行、高级 Mock。

![](https://files.mdnice.com/user/5840/f9276d5a-59e4-4afb-ae44-3c33c80ca565.png)

我们先看下这个**查询宠物详情**的接口，其请求接口为 `/pet/{petId}`，而响应数据为 `code` 与 `data`，`data` 是一个 `Pet` 的一个自定义数据类型。

![](https://files.mdnice.com/user/5840/7c0c7ba9-37cd-4052-b98a-bbed63258993.png)

在数据模型选项卡中，可以看到 `Pet` 这个自定义数据类型，其中有两个字段为 `id`、`name` 和 `photoUrls`。

![](https://files.mdnice.com/user/5840/ff4c39ab-c0e7-4770-93c1-e66cd383971e.png)

在我们的本地是肯定没有宠物店的这个项目和接口的，那我们现在就可以使用一键 Mock 服务，请求 Mock 出来的宠物店数据，非常方便！

切换环境为**Mock服务**，此时地址栏前缀为 `http://127.0.0.1:4523/mock/533840`，点击运行按钮发送请求，见证奇迹的时刻到了，数据正确返回！

![](https://files.mdnice.com/user/5840/68e12984-e582-44e0-8b8b-e48a466bf412.png)

在项目中进行 Mock 时，使用 `http://127.0.0.1:4523/mock/533840` 代替后端的 API 前缀即可，特别好用是不是！

但这仅仅是 Apifox 强大的只能 Mock 下的冰山一角！

**假设，我们有一个用户接口，它有一个字段 email 期待返回邮箱格式的数据，一个字段 phone 期待返回手机格式的数据，一个字段 avatar 期待返回一个头像，而这在 Apifox 下都可以零配置完成！**

这就是，Apifox 强大的智能 Mock 规则: **你需要做的仅仅是定义 API 接口文档中的响应数据，接下来一键 Mock 服务，全部只能工作都交给 Apifox 的智能 Mock 来完成**。

在 Apifox 内部，当接口响应的数据字段未配置 mock 规则时，系统会自动使用智能 Mock 规则来生成数据，以实现使用时零配置即可 mock 出非常人性化的数据。根据项目设置、功能设置、智能 Mock 设置即可打开默认配置。

![](https://files.mdnice.com/user/5840/7a2aa8ec-5b09-4dc1-a38b-9b1b0964ca76.png)


## 使用 Apifox 自定义 Mock

在 Apifox 自动 Mock 非常方便，但我们需要自定义 Mock 功能，在上个接口中，宠物有一个字段是 `name`，表示宠物的名字，我们可不可以将宠物的名字仅仅定位为两个字符。

我们在 Apifox 数据模型设置中找到该宠物的数据模型，并配置其 `name` 字段。

![](https://files.mdnice.com/user/5840/adbe46af-c005-4d85-b0fb-c4eed92ade8e.png)

`@cword(3)` 是[Apifox 的 Mock 语法](https://www.apifox.cn/help/app/mock/mock-rules/)，完全兼容 Mock.js（数据占位符方式），并扩展了一些 Mock.js 没有的语法（如国内手机号 @phone）。

![](https://files.mdnice.com/user/5840/69d8e813-62c2-4f11-80be-431b77216584.png)

如现有 Mock 语法无法满足需求，建议使用 正则表达式 `@regexp` 来实现灵活的定制。正则表达式基本能满足各种特殊场景的需求。

![](https://files.mdnice.com/user/5840/90098d40-a7f8-4a08-8872-f3238bd35cd8.png)

而我们将宠物的名字限制为两个字符，即可使用: `@cword(2)` 替代。

## Apifox 的高级 Mock

Apifox 的智能 Mock 与自定义 Mock 已经足够强大，但是他的功能远不止于此。我们尽管可以使用自定义 Mock 对数据进行每个字段更为精细的模拟，但远远无法满足复杂业务的多样性。

以以上**查询宠物详情**的接口为例，难免有记录不存在的示例，此时接口响应为完全不同的数据类型。此时，我们可以使用 Apifox 的高级 Mock 用以模拟数据。

![](https://files.mdnice.com/user/5840/e694b02c-ef90-4aa4-9d0e-1ef89d9d9caa.png)

当我们查询宠物的 ID 为3时，返回不存在数据的相应格式，同时设置状态码为 404。

![](https://files.mdnice.com/user/5840/f8bc471d-ec66-4ba5-adf6-9844036a5b83.png)

为了满足业务的多样性，我们还可以使用基于模板的高级 Mock 功能与 Apifox 的 Mock 语法相结合。这里使用了 Javascript 的 [nunjucks](https://github.com/mozilla/nunjucks) 模板语法，可以生成你想生成的任意数据。

![](https://files.mdnice.com/user/5840/d3759afb-8586-4c42-82f0-f7f5be4d44dc.png)


## 小结

今天关于 Apifox 强大的功能就介绍到了这里，你是不蠢蠢欲动也想下载尝试一下呢？

客户端下载地址：https://www.apifox.cn/
API Hub网页版地址：https://www.apifox.cn/apihub/

大家可前往下载体验一波~

如果有什么疑问，也可以进Apifox官方交流群和官方工作人员讨论交流。

![](https://mmbiz.qpic.cn/mmbiz_png/nRXib819UwN10LkP959TE1FKNEC1nw0wBdw2ZWQLr2M1Lq3WHP4VzMMvzaJGvpCIXp9qEtPbDqhttFC9HgwHE0g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
