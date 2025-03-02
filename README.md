# AI-Chat
将此项目部署在cloudflare pages项目上，即可实现部署在线AI聊天网站。

## 说明

本教程由秋名山撰写，代码由 我和DeepSeek 共同编写。转载请注明出处，谢谢！

## 部署准备

一个域名
cloudflare账号/服务器/虚拟主机/serv00（四选一即可）
谷歌账号（用于申请Gemini API、注册DeepSeek账号）

本项目GitHub地址：
https://github.com/qmsdh/AI-Chat/

## 申请Gemini API Key

说明：Gemini API是免费的，好像是有额度限制，应该是每小时限制多少次，我分享给好多人用，一直没有限制，不必担心API用完的情况

1. 准备一个谷歌账号，已经有了请跳过。

2. 建议使用美国节点访问。（亲测日本无法正常获取API Key，可能对IP所在地区有限制）

3. 打开Google AI Studio 申请api的网址：https://makersuite.google.com/app/apikey。当然你也可以打开Gemini的首页 http://ai.google.dev ，并点击 Get API key in Google AI Studio 按钮。你需要先同意使用条款才能继续使用。

4. 点击左边菜单里的 Get API key，然后在右边点击 Create API key in new project。

![8384FA5D-DE10-4415-A9EC-DC7ACF75E27A.png](https://img.qmsdh.com/api/cfile/AgACAgUAAyEGAASMeqieAAOYZ8O_o7eLwr6x1ttHn8taXAvoP_sAAprGMRthCSFWl3TFhnTd36MBAAMCAAN3AAM2BA)

## 搭建反代Gemini API

说明：这步操作的原因是国内无法直接访问Gemini的API，所以搭建这个反代可以在国内直连AI，如果不需要请跳过这步。

1. [点击下载](https://github.com/qmsdh/AI-Chat/releases)反代API的源码```_worker.js```

2. 打开 Cloudflare 的 pages & workers

3. 点击创建，选择helloworld，点击部署

![Screenshot_20250302_130834.jpg](https://img.877774.xyz/api/cfile/AgACAgUAAyEGAASMeqieAAOZZ8Pn8Uh_FX0XO2aGIhrINKNoV2gAAt7GMRthCSFWa-GvznUJIuABAAMCAAN3AAM2BA)

4. 点击编辑代码，将原有的代码```全部删除```，将```_worker.js```里面的文件```全部代码```复制到里面。

5. 如果有域名，部署完后点击继续处理项目，自定义域，设置自定义域添加自己的域名（可以不用转入cloudflare），这个域名用于API Key，并非你的；如果没有域名可以用cloudflare给的免费域名（*.workers.dev），这个域名有可能被墙。

注：如果用CF分配的项目域名有可能国内无法正常使用

## 申请 DeepSeek API

说明：
1. 如果需要Google登录请将梯子修改为```全局模式```。
2. DeepSeek API 必须```付费```才能对接使用，如果介意请只用Gemini。[DeepSeek官方文档](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/)里面有API价格，本教程只调用V3和R1。

1. 访问[DeepSeek官网](https://deepseek.com/)，并点击```开放API```。

2. 登陆完后请先充值（支持微信/支付宝），然后点击```API Keys```。```创建```后复制保存好你的API Key。

![Screenshot_20250302_131857.jpg](https://img.877774.xyz/api/cfile/AgACAgUAAyEGAASMeqieAAOaZ8PqaXVXZnu5Ur5j1EfEiUMAAasjAALoxjEbYQkhVr35bAowP02FAQADAgADdwADNgQ)

## 修改源码

1. 从[Release](https://github.com/qmsdh/AI-Chat/releases)中下载```AIChat.zip```源码。

2. 下载完后解压，按照需要修改代码

#### 修改DeepSeek API

打开```/d```文件夹，修改index.html，将```第156行```的```你的API Key```修改为DeepSeek API Key。

#### 修改Gemini API

打开```/g```文件夹，修改script.js，将```第2行```的```你的API Key```修改为Gemini API Key；将```第3行```的```https://generativelanguage.googleapis.com/```修改为```https://你第一个部署的项目的域名/```

#### 修改广告以及网站上的内容

打开```根目录```的index.html。

```第151-196行```请按需修改。如果没设置DeepSeek请删除```第176-172行```的代码；如果没设置Gemini请删除```第183-190行```的代码。

如果需要设置广告，请修改```第253-277行```代码；如果不需要广告，请直接删除```第253-277行```代码。

3. 压缩修改完的所有代码

## 部署AI聊天网站

1. 首先，打开workers & pages，点击创建

![2](https://img.qmsdh.com/api/cfile/AgACAgUAAyEGAASMeqieAAM3ZzmmFz6Z-EgJevwYSu0HqbZ9xsgAAnbAMRv3KNFVR2EdxXGQ7XMBAAMCAAN4AAM2BA)

2. 选择上传资产

![3](https://img.qmsdh.com/api/cfile/AgACAgUAAyEGAASMeqieAAM4ZzmmGaJTGjFvC0veIVS1l35jwh8AAnfAMRv3KNFVPTuzZWjKabgBAAMCAAN5AAM2BA)

3. 输入项目名称，并上传你刚才修改好的源码

![4](https://img.qmsdh.com/api/cfile/AgACAgUAAyEGAASMeqieAAM5ZzmmG046iuvIoNaTRq_6rFDUu48AAnjAMRv3KNFVVcenUHHN1N8BAAMCAAN4AAM2BA)

4. 如果有域名，部署完后点击继续处理项目，自定义域，设置自定义域添加自己的域名（可以不用转入cloudflare）；如果没有域名可以用cloudflare给的免费域名（*.pages.dev），国内可能会墙。

注：这个域名就是你AI聊天网站的域名了。。

## 搭建完毕

接下来，访问你的```AI聊天网站的域名```，就可以尽情使用AI聊天了。

注：这个源码由于没有后端（后端的太麻烦了，不适合做成教程），并未对API进行加密，很有可能被人```盗走API```，自己搭建了给```现实生活中的朋友以及小白们玩玩就行了```，如果要公开发布在网上广泛使用，请一定要慎重考虑，只有Gemini没啥大事儿（毕竟不花钱），DeepSeek可能会被官方删掉泄露的API。
