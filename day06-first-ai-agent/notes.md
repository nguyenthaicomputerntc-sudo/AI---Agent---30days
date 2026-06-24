# Ngày 6 – AI Agent Đầu Tiên: Claude + Telegram qua N8n

**Ngày:** 24/06/2026

## ✅ Đã Hoàn Thành
- [x] Thêm Claude AI vào giữa workflow N8n
- [x] Kết nối Telegram → Claude → Telegram thành công
- [x] Bot @ngochan_aiagent_bot trả lời bằng AI thật
- [x] Fix lỗi expression mode trong N8n Send Message node

## 🔑 Workflow Hoàn Chỉnh
```
[Telegram Trigger] → [HTTP Request: Claude API] → [Send a text message: Telegram]
```

### Node 1: Telegram Trigger
- Event: On message

### Node 2: HTTP Request (Claude API)
- Method: POST
- URL: `https://api.anthropic.com/v1/messages`
- Headers:
  - `x-api-key`: ANTHROPIC_API_KEY
  - `anthropic-version`: 2023-06-01
  - `content-type`: application/json
- Body:
```json
{
  "model": "claude-haiku-4-5-20251001",
  "max_tokens": 1024,
  "messages": [{"role": "user", "content": "{{ $('Telegram Trigger').item.json.message.text }}"}]
}
```

### Node 3: Send a text message (Telegram)
- Chat ID: `{{ $('Telegram Trigger').item.json.message.chat.id }}`
- Text: `{{ $json.content[0].text }}`  ← **phải bật Expression mode!**

## ⚠️ Lỗi Đã Gặp & Cách Fix

### Lỗi 1: Bot gửi `{{ $json.content[0].text }}` như text thường
- **Nguyên nhân**: Field "Text" trong Send Message node ở chế độ Fixed, không phải Expression
- **Fix**: Click icon `=` ở góc phải field Text → chuyển sang Expression mode → nhập lại expression

### Lỗi 2: Chat ID sai
- **Nguyên nhân**: `{{ $json.message.chat.id }}` — $json đang trỏ vào Claude response
- **Fix**: `{{ $('Telegram Trigger').item.json.message.chat.id }}` — chỉ rõ tên node nguồn

## 📋 Cách Khởi Động Mỗi Lần
```powershell
# Terminal 1: Chạy ngrok TRƯỚC
ngrok http 5678

# Terminal 2: Chạy N8n với webhook URL mới từ ngrok
$env:WEBHOOK_URL="https://[url-moi-tu-ngrok].ngrok-free.app"
n8n start
```
⚠️ Ngrok free thay đổi URL mỗi lần restart → phải cập nhật WEBHOOK_URL

## 🧠 Kiến Thức Quan Trọng

### Expression Mode trong N8n
- **Fixed**: Gửi text y chang, không xử lý `{{ }}`
- **Expression**: Evaluate `{{ }}` như code → lấy data động

### Claude API Response Structure
```json
{
  "content": [
    {"type": "text", "text": "Câu trả lời của Claude..."}
  ]
}
```
→ Lấy text: `$json.content[0].text`

## 🔜 Ngày Mai (Ngày 7)
- Thêm System Prompt để bot có "tính cách" riêng
- Bot biết tên, biết context doanh nghiệp (quảng cáo, in ấn)
- Hoặc kết nối Facebook Messenger vào workflow
