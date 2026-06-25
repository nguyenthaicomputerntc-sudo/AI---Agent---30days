# Ngày 11 – Workflow Tự Động: Schedule → AI → TTS → Telegram

**Ngày:** 25/06/2026

## ✅ Đã Hoàn Thành
- [x] Thêm Schedule Trigger (8am mỗi ngày)
- [x] Thêm AI Agent viết script TikTok tự động
- [x] Kết nối AI Agent → Google TTS → Telegram audio
- [x] Workflow chạy thành công end-to-end

## 🔄 Workflow Hoàn Chỉnh
```
[Schedule Trigger: 8am]
        ↓
[AI Agent: Viết script TikTok 30 giây]
  + Anthropic Chat Model (Claude Haiku 4.5)
        ↓
[HTTP Request: Google Translate TTS]
  URL: translate.google.com/translate_tts?q={{ encodeURIComponent($('AI Agent').item.json.output) }}&tl=vi&client=tw-ob
        ↓
[Send an audio file: Telegram]
  Chat ID: 8725284439
  Binary File: ON
```

## 🔑 Kiến Thức Quan Trọng

### encodeURIComponent trong N8n
```javascript
{{ encodeURIComponent($('AI Agent').item.json.output) }}
```
Chuyển text thành URL-safe format để Google TTS đọc được

### Thêm Node Vào Giữa 2 Node
- Click vào đường nối giữa 2 node → hiện dấu "+"
- Hoặc: Tab → thêm node → kéo kết nối thủ công

### Schedule Trigger
- Trigger Interval: Days
- Days Between Triggers: 1
- Trigger at Hour: 8am
- Trigger at Minute: 0

## 🔜 Ngày Mai (Ngày 12)
- Đổi tên workflow thành "Day11-Daily-Content"
- Đăng ký TikTok Developer account
- Hoặc: Thêm node gửi text script kèm audio
