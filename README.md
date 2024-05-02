优选订阅生成器 youxuandingyueqi
这个是一个通过 Cloudflare Workers 搭建，自动生成优选线路 VLESS 节点订阅内容生成器 [实现原理]

Pages 部署方法 视频教程
1. 部署 Cloudflare Pages：
在 Github 上先 Fork 本项目，并点上 Star !!!
在 Cloudflare Pages 控制台中选择 连接到 Git后，选中 WorkerVless2sub项目后点击 开始设置。
2. 给 Pages绑定 自定义域：
在 Pages控制台的 自定义域选项卡，下方点击 设置自定义域。
填入你的自定义次级域名，注意不要使用你的根域名，例如： 您分配到的域名是 fuck.cloudns.biz，则添加自定义域填入 sub.fuck.cloudns.biz即可；
按照 Cloudflare 的要求将返回你的域名DNS服务商，添加 该自定义域 sub的 CNAME记录 WorkerVless2sub.pages.dev 后，点击 激活域即可。
3. 修改 快速订阅入口 以及 添加内置 Vless 节点信息：
例如您的pages项目域名为：sub.fuck.cloudns.biz；

添加 TOKEN 变量，快速订阅访问入口，默认值为: auto ，获取订阅器默认节点订阅地址即 /auto ，例如 https://sub.fuck.cloudns.biz/auto
添加 HOST 变量，例如 edgetunnel-2z2.pages.dev；
添加 UUID 变量，例如 30e9c5c8-ed28-4cd9-b008-dc67277f8b02；
添加 PATH 变量，例如 /?ed=2048；
4. 添加你的专属优选线路：
添加变量 ADD/ADDNOTLS 本地静态的优选线路，若不带端口号 TLS默认端口为443 / noTLS默认端口为80，#号后为备注别名，例如：
icook.tw:2053#优选域名
cloudflare.cfgo.cc#优选官方线路
添加变量 ADDAPI/ADDNOTLSAPI 为 优选IP地址txt文件 的 URL。例如：
https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressesapi.txt
https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressesipv6api.txt
「 我不是小白！我有IP库！我知道IPtest是什么！我也有csv测速文件！ 」
Workers 部署方法 视频教程
1. 部署 Cloudflare Worker：
在 Cloudflare Worker 控制台中创建一个新的 Worker。
将 worker.js 的内容粘贴到 Worker 编辑器中。
2. 修改 快速订阅入口 以及 添加内置 Vless 节点信息：
例如您的workers项目域名为：sub.cmliussss.workers.dev；

添加 TOKEN 变量，快速订阅访问入口，默认值为: auto ，获取订阅器默认节点订阅地址即 /auto ，例如 https://sub.cmliussss.workers.dev/auto
添加 HOST 变量，例如 edgetunnel-2z2.pages.dev；
添加 UUID 变量，例如 30e9c5c8-ed28-4cd9-b008-dc67277f8b02；
添加 PATH 变量，例如 /?ed=2048；
3. 添加你的专属优选线路：
3.1 修改 addresses 参数示例

修改 addresses 参数添加本地静态的优选线路，若不带端口号默认443，不支持生成非TLS订阅，#号后为备注别名，例如：
let addresses = [
	'icook.tw:2053#优选域名',
	'cloudflare.cfgo.cc#优选官方线路',
	'185.221.160.203:443#电信优选IP',
];
该方式仅推荐添加优选域名的部分，频繁变更的优选推荐通过 addressesapi 来实现。
3.2 修改 addressesapi 参数示例

修改 addressesapi 参数，在脚本中设置 addressesapi 变量为 优选IP地址txt文件 的 URL。例如：
let addressesapi = [
	'https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressesapi.txt',
	'https://addressesapi.090227.xyz/CloudFlareYes',
];
可参考 addressesapi.txt 内容格式 自行搭建。
「 我不是小白！我有IP库！我知道IPtest是什么！我也有csv测速文件！ 」
订阅生成器 使用方法 视频教程
例如您的workers项目域名为：sub.cmliussss.workers.dev；

