# Casmara Email Template Editor

一個功能完整的電子郵件模板編輯器，用於創建和自定義 Casmara Beauty Advisor 的訪問通知郵件。

## 功能特點

- 📝 實時編輯電子郵件內容
- 👀 即時預覽效果
- 📋 一鍵複製 HTML 代碼
- 📱 響應式設計，支持移動設備
- 🎨 現代化 UI 設計
- ⚡ 純靜態文件，無需服務器

## 快速開始

### 本地運行

1. 下載項目文件
2. 在瀏覽器中直接打開 `editable_email_template.html`

或使用本地服務器：
```bash
# Python 3
python3 -m http.server 8000

# Node.js
npx serve .

# PHP
php -S localhost:8000
```

然後訪問 `http://localhost:8000/editable_email_template.html`

## 快速部署

### 🚀 Vercel（推薦）
```bash
npm i -g vercel
vercel
```

### 🌐 Netlify
1. 拖放文件夾到 [netlify.com](https://netlify.com)
2. 或使用 CLI：`netlify deploy`

### 📚 GitHub Pages
1. 推送到 GitHub 倉庫
2. 啟用 Pages 功能
3. 選擇 main 分支

## 項目結構

```
.
├── editable_email_template.html    # 主應用文件
├── vercel.json                     # Vercel 配置
├── netlify.toml                    # Netlify 配置
├── .htaccess                       # Apache 配置
├── nginx.conf                      # Nginx 配置示例
├── .github/workflows/deploy.yml    # GitHub Actions
├── DEPLOYMENT_GUIDE.md             # 詳細部署指南
└── README.md                       # 本文件
```

## 使用說明

1. **編輯內容**：在左側編輯器中填寫客戶和訪問信息
2. **實時預覽**：右側會實時顯示郵件效果
3. **複製代碼**：點擊「複製 HTML」按鈕獲取完整郵件代碼
4. **重置表單**：點擊「重置」按鈕恢復默認值

## 技術規格

- **前端**：HTML5, CSS3, Vanilla JavaScript
- **樣式**：CSS Grid, Flexbox, CSS 動畫
- **字體**：Google Fonts (Playfair Display, Inter)
- **兼容性**：現代瀏覽器（Chrome 60+, Firefox 60+, Safari 12+）
- **響應式**：支持桌面、平板、手機

## 瀏覽器支持

| 瀏覽器 | 版本 |
|--------|------|
| Chrome | 60+ |
| Firefox | 60+ |
| Safari | 12+ |
| Edge | 79+ |

## 部署選項

詳細的部署指南請參考 [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md)，包含：

- 靜態網站部署（Vercel, Netlify, GitHub Pages）
- 傳統服務器部署（Apache, Nginx）
- 雲服務部署（AWS, GCP, Azure）

## 許可證

© 2025 Casmara. 保留所有權利。

## 支持

如遇問題，請檢查：
- 瀏覽器開發者工具控制台
- 網絡連接狀態
- JavaScript 是否已啟用