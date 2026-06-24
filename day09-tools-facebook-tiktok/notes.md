# Ngày 9 – Tools, Facebook & TikTok Plan

**Ngày:** 25/06/2026

## ✅ Đã Hoàn Thành
- [x] Thêm Wikipedia Tool vào AI Agent
- [x] Bot tự động tra Wikipedia khi có câu hỏi kiến thức
- [x] Cập nhật System Prompt để cho phép tìm kiếm tổng quát

## 🔧 Wikipedia Tool
- Không cần API key, không cần cấu hình
- AI Agent tự quyết định khi nào dùng tool
- Cần cho phép trong System Prompt nếu bot quá tập trung vào 1 chủ đề

## 🧠 Bài Học: Tools trong AI Agent
AI Agent có thể dùng nhiều tools:
- **Wikipedia**: Tra cứu kiến thức miễn phí
- **HTTP Request Tool**: Gọi bất kỳ API nào
- **Code Tool**: Chạy code JS/Python
- **Calculator**: Tính toán
- **SerpAPI/Tavily**: Tìm kiếm Google (cần API key)

## 📋 Kế Hoạch Facebook Messenger
Cần chuẩn bị:
1. Tài khoản Facebook Developer: developers.facebook.com
2. Tạo App → chọn loại "Business"
3. Thêm sản phẩm "Messenger"
4. Kết nối Facebook Page
5. Lấy Page Access Token
6. Cấu hình Webhook → trỏ về N8n

## 📋 Kế Hoạch TikTok Automation
Workflow mục tiêu:
```
[Schedule: 8am] → [Claude: Viết script] → [TTS: Text to Speech] 
→ [Generate Video] → [TikTok: Upload] → [Telegram: Thông báo]
```
Cần:
- TikTok Developer Account
- TikTok API (Content Posting API)
- Video generation tool (có thể dùng Canva API hoặc FFmpeg)

## 🔜 Ngày Mai (Ngày 10)
- Setup Facebook Developer App
- Kết nối Facebook Messenger vào N8n
- Test bot trả lời qua Facebook