1. 快速订阅
添加 TOKEN 变量，快速订阅访问入口，默认值为: auto ，获取订阅器默认节点订阅地址即 /auto ，例如：
https://sub.cmliussss.workers.dev/auto
2. 自定义订阅
自定义订阅格式 https://[你的Workers域名]/sub?host=[你的Vless域名]&uuid=[你的UUID]&path=[你的ws路径]
host：您的 VLESS 伪装域名，例如 edgetunnel-2z2.pages.dev；
uuid：您的 VLESS 客户端 UUID，例如 30e9c5c8-ed28-4cd9-b008-dc67277f8b02；
path（可选）：您的 VLESS 的 WS 路径（没有可留空不填），例如 /?ed=2048。
自定义订阅地址如下：
https://sub.cmliussss.workers.dev/sub?host=edgetunnel-2z2.pages.dev&uuid=30e9c5c8-ed28-4cd9-b008-dc67277f8b02&path=/?ed=2048
注意路径必须包含 "/sub"。
3. 指定 clash、singbox 配置文件
添加 format=clash 键值，获取 clash 订阅配置，例如：

https://sub.cmliussss.workers.dev/auto?format=clash
https://sub.cmliussss.workers.dev/sub?format=clash&host=edgetunnel-2z2.pages.dev&uuid=30e9c5c8-ed28-4cd9-b008-dc67277f8b02&path=/?ed=2048
添加 format=singbox 键值，获取 singbox 订阅配置，例如：

https://sub.cmliussss.workers.dev/auto?format=singbox
https://sub.cmliussss.workers.dev/sub?format=singbox&host=edgetunnel-2z2.pages.dev&uuid=30e9c5c8-ed28-4cd9-b008-dc67277f8b02&path=/?ed=2048
变量说明
变量名	示例	备注
TOKEN	auto	快速订阅内置节点的订阅路径地址 /auto (支持多元素, 元素之间使用,作间隔)
HOST	edgetunnel-2z2.pages.dev	快速订阅内置节点的伪装域名
UUID	b7a392e2-4ef0-4496-90bc-1c37bb234904	快速订阅内置节点的UUID
PATH	/?ed=2560	快速订阅内置节点的路径信息
ADD	icook.tw:2053#官方优选域名	对应addresses字段 (支持多元素, 元素之间使用,作间隔)
ADDAPI	https://raw.github.../addressesapi.txt	对应addressesapi字段 (支持多元素, 元素之间使用,作间隔)
ADDNOTLS	icook.hk:8080#官方优选域名	对应addressesnotls字段 (支持多元素, 元素之间使用,作间隔)
ADDNOTLSAPI	https://raw.github.../addressesapi.txt	对应addressesnotlsapi字段 (支持多元素, 元素之间使用,作间隔)
ADDCSV	https://raw.github.../addressescsv.csv	对应addressescsv字段 (支持多元素, 元素之间使用,作间隔)
DLS	8	addressescsv测速结果满足速度下限
NOTLS	false	改为true, 将不做域名判断 始终返回noTLS节点
TGTOKEN	6894123456:XXXXXXXXXX0qExVsBPUhHDAbXXXXXqWXgBA	发送TG通知的机器人token
TGID	6946912345	接收TG通知的账户数字ID
SUBAPI	api.v1.mk	clash、singbox等 订阅转换后端
SUBCONFIG	https://raw.github.../ACL4SSR_Online_Full_MultiMode.ini	clash、singbox等 订阅转换配置文件
SUBNAME	WorkerVless2sub	订阅生成器名称
PS	【请勿测速】	节点名备注消息
Star 星星走起
Stargazers over time

感谢
我自己的脑洞，SAKURA-YUMI，EzSync、ACL4SSR、肥羊
