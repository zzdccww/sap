SAP-SS-ARGO 是一个专为 SAP BTP Cloud Foundry 环境设计的轻量级 Node.js 应用。

众所周知，如今SAP试用版账号搭建节点完全没速度。

作为纯小白看不懂一行代码，唯有不断尝试绕过流量监测的办法。

偶然发现Shadowsocks+ws+argo协议被针对的不明显（aes弱加密方式还是会被识别，本脚本采用chacha20-ietf-poly1305加密方式）。

优点：相比VLESS方案，能够躲过SAP流量监测（肯定是暂时的，SAP这么大的公司想封节点还不跟玩似的）。

缺点：较于之前没被流量监测的时候，代理速度较慢（这不是本脚本的错，是SAP限速了）。

web 文件：充当代理核心服务器（为 Xray / V2Ray 或定制的代理内核），负责在本地处理 Shadowsocks 和 Websocket 的加解密协议。
bot 文件：充当 cloudflared 服务程序，负责使用 Cloudflare Argo Tunnel 和公网建立隧道建立连接。

