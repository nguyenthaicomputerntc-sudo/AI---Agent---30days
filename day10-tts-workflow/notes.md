# Ngày 10 – Google TTS Free + Gửi Audio Telegram

**Ngày:** 25/06/2026

## ✅ Đã Hoàn Thành
- [x] Test Google Cloud TTS (cần billing → bỏ qua)
- [x] Dùng Google Translate TTS miễn phí
- [x] Gửi file audio MP3 về Telegram thành công
- [x] Audio tiếng Việt 4 giây, chất lượng tốt

## 🔑 Google Translate TTS (Miễn Phí)

### URL Template
```
https://translate.google.com/translate_tts?ie=UTF-8&q=NỘI_DUNG&tl=vi&client=tw-ob
```

### Tham số
- `q`: Văn bản cần đọc (URL encode)
- `tl`: Ngôn ngữ (vi = tiếng Việt)
- `client`: tw-ob (bắt buộc)
- Response: File audio/mpeg

### Trong N8n
- Node: HTTP Request
- Method: GET
- URL: URL trên với text mong muốn
- Response Format: File (Binary)

## 📤 Gửi Audio về Telegram

### Node: Send an audio file
- Credential: Telegram account
- Chat ID: 8725284439 (hoặc dynamic)
- Binary File: ON
- Input Binary Field: `{{ $binary.data }}`

## 🔄 Workflow Hoàn Chỉnh (Sắp Xây)
```
[Schedule: 8am] 
    ↓
[AI Agent: Viết script quảng cáo]
    ↓
[HTTP Request: Google TTS → MP3]
    ↓
[Telegram: Gửi audio]
    ↓
[Telegram: Gửi text script kèm theo]
```

## 🔜 Ngày Mai (Ngày 11)
- Kết nối Schedule Trigger với AI Agent
- AI Agent viết script → TTS đọc → Telegram nhận audio mỗi sáng
- Đăng ký TikTok Developer account
