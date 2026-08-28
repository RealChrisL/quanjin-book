# 全謹預約頁(LIFF)

`index.html` — LINE LIFF 預約入口,服務於 https://book.talent3000.com/

- LIFF app:`2011298513-aJ8dyNQ0`(全謹預約 Login channel,**全謹代書** provider)
- 身分自解:`liff.getProfile()` 的 userId → cal.com `metadata[line_uid]`,
  與 Messaging API webhook 的 userId 同源(userId 是 provider-scoped)
- 預約閘:`GET /booking-gate/{uid}` — 已有在途預約則擋下重複下單(fail-open)
- `?debug=1` — 顯示解析到的 userId,用於驗證 provider 綁定

**改動前請先看 line-bot 的 `lib/outbound_validator.py:_BOOKING_LINK_MARKERS`
與 `scripts/hook_reply_gate.py`** — 本頁網址是 L7 連結鎖的標記之一,
換網址必須同步更新兩處,否則 agent 洩漏新網址時不會被攔。
