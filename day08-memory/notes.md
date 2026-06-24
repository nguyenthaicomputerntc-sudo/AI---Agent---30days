# Ngày 8 – Conversation Memory: Bot Nhớ Lịch Sử Chat

**Ngày:** 25/06/2026

## ✅ Đã Hoàn Thành
- [x] Tạo workflow mới "Day8-AI" với n8n AI Agent node
- [x] Kết nối Anthropic Chat Model (Claude Haiku 4.5)
- [x] Thêm Simple Memory → bot nhớ lịch sử hội thoại
- [x] Test thành công: nói tên → hỏi lại → bot nhớ đúng
- [x] Thêm System Prompt → bot có tính cách Quảng Cáo Ngọc Hân

## 🔑 Workflow Hoàn Chỉnh
```
[Telegram Trigger] → [AI Agent] → [Send a text message]
                          ↑
              [Anthropic Chat Model] + [Simple Memory]
```

## ⚙️ Cấu Hình Chi Tiết

### AI Agent Node
- Source for Prompt: Define below
- Prompt: `{{ $('Telegram Trigger').item.json.message.text }}`
- System Message: "Bạn là trợ lý AI của Quảng Cáo Ngọc Hân..."

### Anthropic Chat Model
- Model: Claude Haiku 4.5
- Credential: Anthropic account

### Simple Memory
- Session ID: Define below
- Session Key: `{{ $('Telegram Trigger').item.json.message.chat.id }}`
- Context Window Length: 5 (nhớ 5 tin nhắn gần nhất)

### Send a text message
- Chat ID: `{{ $('Telegram Trigger').item.json.message.chat.id }}`
- Text: `{{ $json.output }}`  ← output từ AI Agent

## 🧠 Kiến Thức Quan Trọng

### AI Agent vs HTTP Request
| | HTTP Request | AI Agent Node |
|---|---|---|
| Memory | ❌ Không có | ✅ Có sẵn |
| Cấu hình | Phức tạp | Đơn giản |
| Tools | ❌ | ✅ Có thể thêm |
| Output | `$json.content[0].text` | `$json.output` |

### Simple Memory
- Lưu trong RAM của n8n (mất khi restart)
- Session ID = chat.id → mỗi user có memory riêng
- Context Window = số tin nhắn được nhớ

### Khi Nào Dùng Simple Memory vs Database
- **Simple Memory**: Dev/test, không cần persist
- **Postgres/Redis**: Production, cần lưu lâu dài

## 🔜 Ngày Mai (Ngày 9)
- Kết nối Facebook Messenger hoặc Zalo
- Hoặc thêm Tools cho AI Agent (tìm kiếm web, đọc file...)
- Hoặc tạo workflow TikTok tự động
