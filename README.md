# Short — 好縮短網址 MCP

好縮（https://short.gooo.name，短網址網域 s.gooo.name）的官方 MCP Server。
讓 AI 助手直接幫你縮網址、自訂短碼、加密碼保護、查看點擊統計。
用 Google 登入綁定會員帳號後，建立的短網址會自動歸到你的帳號。

## 安裝

MCP 端點：`https://s.gooo.name/mcp`（Streamable HTTP，不需要 API 金鑰）

從 Cursor Marketplace 安裝 Short，或手動在 `mcp.json` 加入：

    {
      "mcpServers": {
        "short": { "url": "https://s.gooo.name/mcp" }
      }
    }

## 工具

| 工具 | 用途 |
|---|---|
| `shorten_url` | 縮短網址，可選自訂短碼（至少 5 碼）、密碼保護、來源渠道標籤 |
| `check_code_availability` | 檢查自訂短碼是否可用 |
| `get_url_info` | 查詢短網址的原始網址、標題、點擊數、建立時間 |
| `get_stats_overview` | 服務整體統計與熱門網域排行 |
| `login` | 取得會員登入連結（10 分鐘有效），用 Google 登入綁定 |
| `logout` | 解除綁定，回到訪客模式 |
| `get_account_status` | 查詢登入帳號、方案與已用配額 |

## 使用範例

- 「幫我把 https://example.com/very/long/link 縮短」
- 「用自訂短碼 my-doc 縮這個網址，並加上密碼」
- 「查一下 s.gooo.name/XXXXXX 被點了幾次」

## 登入與方案

本外掛免費使用。用 Gmail（Google 帳號）登入即可開始使用，需要更多短網址配額時，可升級取得 PRO 授權。

1. 請 AI 執行 `login`，取得授權連結（10 分鐘有效）。
2. 在瀏覽器用 Google 登入完成綁定。
3. 之後建立的短網址都會歸到你的會員帳號，可在官網 Dashboard 查看成效。

| 方案 | 短網址配額 |
|---|---|
| Free | 20 組 |
| Pro | 99,999 組 |

## 隱私

建立短網址時，服務會抓取目標網頁的標題與縮圖。
登入時只用 Google 帳號的 Email 識別會員。

## 聯絡

- 官網：https://short.gooo.name
- 問題回報：https://github.com/gooonamee/short-mcp/issues
- Email：contact.goooname@gmail.com
