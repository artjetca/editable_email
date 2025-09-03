# Casmara Email Template 部署指南

本項目是一個純靜態 HTML 應用程序，包含一個可編輯的電子郵件模板編輯器。以下是各種部署選項的詳細說明。

## 項目概述

- **項目類型**: 純靜態 HTML/CSS/JavaScript
- **主文件**: `editable_email_template.html`
- **依賴**: 僅使用 CDN 資源（Google Fonts）
- **瀏覽器兼容性**: 現代瀏覽器（支持 ES6+）

## 部署選項

### 1. 靜態網站部署（推薦）

#### 1.1 Vercel 部署

**優點**: 免費、快速、全球 CDN、自動 HTTPS

**步驟**:
1. 註冊 [Vercel](https://vercel.com) 帳戶
2. 安裝 Vercel CLI: `npm i -g vercel`
3. 在項目目錄執行: `vercel`
4. 按照提示完成部署
5. 使用提供的 `vercel.json` 配置文件

**命令部署**:
```bash
cd /path/to/your/project
vercel --prod
```

#### 1.2 Netlify 部署

**優點**: 免費、表單處理、分支預覽、自動 HTTPS

**方法一 - 拖放部署**:
1. 訪問 [Netlify](https://netlify.com)
2. 將整個項目文件夾拖放到部署區域
3. 自動部署完成

**方法二 - Git 部署**:
1. 將代碼推送到 GitHub/GitLab
2. 在 Netlify 連接 Git 倉庫
3. 使用提供的 `netlify.toml` 配置

**方法三 - CLI 部署**:
```bash
npm install -g netlify-cli
netlify deploy
netlify deploy --prod
```

#### 1.3 GitHub Pages 部署

**優點**: 免費、與 GitHub 集成、版本控制

**步驟**:
1. 創建 GitHub 倉庫
2. 推送代碼到 `main` 分支
3. 在倉庫設置中啟用 GitHub Pages
4. 選擇 `main` 分支作為源
5. 使用提供的 GitHub Actions 工作流程

**自動部署**:
- 使用 `.github/workflows/deploy.yml` 實現自動部署
- 每次推送到 main 分支時自動更新

### 2. 傳統 Web 服務器部署

#### 2.1 Apache 部署

**配置文件** (`.htaccess`):
```apache
RewriteEngine On
RewriteRule ^$ editable_email_template.html [L]

# 安全頭部
Header always set X-Frame-Options DENY
Header always set X-Content-Type-Options nosniff
Header always set X-XSS-Protection "1; mode=block"

# 緩存設置
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresByType text/html "access plus 1 hour"
    ExpiresByType text/css "access plus 1 month"
    ExpiresByType application/javascript "access plus 1 month"
</IfModule>
```

**部署步驟**:
1. 將所有文件上傳到 web 根目錄
2. 確保 Apache 啟用了 mod_rewrite 和 mod_expires
3. 設置適當的文件權限 (644 for files, 755 for directories)

#### 2.2 Nginx 部署

**配置文件** (`nginx.conf`):
```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /path/to/your/project;
    index editable_email_template.html;

    # 安全頭部
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";

    # 根路徑重定向
    location = / {
        try_files /editable_email_template.html =404;
    }

    # 靜態文件緩存
    location ~* \.(css|js|png|jpg|jpeg|gif|ico|svg)$ {
        expires 1M;
        add_header Cache-Control "public, immutable";
    }

    # HTML 文件
    location ~* \.html$ {
        expires 1h;
        add_header Cache-Control "public";
    }
}
```

### 3. 雲服務部署

#### 3.1 AWS S3 + CloudFront

**步驟**:
1. 創建 S3 存儲桶
2. 啟用靜態網站託管
3. 上傳文件到 S3
4. 配置 CloudFront 分發
5. 設置自定義域名（可選）

**AWS CLI 部署**:
```bash
aws s3 sync . s3://your-bucket-name --delete
aws cloudfront create-invalidation --distribution-id YOUR_DISTRIBUTION_ID --paths "/*"
```

#### 3.2 Google Cloud Storage

**步驟**:
1. 創建 GCS 存儲桶
2. 啟用靜態網站託管
3. 上傳文件
4. 配置 Cloud CDN（可選）

#### 3.3 Azure Static Web Apps

**步驟**:
1. 在 Azure Portal 創建 Static Web App
2. 連接 GitHub 倉庫
3. 配置構建設置（無需構建步驟）
4. 自動部署

## 部署前檢查清單

- [ ] 確保所有外部資源（字體、圖片）使用 HTTPS
- [ ] 測試所有 JavaScript 功能
- [ ] 驗證響應式設計
- [ ] 檢查瀏覽器兼容性
- [ ] 設置適當的安全頭部
- [ ] 配置緩存策略

## 推薦部署方案

1. **開發/測試**: Netlify 拖放部署
2. **生產環境**: Vercel 或 Netlify（Git 集成）
3. **企業級**: AWS S3 + CloudFront
4. **預算有限**: GitHub Pages

## 故障排除

### 常見問題

1. **JavaScript 不工作**
   - 檢查瀏覽器控制台錯誤
   - 確保使用 HTTPS（某些功能需要安全上下文）

2. **字體未加載**
   - 檢查 Google Fonts CDN 連接
   - 驗證網絡連接

3. **移動端顯示問題**
   - 檢查 viewport meta 標籤
   - 測試響應式 CSS

### 性能優化

1. **啟用 Gzip 壓縮**
2. **設置適當的緩存頭部**
3. **使用 CDN 加速**
4. **優化圖片（如有）**

## 聯繫支持

如需技術支持，請檢查:
- 瀏覽器開發者工具
- 服務器錯誤日誌
- 網絡連接狀態

---

**注意**: 此項目不需要服務器端處理，純靜態部署即可滿足所有功能需求。