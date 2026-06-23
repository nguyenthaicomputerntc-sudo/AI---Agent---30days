# Ngày 3 – GitHub Workflow Nâng Cao

**Ngày:** 23/06/2026

## ✅ Đã Hoàn Thành
- [x] Tạo và chuyển sang branch mới: day03-github-workflow
- [x] Tạo .gitignore bảo vệ API keys
- [x] Tạo .env.example làm template

## 🔑 Kiến Thức Quan Trọng

### Branch Workflow
```
main          ← code ổn định, production
  └── day03-github-workflow  ← code thử nghiệm
  └── feature/telegram-bot   ← tính năng mới
  └── fix/api-error          ← sửa lỗi
```

### Quy Tắc Bảo Mật
- `.env` → lưu API keys thật → KHÔNG commit
- `.env.example` → template không có keys → OK commit
- `.gitignore` → danh sách file Git bỏ qua

### Cách Dùng .env
```python
from dotenv import load_dotenv
import os

load_dotenv()
token = os.getenv("TELEGRAM_BOT_TOKEN")
```

## 🔜 Ngày Mai (Ngày 4)
- Cài đặt N8n
- Tạo workflow đầu tiên
