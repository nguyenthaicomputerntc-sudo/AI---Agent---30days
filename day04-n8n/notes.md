# Ngày 4 – N8n Setup & Workflow Đầu Tiên

**Ngày:** 23/06/2026

## ✅ Đã Hoàn Thành
- [x] Cài N8n: `npm install -g n8n`
- [x] Khởi động: `n8n start` → http://localhost:5678
- [x] Tạo account và vào dashboard
- [x] Tạo workflow đầu tiên: Manual Trigger → HTTP Request
- [x] Gọi API thành công, nhận data về

## 🔑 Kiến Thức Quan Trọng

### Cấu trúc Workflow N8n
```
[Trigger Node] → [Action Node] → [Action Node] → ...
```
- **Trigger**: Khi nào workflow chạy (manual, schedule, webhook...)
- **Action**: Làm gì (HTTP Request, gửi email, đăng bài...)
- **Data**: Chảy từ node này sang node khác dạng JSON

### Workflow Đã Tạo
- URL: http://localhost:5678
- Tên: Day4 - HTTP Request Test
- API test: https://dummyjson.com/quotes/random
- Kết quả: Lấy được quote + author từ internet

### Lệnh Khởi Động N8n
```powershell
n8n start
# Mở http://localhost:5678
```

## 📋 Workflow TikTok Tương Lai
```
[Schedule: 8am] → [Claude: Viết script] → [TikTok: Upload] → [Telegram: Thông báo]
```

## 🔜 Ngày Mai (Ngày 5)
- Telegram Bot API
- Tạo bot nhận/gửi tin nhắn
- Kết nối Telegram vào N8n
