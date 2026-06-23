# Ngày 2 – MCP Basics

**Ngày:** 23/06/2026

## ✅ Đã Hoàn Thành
- [x] Cài @modelcontextprotocol/server-filesystem (npm install -g)
- [x] Kết nối MCP Filesystem vào Claude Desktop
- [x] Test thành công: Claude đọc được file thật trên máy

## 🔑 Bài Học Quan Trọng
1. **File config đúng** là file Claude Desktop dùng trong Settings → Developer → Edit Config
   - Không phải tự tìm đường dẫn, dùng "Edit Config" để mở đúng file
2. **Encoding UTF-8** quan trọng khi dùng PowerShell ghi file JSON có tiếng Việt
3. **Dùng đường dẫn tuyệt đối** cho node.exe thay vì `npx` để tránh lỗi PATH
4. **Giữ nguyên preferences** khi thêm mcpServers vào config file

## ⚙️ Config Đang Dùng
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "C:\\Program Files\\nodejs\\node.exe",
      "args": [
        "C:\\Users\\NGUYEN THAI COMPUTER\\AppData\\Roaming\\npm\\node_modules\\@modelcontextprotocol\\server-filesystem\\dist\\index.js",
        "E:\\hoc-ai-agent"
      ]
    }
  }
}
```

## 📍 Vị Trí Config File
Settings → Developer → Edit Config (Claude Desktop tự mở đúng file)

## 🔜 Ngày Mai (Ngày 3)
- GitHub workflow nâng cao: branch, pull request
- Cấu trúc dự án chuẩn cho AI Agent project
