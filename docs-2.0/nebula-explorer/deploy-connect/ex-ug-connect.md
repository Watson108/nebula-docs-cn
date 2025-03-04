# 连接数据库

在成功启动 Explorer 后，用户需要配置连接 NebulaGraph。默认情况下可以直接连接数据库。为保证数据安全，还支持 OAuth2.0 认证，认证通过后才可以连接数据库。

## 前提条件

在连接 NebulaGraph 数据库前，用户需要确认以下信息：

- 已经安装部署了 Explorer。详细信息，参见[部署 Explorer](../deploy-connect/ex-ug-deploy.md)。

- NebulaGraph 的 Graph 服务本机 IP 地址以及服务所用端口。默认端口为 `9669`。

- NebulaGraph 数据库登录账号信息，包括用户名和密码。

## OAuth2.0 认证设置

!!! caution

    该功能仍处于测试中，后续会继续进行调整优化。

!!! note

    如果想直接连接数据库，请参见后文**连接数据库**部分。

如果需要开启 OAuth2.0 认证，需要在 Explorer 安装目录内修改配置文件。路径为`config/app-config.yaml`。

OAuth 部分的配置说明如下。

|参数|示例|说明|
|:--|:--|:--|
|`Enable`|`false`|是否开启 OAuth2.0 认证。|
|`ClientID` | `4953xxx-mmnoge13xx.apps.googleusercontent.com`| 应用的 ClientId。  |
|`ClientSecret` | `GOCxxx-xaytomFexxx` | 应用的 ClientSecret。 |
|`RedirectURL` | `http://dashboard.vesoft-inc.com/login` |重定向到 Dashboard 的 URL。   |
|`AuthURL` | `https://accounts.google.com/o/oauth2/auth` | 认证 URL。  |
|`TokenURL` | `https://oauth2.googleapis.com/token`| 获取 access_token 的 URL。 |
|`UserInfoURL` | `https://www.googleapis.com/oauth2/v1/userinfo`| 获取用户信息的 URL。 |
|`UsernameKey` | `email`| 用户名字段。 |
|`Organization` |  `vesoft company`       |  组织名称。             |
|`TokenName`|`oauth_token`|Cookie 里的 Token 名称。|
|`Scope`| `email`| OAuth 的权限范围。权限范围需要是厂商 OAuth2.0 平台配置的 scope 的子集，否则请求会失败。请求的 scope 需要能获取到`UsernameKey`的值。|
|`AvatarKey`|`picture`|用户信息里的 Avatar Key。|

配置完成后重启 Explorer 服务，登录页面会先展示 OAuth 认证页面，通过后才能继续连接数据库。

## 连接数据库

按以下步骤连接 NebulaGraph 数据库：

1. 在 Explorer 的**配置数据库**页面上，输入以下信息：

   - **Host**：填写 NebulaGraph 的 Graph 服务本机 IP 地址及端口。格式为 `ip:port`。如果端口未修改，则使用默认端口 `9669`。

    !!! Note

        即使 NebulaGraph 数据库与 Explorer 部署在同一台机器上，用户也必须在 **Host** 字段填写这台机器的本机 IP 地址，而不是 `127.0.0.1` 或者 `localhost`。

   - **用户名**和**密码**：根据 NebulaGraph 的[身份验证](../../7.data-security/1.authentication/1.authentication.md)设置填写登录账号和密码。
     - 如果未启用身份验证，可以填写默认用户名 `root` 和任意密码。
     - 如果已启用身份验证，但是未创建账号信息，用户只能以 GOD 角色登录，必须填写 `root` 及对应的密码 `nebula`。
     - 如果已启用身份验证，同时又创建了不同的用户并分配了角色，不同角色的用户使用自己的账号和密码登录。

2. 完成设置后，点击**登录**按钮。

  !!! note

        一次连接会话持续 30 分钟。如果超过 30 分钟没有操作，会话即断开，用户需要重新登录数据库。

首次登录会显示欢迎页，根据使用流程展示相关功能，并且支持自动下载并导入测试数据集。

想要再次访问欢迎页，在 ![help](https://docs-cdn.nebula-graph.com.cn/figures/navbar-help.png) 下选择**新手引导**。

## 断开连接

在页面右上角，选择![icon](https://docs-cdn.nebula-graph.com.cn/figures/image-icon10.png)图标 > 清空连接。

如果浏览器上显示**配置数据库**页面，表示 Explorer 已经成功断开了与 NebulaGraph 数据库的连接。
