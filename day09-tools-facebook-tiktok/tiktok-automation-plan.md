# Kế Hoạch TikTok Automation – Quảng Cáo Ngọc Hân

## 🎯 Mục Tiêu
Tự động tạo và đăng video TikTok mỗi ngày về dịch vụ in ấn/quảng cáo

## 🔄 Workflow Hoàn Chỉnh
```
[Schedule: 8:00 sáng]
        ↓
[Claude: Viết script video]
        ↓
[Google TTS / ElevenLabs: Tạo giọng đọc]
        ↓
[Tạo video (Canva API hoặc FFmpeg)]
        ↓
[TikTok API: Upload video]
        ↓
[Telegram: Thông báo đã đăng xong]
```

## 📝 Node Chi Tiết

### Node 1: Schedule Trigger
- Chạy lúc 8:00 sáng mỗi ngày
- Hoặc thứ 2, 4, 6 hàng tuần

### Node 2: Claude – Viết Script
Prompt cho Claude:
```
Viết script TikTok 30 giây về dịch vụ [chủ đề hôm nay] 
của Quảng Cáo Ngọc Hân. Ngắn gọn, thu hút, 
có call-to-action cuối video. Chủ đề xoay vòng:
- Thứ 2: In tờ rơi, brochure
- Thứ 4: Biển quảng cáo, banner
- Thứ 6: Ly nhựa thương hiệu, bao bì
```

### Node 3: Text-to-Speech
Tùy chọn:
- **Google TTS** (miễn phí): Giọng vi-VN
- **ElevenLabs** (có phí): Giọng tự nhiên hơn

### Node 4: Tạo Video
Tùy chọn:
- **Canva API**: Dùng template có sẵn, ghép text + hình
- **FFmpeg** (local): Ghép ảnh + audio thành video
- **Remotion** (code): Tạo video bằng React

### Node 5: TikTok Upload
- API: TikTok Content Posting API
- Cần: TikTok Developer Account + App được duyệt
- Endpoint: `POST https://open.tiktokapis.com/v2/post/publish/video/init/`

### Node 6: Telegram Notification
- Gửi thông báo: "✅ Đã đăng TikTok lúc 8:05 sáng"
- Kèm link video

## 🔑 API Cần Chuẩn Bị
1. **TikTok Developer Account**: developer.tiktok.com
2. **TikTok App**: Tạo app, xin quyền `video.publish`
3. **Google Cloud TTS** hoặc ElevenLabs API key
4. **Canva API** (optional): canva.com/developers

## 📅 Timeline
- **Ngày 10-11**: Đăng ký TikTok Developer + chờ duyệt
- **Ngày 12**: Setup Google TTS trong N8n
- **Ngày 13**: Tạo video template với Canva/FFmpeg
- **Ngày 14**: Kết nối TikTok API + test upload
- **Ngày 15**: Chạy thử workflow hoàn chỉnh

## ⚠️ Lưu Ý Quan Trọng
- TikTok API cần app được review (7-14 ngày)
- Video phải có âm thanh
- Độ dài khuyến nghị: 15-60 giây
- Tỷ lệ khung: 9:16 (vertical)
- Kích thước tối thiểu: 720x1280px
