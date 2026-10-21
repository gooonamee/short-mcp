# Short — 好縮短網址 MCP Server

[![MCP](https://img.shields.io/badge/MCP-Compatible-blue.svg)](https://modelcontextprotocol.io/)
[![Endpoint](https://img.shields.io/badge/Endpoint-https%3A%2F%2Fshort.gooo.name%2Fmcp-green.svg)](https://short.gooo.name/mcp)
[![License](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)

好縮（[https://short.gooo.name](https://short.gooo.name)，短網址跳轉專用網域為 `s.gooo.name`）的官方 MCP（Model Context Protocol）伺服器。

讓 **Cursor**、**Google Gemini**、**Muse**、**Cue**、**Claude Desktop**、**Windsurf** 等各大 AI Agent 直接幫你縮短網址、自訂短碼、開啟密碼防護、即時抓取縮圖與查詢點擊統計數據！

---

## ⚡ 遠端連線端點 (無需 API 金鑰，即裝即用)

本服務提供標準雲端託管端點，主機網址統一為 `https://short.gooo.name/`，支援 **Streamable HTTP** 與 **SSE (Server-Sent Events)**：

| 協議類型 | 端點網址 | 建議客戶端 |
|---|---|---|
| **Streamable HTTP** | `https://short.gooo.name/mcp` | Cursor, Gemini, Cue, Windsurf |
| **SSE (長連線)** | `https://short.gooo.name/mcp/sse` | Claude Desktop, Muse |
| **Direct POST** | `https://short.gooo.name/api/mcp` | Webhook, 自動化腳本 |

> 💡 **網域區隔說明**：
> - **服務主機與 API 端點**：統一使用 `https://short.gooo.name/`（如 `/mcp`、`/auth/bind`、`/dashboard`）。
> - **短網址轉址跳轉**：統一使用精簡網域 `https://s.gooo.name/`（如 `https://s.gooo.name/XXXXXX`）。

---

## 🚀 各大 AI Agent 設定指南

### 1. 🎯 Cursor
在專案根目錄的 `.cursor/mcp.json`（或個人設定的 `mcp.json`）中加入：
```json
{
  "mcpServers": {
    "short": {
      "url": "https://short.gooo.name/mcp"
    }
  }
}
```
*或者直接在 Cursor Settings ➔ Features ➔ MCP ➔ Add new MCP server，輸入 Name: `short`，Type: `http`，URL: `https://short.gooo.name/mcp`。*

---

### 2. ♊ Google Gemini (Gemini CLI / Antigravity / Google Agent)
在 Gemini MCP 設定檔（例如 `gemini.json` 或 `settings.json`）中加入：
```json
{
  "mcpServers": {
    "short": {
      "url": "https://short.gooo.name/mcp"
    }
  }
}
```
*亦可使用本 repository 提供的 [`gemini.json`](./gemini.json)。*

---

### 3. 🎨 Muse (Muse AI Agent)
Muse 支援透過 SSE 或 HTTP 連接 MCP。在 Muse 設定檔（或專案 `muse.json`）中加入：
```json
{
  "mcpServers": {
    "short": {
      "url": "https://short.gooo.name/mcp/sse"
    }
  }
}
```
*亦可使用本 repository 提供的 [`muse.json`](./muse.json)。*

---

### 4. 🤖 Cue (Cue AI)
在 Cue 設定檔（或 `cue.json`）中加入：
```json
{
  "mcpServers": {
    "short": {
      "url": "https://short.gooo.name/mcp"
    }
  }
}
```
*亦可使用本 repository 提供的 [`cue.json`](./cue.json)。*

---

### 5. ⚡ Claude Desktop
在 Claude Desktop 設定檔中加入：
* **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
* **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "short": {
      "url": "https://short.gooo.name/mcp/sse"
    }
  }
}
```
*亦可使用本 repository 提供的 [`claude_desktop_config.json`](./claude_desktop_config.json)。*

---

### 6. 💬 OpenAI / ChatGPT (Custom MCP Server / Developer Mode)
依照 OpenAI 官方自訂 MCP 連接規範：
1. 進入 ChatGPT **Settings** ➔ **Security and login** ➔ 開啟 **Developer mode**（支援 Plus / Pro / Team / Business / Enterprise 工作區）。
2. 在 Plugins / Apps 界面中點選 **+** ➔ **Add custom MCP server**。
3. 輸入伺服器端點網址：
   ```text
   https://short.gooo.name/mcp
   ```
4. 驗證方式選擇 **No authentication**（好縮支援免金鑰訪客模式，或由對話中輸入「登入好縮」完成綁定）。
5. 點擊建立，ChatGPT 將自動完成 `initialize` 握手與 `tools/list` 探索，掃描並載入 7 項好縮專屬工具！
*亦可參考本 repository 提供的 [`chatgpt.json`](./chatgpt.json)。*

---

### 7. 🏄 Windsurf / VS Code (Roo Code, Cline, Continue)
在 Windsurf MCP 配置檔（`~/.codeium/windsurf/mcp_config.json`）或 VS Code 外掛設定中加入：
```json
{
  "mcpServers": {
    "short": {
      "url": "https://short.gooo.name/mcp"
    }
  }
}
```

---

## 🛠️ 提供之 MCP 工具清單

| 工具名稱 | 說明 | 參數 |
|---|---|---|
| `shorten_url` | 縮短網址。若已登入自動歸戶；未登入為訪客模式。支援自動擷取網頁縮圖與標題 | `url` (必填), `custom_code` (可選，至少 5 碼), `password` (可選), `channel` (可選) |
| `login` | 取得 10 分鐘一次性專屬 Google 授權綁定連結 (Magic Link) | `client_name` (可選), `session_id` (可選) |
| `get_account_status` | 查詢目前 AI Agent 的登入狀態、Google Email、會員方案與已用配額 | `session_id` (可選) |
| `logout` | 解除 AI Agent 與會員帳號綁定，重置為訪客模式 | `session_id` (可選) |
| `get_url_info` | 查詢指定短網址的原始長網址、網頁標題、點擊總數、密碼防護與建立時間 | `code` (短碼或完整短網址，如 `s.gooo.name/abcde`) |
| `check_code_availability`| 檢查自訂短碼是否可用（確認未被佔用且非系統保留字） | `code` (欲檢查之代碼) |
| `get_stats_overview` | 查詢好縮即時營運指標（總短網址數、今日新增數、Top 目標網域排行） | 無 |

---

## 🔐 對話式登入與帳號綁定

免手動輸入 API 金鑰！透過現代化的**對話式 Magic Link** 輕鬆完成會員綁定：

1. **請 AI 登入**：在對話中對 AI 說：「**幫我登入好縮**」或「**查看好縮帳號狀態**」。
2. **獲取授權連結**：AI 自動呼叫 `login` 工具回傳專屬連結（10 分鐘有效）：
   > `👉 點此登入好縮會員帳號：https://short.gooo.name/auth/bind?token=xxxxxx`
3. **完成 Google 登入**：點擊開啟瀏覽器，完成 Google 登入或確認綁定。
4. **自動歸戶生效**：往後該 AI Agent 建立的所有短網址皆會自動歸屬於您的會員帳號，可在官網 Dashboard 查看成效！

---

## 💬 使用範例

* **基本縮短**：
  > 「幫我把這個網址縮短：`https://github.com/gin-gonic/gin`」
* **自訂短碼與密碼保護**：
  > 「幫我縮短這篇教學 `https://example.com/guide`，自訂短碼 `my-guide`，並加上開啟密碼 `pass888`」
  > （產出的短網址為 `https://s.gooo.name/my-guide`）
* **查詢成效與統計**：
  > 「查一下 `https://s.gooo.name/my-guide` 的點擊次數與詳細資料」
* **帳號管理**：
  > 「查詢我目前好縮會員帳號狀態與配額」
  > 「登出好縮帳號」

---

## 📊 會員方案與配額

| 方案 | 專屬短網址配額 | 自訂短碼 | 密碼防護 | 數據儀表板 |
|---|---|:---:|:---:|:---:|
| **訪客模式** | 1 組（10 分鐘） | ❌ | ❌ | ❌ |
| **Free 會員** | 20 組（刪除自動釋放） | ✅ | ✅ | ✅ |
| **Pro 會員** | 99,999 組 | ✅ | ✅ | ✅ |

*登入後即可免費享有 20 組活躍配額，若需更多短網址配額，可於官網升級 Pro 授權。*

---

## 🔒 隱私與安全性

* **安全性檢測**：所有長網址均經過 Google Safe Browsing 與惡意網址黑名單檢驗，防範釣魚詐騙。
* **縮圖擷取**：建立短網址時系統會在背景安全擷取 OpenGraph 標題與預覽縮圖。
* **隱私政策**：Google 登入僅用於識別會員帳號（Email 與會員權益），不收集多餘權限。

---

## 📬 聯絡與支援

* 官網與服務主機：[https://short.gooo.name](https://short.gooo.name)
* 短網址跳轉專用網域：[https://s.gooo.name](https://s.gooo.name)
* GitHub Issues：[gooonamee/short-mcp/issues](https://github.com/gooonamee/short-mcp/issues)
* 聯繫 Email：contact.goooname@gmail.com
