# Ngày 12 – Nâng Cấp Workflow + TikTok Developer

**Ngày:** 25/06/2026

## ✅ Đã Hoàn Thành
- [x] Nâng cấp prompt AI Agent xoay chủ đề theo ngày
- [x] Thêm node Send Text gửi kèm script
- [ ] Đăng ký TikTok Developer account
- [ ] Commit GitHub

## 🔄 Workflow Nâng Cấp

```
[Schedule: 8am]
      ↓
[AI Agent: Prompt xoay theo ngày]
      ↓
[HTTP Request: Google TTS]
      ↓
[Send audio file: Telegram]
      ↓
[Send text message: Telegram] ← MỚI
```

## 🔑 Prompt Xoay Theo Ngày (AI Agent)

```javascript
Viết script TikTok 30 giây bằng tiếng Việt về {{ $now.format('d') === '1' ? 'in tờ rơi và brochure' : $now.format('d') === '2' ? 'biển quảng cáo và banner' : $now.format('d') === '3' ? 'in bao bì và nhãn hàng' : $now.format('d') === '4' ? 'ly nhựa in thương hiệu' : $now.format('d') === '5' ? 'standee và backdrop sự kiện' : 'dịch vụ in ấn tổng hợp' }} của Quảng Cáo Ngọc Hân. Ngắn gọn, thu hút, có call-to-action. Chỉ trả về nội dung script.
```

## 📝 Node Gửi Text Script (Telegram)

- Node: Send a text message
- Chat ID: 8725284439
- Text:
```
📝 Script TikTok hôm nay:

{{ $('AI Agent').item.json.output }}

---
🎙️ Audio đã gửi phía trên ↑
```

## 🎵 TikTok Developer Setup

**URL**: https://developers.tiktok.com

**Bước:**
1. Login bằng TikTok account
2. Manage apps → Connect an app
3. App name: NgocHan AI Agent
4. Products: Content Posting API → scope: video.publish
5. Submit review → chờ 7-14 ngày

**Lưu vào .env sau khi có:**
```
TIKTOK_CLIENT_KEY=
TIKTOK_CLIENT_SECRET=
TIKTOK_REDIRECT_URI=http://localhost:5678/oauth2/callback
```

## 🔜 Ngày 13
- Nếu TikTok duyệt: setup OAuth flow trong N8n
- Nếu chưa duyệt: làm video template với FFmpeg hoặc Canva
- Thêm ElevenLabs TTS (giọng tự nhiên hơn Google)
