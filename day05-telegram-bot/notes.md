# Ngày 5 – Telegram Bot API

**Ngày:** 23/06/2026

## ✅ Đã Hoàn Thành
- [x] Tạo bot @ngochan_aiagent_bot qua @BotFather
- [x] Lấy Bot Token và Chat ID
- [x] Test gửi tin nhắn qua API trực tiếp
- [x] Cài ngrok để expose localhost ra internet
- [x] Kết nối Telegram Trigger vào N8n
- [x] Bot tự động nhận và trả lời tin nhắn

## ⚙️ Thông Tin Bot
- Bot username: @ngochan_aiagent_bot
- Chat ID: 8725284439 (lưu trong .env)

## 🔑 Workflow Đã Xây
```
[Telegram: On Message] → [Telegram: Send Message]
```

## 📋 Cách Khởi Động Mỗi Lần
```powershell
# Terminal 1: Chạy ngrok TRƯỚC
ngrok http 5678

# Terminal 2: Chạy N8n với webhook URL
$env:WEBHOOK_URL="https://kitty-empathic-venomous.ngrok-free.dev"
n8n start
```
⚠️ Ngrok free thay đổi URL mỗi lần restart → cần cập nhật WEBHOOK_URL

## 🔜 Ngày Mai (Ngày 6)
- Thêm Claude AI vào giữa workflow
- Nhận câu hỏi từ Telegram → Claude trả lời → Gửi lại Telegram
- AI Agent đầu tiên hoàn chỉnh!
