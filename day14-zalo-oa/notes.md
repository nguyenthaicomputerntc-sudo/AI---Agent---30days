# Ngày 14 – Kết Nối Zalo OA với N8n

**Ngày:** 25/06/2026

## ✅ Đã Hoàn Thành
- [x] Xác thực domain với Cloudflare Tunnel
- [x] Webhook nhận tin nhắn từ Zalo OA thành công
- [x] AI Agent (Claude Haiku) xử lý và tạo phản hồi
- [x] HTTP Request gọi Zalo OA Message API
- [ ] Chờ Zalo duyệt quyền "Gửi tin nhắn" API

## 🔄 Workflow Hoàn Chỉnh

```
[Zalo OA: User nhắn tin]
        ↓
[Webhook: POST /zalo-webhook]
        ↓
[AI Agent: Claude Haiku]
  System: Trợ lý Quảng Cáo Ngọc Hân
  Input: {{ $('Webhook').item.json.body.message.text }}
        ↓
[HTTP Request: Zalo OA API]
  POST https://openapi.zalo.me/v3.0/oa/message/cs
  Header: access_token
  Body: { recipient: { user_id }, message: { text } }
```

## 🛠️ Vấn Đề & Giải Pháp

### 1. Zalo Bot community node lỗi "Not Found"
- **Vấn đề:** Node tự đăng ký webhook nhưng API Zalo thay đổi
- **Giải pháp:** Dùng Webhook node thông thường + đăng ký thủ công

### 2. ngrok free tier có interstitial page
- **Vấn đề:** Zalo không verify được domain qua ngrok (trang cảnh báo)
- **Giải pháp:** Dùng **Cloudflare Tunnel** (`cloudflared tunnel --url http://localhost:5678`)
- **URL:** `https://alien-cylinder-will-throws.trycloudflare.com`

### 3. Zalo domain verification file
- **Vấn đề:** File HTML cần serve tại `/zalo_verifier...html` nhưng N8n thêm `/webhook/` prefix
- **Giải pháp:** Verify URL prefix `https://[cloudflare]/webhook/` thay vì root domain
- **File content:** Full HTML với meta tag `zalo-platform-site-verification`
- **N8n:** Webhook1 (GET) → Respond to Webhook (trả về HTML đầy đủ)

### 4. JSON Body expression lỗi `}}`
- **Vấn đề:** N8n parse `}}` từ nested JSON objects nhầm là kết thúc expression
- **Giải pháp:** Thêm space: `output} })` thay vì `output}})` 
- **Expression:**
```javascript
={{ JSON.stringify({"recipient": {"user_id": $('Webhook').item.json.body.sender.id}, "message": {"text": $('AI Agent').item.json.output} }) }}
```

### 5. App chưa được duyệt (-209)
- **Vấn đề:** Zalo yêu cầu duyệt app trước khi gọi Message API
- **Giải pháp:** Nộp xét duyệt tại Zalo Developer → Đăng ký sử dụng API → Official Account API

## 🔑 Cấu Hình N8n Webhook

**Workflow "zalo" — 3 nodes:**
```
Webhook (POST /zalo-webhook)
    → AI Agent (Claude Haiku 4.5)
    → HTTP Request (Zalo API reply)

Webhook1 (GET /zalo_verifier...html)
    → Respond to Webhook (HTML verification file)
```

**Khởi động N8n:**
```powershell
$env:WEBHOOK_URL="https://alien-cylinder-will-throws.trycloudflare.com"
$env:N8N_RESTRICT_FILE_ACCESS_TO="C:\Users\NGUYEN THAI COMPUTER\"
$env:NODE_FUNCTION_ALLOW_BUILTIN="child_process"
n8n start
```

**Khởi động Cloudflare Tunnel:**
```powershell
cloudflared tunnel --url http://localhost:5678
```

> ⚠️ Cloudflare Tunnel URL thay đổi mỗi lần restart (trừ khi dùng named tunnel)
> Sau khi có URL mới: cập nhật WEBHOOK_URL + webhook URL trong Zalo Developer

## 📊 Zalo OA Data Structure (Webhook payload)

```json
{
  "body": {
    "app_id": "1458177655810374478",
    "user_id_by_app": "...",
    "event_name": "user_send_text",
    "sender": { "id": "USER_ZALO_ID" },
    "recipient": { "id": "OA_ID" },
    "message": {
      "msg_id": "...",
      "text": "Tin nhắn từ user"
    }
  }
}
```

**Field dùng để reply:** `$('Webhook').item.json.body.sender.id`

## 🔜 Ngày 15
- Khi Zalo duyệt API: test bot reply tin nhắn thật
- Named Cloudflare Tunnel (URL cố định)
- Lưu OA Access Token vào N8n Credentials (thay vì hardcode)
- Thêm Memory cho Zalo bot (nhớ lịch sử chat)
