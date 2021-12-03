此文章适合相应域名服务商，借助api通过acme实现自动添加解析记录

# 使用 acme.sh 免费申请 Let’s Encrypt 泛域名 SSL 证书

[技术](https://munue.com/jishu)

# 使用 acme.sh 免费申请 Let’s Encrypt 泛域名 SSL 证书

[2021-07-18](https://munue.com/68.html)[2](javascript:;)[802](https://munue.com/68.html)[2](https://munue.com/68.html#comments)

[![img](https://munue.com/wp-content/uploads/2021/07/1626536489-letsencryptssl.png)](https://munue.com/wp-content/uploads/2021/07/1626536489-letsencryptssl.png)

现在绝大多数网站都部署了全站 https 加密访问，而 Let’s Encrypt 这个项目通过自动化申请 SSL 证书，使配置和维护 https 变得更加简单，我的腾讯云服务器就使用 acme.sh 基于 dns-api 协议生成证书，便捷实现 Let’s Encrypt 泛域名 SSL 证书的申请，安装及自动续期。

## 安装 acme.sh

> curl https://get.acme.sh | sh

acme.sh 实现了 acme 协议,可以帮助你快速申请SSL证书，自动更新证书等操作，极大简化操作步骤。

## 设置默认证书

> acme.sh --set-default-ca --server letsencrypt

现在 acme.sh 已经支持 ZeroSSL、BuyPass、Let’s Encrypt 等多种不同证书。若要更换为ZeroSSL，则改为 --server zerossl

## 配置DNS API

> export Ali_Key="<key>"
> export Ali_Secret="<secret>"
>
> export DP_Id="<id>"
> export DP_Key="<key>"

acme.sh 目前支持 cloudflare，aliyun，dnspod， cloudxns，godaddy 等数十种解析商的自动集成。

以 DNSPod 为例，你需要先登录到 dnspod 账号（https://console.dnspod.cn/account/token/apikey），生成你的 api id 和 api key，都是免费的。

acme.sh 支持多个DNS服务商，这里给出的 api id 和 api key 会被自动记录下来，将来你在使用 dnspod api 的时候，就不需要再次指定了。

## 申请证书

> acme.sh --issue --dns dns_dp -d domain.com -d *.domain.com --server letsencrypt

这里要注意的两点，你用的是 dnspod 的，则红色字符为 dns_dp，用的是 aliyun ，则为 dns_ali ，请注意修改服务商名。domain.com 则修改为你自己的域名，*.domain.com 则是支持泛域名。

[![img](https://munue.com/wp-content/uploads/2021/07/1626533771-20210717121517.png)](https://munue.com/wp-content/uploads/2021/07/1626533771-20210717121517.png)

等待程序自动申请完毕，看到如上图所示，就说明申请成功了。证书文件自动存放在 /root/.acme.sh/域名文件夹中。请不要直接使用此目录下的文件， 这里面的文件都是内部使用，而且目录结构可能会变化。

正确的使用方法是使用 --installcert 命令，将证书文件 Copy 到相应的位置，再按需下载到本地保存。

## 安装证书

> acme.sh --installcert -d domain.com -d *.domain.com \
> --key-file /home/wwwroot/ladingwu.xin/ssl/domain.com.key \
> --fullchain-file /home/wwwroot/ladingwu.xin/ssl/domain.com.cer \
> --reloadcmd "service nginx reload" \
> --reloadcmd "chown -R www:www /home/wwwroot/ladingwu.xin/ssl/"

上述命令将 domain.com SSL证书，导出到了域名文件夹/ssl 目录下，方便使用 FTP 软件将 .key 和 .cer 文件下载到本地。

## 自动续期

> acme.sh --install-cronjob

Let’s Encrypt 免费版 SSL 证书有效期只有90天，到期后会自动更新，你无需任何操作。但如果你是用于像上海云盾一样的CDN应用商，则每过三个月就要手动重新下载一次，进行证书文件更换。

## 更新 acme.sh

目前由于 acme 协议和 Let’s Encrypt CA 都在频繁的更新, 因此 acme.sh 也经常更新以保持同步.

升级 acme.sh 到最新版 ：

> acme.sh --upgrade

如果你不想手动升级， 可以开启自动升级，之后 acme.sh 就会自动保持更新了：

> acme.sh --upgrade --auto-upgrade

查看 acme.sh 当前版本：

> acme.sh -v

## 申请 ZeroSSL 泛域名证书

ZeroSSL 在2016年就已经推出，和 Let’s Encrypt 一样，证书有效期只有90天，支持泛域名SSL证书。和 Let’s Encrypt 不同的是，ZeroSSL API 没有速率限制，不存在同一IP多次申请SSL证书被限制的问题，ZeroSSL 还提供了WEB界面可在后台管理SSL证书，相比 Let’s Encrypt 功能更加丰富。

- ZeroSSL官网：[https://zerossl.com/](https://zerossl.com/?fpr=xiaoz)

申请证书之前，需要先注册ZeroSSL账户，并用下面的命令绑定关联账户（myemail@example.com 改成你自己的ZeroSSL 邮箱，不要乱填）：

> acme.sh --register-account -m myemail@example.com --server zerossl

此步骤在配置DNS API之后， 然后按上面的申请证书流程进行操作。

acme.sh 默认 server 使用 Let’s Encrypt，将在2021/08/01发布v3版本，默认 server 将更改为 ZeroSSL 。