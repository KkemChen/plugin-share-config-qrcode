# plugin-share-config-qrcode

GUI.for.Clash 插件 —— 通过 QR 码将完整 Mihomo 配置分享到手机端 CMFA (Clash Meta For Android)。

## 功能

- 选择一个 Profile，自动生成适配手机端的完整 Mihomo 配置
- 局域网内启动临时 HTTP 服务，生成 QR 码供手机扫码导入
- 自动处理以下适配：
  - **TUN 模式**：启用 TUN，设置 `stack: Mixed`、`auto-route`、`dns-hijack`
  - **proxy-providers 内联**：消除所有 proxy-providers，节点全部内联，proxy-groups 的 `use` 展开为 `proxies`，避免重名冲突
  - **rule-providers 转换**：本地 `file` 类型的 rule-provider 转为 `http` 类型
  - **GLOBAL 组补全**：将所有非 hidden 自定义代理组加入 GLOBAL，确保 CMFA 能显示
  - **DNS 引导**：设置 `proxy-server-nameserver` 和 `default-nameserver`，避免 TUN 模式下 DNS 循环依赖
  - **PC 配置清理**：移除 `secret`，重置 `external-controller`

## 安装

### 方式一：通过插件中心安装

如果本插件已上架 [Plugin-Hub](https://github.com/GUI-for-Cores/Plugin-Hub)，可直接在 GUI.for.Clash 的插件中心搜索安装。

### 方式二：通过自定义仓库链接安装

1. 在 GUI.for.Clash 中，进入 **插件** 页面
2. 点击右上角导入，选择 **从 URL 导入**
3. 输入本仓库的插件清单地址：
   ```
   https://raw.githubusercontent.com/KkemChen/plugin-share-config-qrcode/main/plugins/gfc.json
   ```
4. 选择本插件进行安装

> 将 `KkemChen` 替换为你的 GitHub 用户名。

### 方式三：手动安装

1. 下载 `plugins/GFC/plugin-share-config-qrcode.js`
2. 放入 GUI.for.Clash 的 `data/plugins/` 目录
3. 在 GUI.for.Clash 中手动添加插件配置

## 使用

1. 在 GUI.for.Clash 的插件页面，点击本插件的 **运行** 按钮
2. 如有多个 Profile，选择要分享的配置
3. 弹窗显示 QR 码和链接地址
4. 手机端 CMFA 扫码或手动输入链接导入配置
5. 关闭弹窗后临时 HTTP 服务自动停止

### 注意事项

- 电脑和手机需在同一局域网
- 需关闭电脑防火墙或放行配置中的端口（默认 18963）
- 如有多个网卡 IP，尝试不同的 QR 码

## 配置项

| 配置 | 说明 | 默认值 |
|------|------|--------|
| HTTP 服务端口 | 临时 HTTP 服务监听端口 | 18963 |

## 依赖

- [qrcode.js](https://github.com/soldair/node-qrcode) — QR 码生成库，首次运行时自动下载

## 开发

### 项目结构

```
plugins/
├── GFC/
│   └── plugin-share-config-qrcode.js   # 插件主文件
└── gfc.json                             # 插件清单（Plugin-Hub 格式）
```

### 调试

取消插件代码中 `DEBUG` 注释行，运行后会在 `data/third/share-config-qrcode/debug-config.yaml` 输出生成的完整配置，便于排查问题。

## 许可

MIT
