接口名称：traceint 微校授权回调

Request URL：
https://wechat.v2.traceint.com/index.php/urlNew/weixiao.html?...

请求方法：
GET

作用：
接收微校 OAuth 授权结果，给 traceint 域名下发登录态 cookie，然后跳转到 web.traceint.com 首页。

Status Code：
302

Response Headers：

Location：
https://web.traceint.com/web/index.html#/pages/index/index?r=1783078604

Set-Cookie：
Authorization=******; expires=Fri, 03-Jul-2026 13:36:53 GMT; path=/; domain=traceint.com; httponly

Set-Cookie：
SERVERID=******; Path=/

关键结论：
1. traceint 登录态在这一步生成。
2. 主登录 cookie 名可能是 Authorization。
3. 后续 GraphQL 请求会依赖这个 cookie。
4. SERVERID 更像负载均衡标记，不是主要身份凭证。

登录链路：
登录/OAuth 链路：
open.wecard.qq.com 授权
  ↓
weixiao.qq.com 微校中转
  ↓
wechat.v2.traceint.com/index.php/urlNew/weixiao.html
  ↓
Set-Cookie: Authorization=******
  ↓
web.traceint.com/web/index.html
  ↓
GraphQL index / list / libLayout / reserueSeat