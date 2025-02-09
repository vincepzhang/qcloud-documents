## 操作场景
该任务指导您通过 Serverless Framework 提供的 API 网关组件快速创建与部署 API 网关服务/接口。

## 前提条件
已完成 Serverless Framework 的安装工作。

## 操作步骤
### 配置 API 网关服务

本地创建 `serverless.yml` 文件：

```console
touch serverless.yml
```

 在 `serverless.yml` 中进行如下配置： 

```yml
# serverless.yml

component: apigateway # (必填) 组件名称，此处为 apigateway
name: apigwDemo # (必填) 实例名称
org: orgDemo # (可选) 用于记录组织信息，默认值为您的腾讯云账户 appid
app: appDemo # (可选) 该 next.js 应用名称
stage: dev # (可选) 用于区分环境信息，默认值是 dev

inputs:
  region: ap-guangzhou
  protocols:
    - http
    - https
  serviceName: serverless
  environment: release
  endpoints:
    - path: /
      protocol: HTTP
      method: GET
      apiName: index
      function:
        functionName: myFunction
```

[查看详细配置文档>>]( https://github.com/serverless-components/tencent-apigateway/blob/master/docs/configure.md )

### 部署 API 网关服务

执行以下命令进行扫码授权部署：

```console
sls deploy
```

>?微信扫码授权部署有过期时间，如果想要持久授权，请参考 [账号配置](#account)。

### 移除已部署的服务

执行以下命令移除部署的服务：

```console
sls remove
```

<span id="account"></span>
### 账号配置（可选）

当前默认支持 CLI 扫描二维码登录，如您希望配置持久的环境变量/密钥信息，也可以本地创建 `.env` 文件：

```shell
touch .env # 腾讯云的配置信息
```

在 `.env` 文件中配置腾讯云的 SecretId 和 SecretKey 信息并保存：

```text
# .env
TENCENT_SECRET_ID=********
TENCENT_SECRET_KEY=********
```

>?
>- 如果没有腾讯云账号，请先 [注册新账号](https://cloud.tencent.com/register)。
>- 如果已有腾讯云账号，可以在 [API 密钥管理](https://console.cloud.tencent.com/cam/capi) 中获取 SecretId 和 SecretKey。
