# Ngày 7 – System Prompt & Fix Expression

**Ngày:** 24/06/2026

## ✅ Đã Hoàn Thành
- [x] Fix lỗi expression `{{ $json.content[0].text }}` không evaluate
- [x] Dùng node reference đầy đủ: `{{ $('HTTP Request').item.json.content[0].text }}`
- [x] Thêm System Prompt → bot có tính cách riêng
- [x] Bot tự giới thiệu là trợ lý AI của Quảng Cáo Ngọc Hân

## 🔑 Fix Lỗi Expression

### Vấn đề
`{{ $json.content[0].text }}` gửi literal text thay vì evaluate

### Nguyên nhân
Trong N8n, khi có nhiều node, `$json` có thể không trỏ đúng node mong muốn

### Giải pháp
Dùng tên node cụ thể thay vì `$json`:
```
{{ $('HTTP Request').item.json.content[0].text }}
```

## 🤖 System Prompt

Thêm field `"system"` vào body của HTTP Request node:

```json
{
  "model": "claude-haiku-4-5-20251001",
  "max_tokens": 1024,
  "system": "Bạn là trợ lý AI của Quảng Cáo Ngọc Hân - công ty chuyên in ấn, biển quảng cáo, in lớn, bao bì sản phẩm và ly nhựa thương hiệu. Hãy trả lời ngắn gọn, thân thiện bằng tiếng Việt. Khi khách hỏi về dịch vụ, hãy tư vấn nhiệt tình về in ấn và quảng cáo.",
  "messages": [
    {
      "role": "user",
      "content": "{{ $('Telegram Trigger').item.json.message.text }}"
    }
  ]
}
```

### Kết quả
Bot tự giới thiệu:
- Tên: Trợ lý AI của Quảng Cáo Ngọc Hân
- Dịch vụ: In ấn, biển quảng cáo, bao bì, ly nhựa, in lớn
- Ngôn ngữ: Tiếng Việt, thân thiện

## 📋 Workflow Hoàn Chỉnh (4 Node)
```
[Telegram Trigger] → [HTTP Request: Claude API] → [Edit Fields] → [Send a text message]
```

## 🧠 Kiến Thức Quan Trọng

### Node Reference trong N8n
```javascript
// Cách 1: $json — trỏ vào output của node NGAY TRƯỚC
{{ $json.field }}

// Cách 2: Tên node cụ thể — luôn đúng dù workflow phức tạp
{{ $('Tên Node').item.json.field }}
```

### System Prompt vs User Message
- **System Prompt**: Định nghĩa tính cách, vai trò, ngữ cảnh của bot
- **User Message**: Câu hỏi/yêu cầu từ người dùng
- System Prompt chạy mỗi lần nhưng không hiển thị cho user

## 🔜 Ngày Mai (Ngày 8)
- Thêm conversation history (bot nhớ context)
- Hoặc kết nối thêm kênh (Facebook, Zalo)
- Hoặc tạo workflow TikTok tự động
