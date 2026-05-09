你现在 iPhone 已经装好了，电脑端按下面做就行。注意：现在有两个名字很像的项目：

* **Happy**：命令一般是 `happy`，安装：`npm install -g happy`，然后用 `happy codex` 启动 Codex。官方 README 就是这么写的。([GitHub][1])
* **Happier**：命令一般是 `happier`，Windows 安装：`iwr https://happier.dev/install.ps1 -useb | iex`，然后用 `happier codex`。它是 Happy 的分支/衍生项目，功能更宽，但 README 也明确说还在 alpha preview，可能有 bug。([GitHub][2])

你如果下载的 App 叫 **Happy: Codex & Claude Code App**，优先用下面的 **Happy** 步骤。

---

## 1. 先确认电脑上 Codex 本身可用

在 PowerShell 里运行：

```powershell
codex --version
```

再进入你的项目目录测试：

```powershell
cd "你的项目路径"
codex
```

如果直接 `codex` 本身就不能用，先不要管 Happy，先把 Codex CLI 修好。

---

## 2. 安装 Happy CLI

PowerShell 里运行：

```powershell
npm install -g happy
```

装完检查：

```powershell
happy --version
```

如果提示找不到 `npm`，说明 Node.js 没装好，或者 PATH 没生效。你之前折腾过 Node/OpenClaw，所以大概率这里能直接过。

---

## 3. 配对 iPhone

在电脑 PowerShell 里运行：

```powershell
happy
```

第一次运行通常会让你登录/配对，可能显示二维码或连接提示。
然后在 iPhone 的 Happy App 里找类似：

```text
Add device
Pair device
Scan QR code
Connect computer
```

扫码或按 App 提示完成配对。

官方 App Store 说明里也写了大致流程：电脑安装 happy-coder / happy CLI，扫描二维码配对，然后用 `happy` 代替 `codex` 或 `claude` 启动加密会话。([App Store][3])

---

## 4. 用 Happy 启动 Codex

以后不要直接在项目目录运行：

```powershell
codex
```

而是运行：

```powershell
cd "你的项目路径"
happy codex
```

这一步的含义是：**Codex 仍然跑在你的电脑上，读写的也是本机项目文件；Happy 只是把这个会话同步/映射到手机端。**

官方 README 也明确写了：用 `happy codex` 代替 `codex`；当你从手机控制时，它会把 session 切换到 remote mode；想切回电脑时，在键盘按任意键即可。([GitHub][1])

---

## 5. 手机端怎么用

电脑上已经在项目目录跑了：

```powershell
happy codex
```

之后，打开 iPhone Happy App，应该能看到这台电脑或当前 session。

你可以在手机上：

```text
查看 Codex 输出
继续输入任务
批准权限请求
看任务是否完成
收到推送通知
```

Happy 的 README 里提到它支持手机访问 Codex/Claude Code、权限请求或错误时推送通知、设备间一键切换、端到端加密。([GitHub][1])

---

## 6. 推荐你第一次这样测试

不要一上来让它改大项目。先新建一个测试目录：

```powershell
mkdir C:\tmp\happy-codex-test
cd C:\tmp\happy-codex-test
"hello" | Out-File .\README.md -Encoding utf8
happy codex
```

然后在 Codex/Happy 里输入一个很小的任务：

```text
Read README.md and append one sentence saying this is a Happy Codex test.
```

如果手机端能看到输出，并且电脑目录里的 `README.md` 被改了，说明链路通了。

---

## 7. 常见问题

### A. `happy codex` 没反应或卡住

先分别测试：

```powershell
codex
```

和：

```powershell
happy --version
```

如果 `codex` 正常、`happy codex` 卡住，可能是 Happy 对当前 Codex 版本/权限交互有兼容问题。GitHub issues 里确实有人反馈过 iPhone 连接后 `happy codex` 挂起，以及 Codex 权限批准后卡住的问题。([GitHub][4])

这时可以试：

```powershell
npm update -g happy
```

然后重新开一个 PowerShell，再运行：

```powershell
happy codex
```

### B. 手机看不到电脑

检查三点：

1. 电脑端 `happy` 是否已经登录/配对。
2. 电脑端是否正在运行 `happy codex`。
3. Windows 防火墙/代理是否拦截了 Happy 的连接。

Happy 不是简单局域网工具，它通过加密同步/桥接来连接设备；README 写的是端到端加密，并且代码不会以明文离开设备。([GitHub][1])

### C. 不知道自己装的是 Happy 还是 Happier

看 App 名字：

```text
Happy: Codex & Claude Code App
```

电脑用：

```powershell
npm install -g happy
happy codex
```

如果 App 名字是：

```text
Happier: Claude Codex OpenCode
```

电脑用：

```powershell
iwr https://happier.dev/install.ps1 -useb | iex
happier auth login
happier codex
```

Happier 的 README 明确给了 Windows 安装命令和 `happier codex` 用法。([GitHub][2])

---

## 最简流程

你可以直接按这个跑：

```powershell
codex --version
npm install -g happy
happy --version
cd "你的项目路径"
happy
happy codex
```

然后打开 iPhone App，配对电脑，进入当前 session。

[1]: https://github.com/slopus/happy "GitHub - slopus/happy: Mobile and Web client for Codex and Claude Code, with realtime voice, encryption and fully featured · GitHub"
[2]: https://github.com/happier-dev/happier "GitHub - happier-dev/happier: Web, Desktop & Mobile client for Codex, Claude Code, OpenCode, Kimi, Augment Code, Qwen, fully end-to-end encrypted · GitHub"
[3]: https://apps.apple.com/us/app/happy-codex-claude-code-app/id6748571505?utm_source=chatgpt.com "Happy: Codex & Claude Code App - App Store - Apple"
[4]: https://github.com/slopus/happy/issues/987?utm_source=chatgpt.com "happy codex mobile remote mode hangs even on a ..."
s