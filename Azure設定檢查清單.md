# Azure 設定檢查清單

## ⚠️ 重要：必須完成的 Azure Portal 設定

根據您提供的 Azure Portal 截圖，需要完成以下設定：

---

## ✅ 步驟 1：儲存重新導向 URI

### 當前狀態
- ✅ 新 URI `https://teamsapp-test.vercel.app` 已在右側面板顯示
- ⚠️ 需要點擊「設定」或「儲存」按鈕保存

### 操作步驟
1. 在 Azure Portal 的「驗證」頁面
2. 確認右側面板中的 `https://teamsapp-test.vercel.app` 有綠色勾號
3. 點擊右側面板底部的「**設定**」按鈕
4. 或點擊左側主面板底部的「**儲存**」按鈕
5. 等待保存成功

---

## ✅ 步驟 2：更新應用程式識別碼 URI（最重要！）

### 位置
Azure Portal > Azure Active Directory > 應用程式註冊 > RHEMA 請款系統 > **公開 API**

### 需要更新為
```
api://teamsapp-test.vercel.app/33abd69a-d012-498a-bddb-8608cbf10c2d
```

### 操作步驟
1. 前往「公開 API」頁面
2. 點擊「**編輯應用程式識別碼 URI**」
3. 將 URI 更新為上述值
4. 點擊「**儲存**」

---

## ✅ 步驟 3：確認範圍（Scopes）

### 位置
Azure Portal > Azure Active Directory > 應用程式註冊 > RHEMA 請款系統 > **公開 API > 範圍**

### 需要確認範圍
- **範圍名稱**：`access_as_user`
- **完整範圍**：`api://teamsapp-test.vercel.app/33abd69a-d012-498a-bddb-8608cbf10c2d/access_as_user`
- **狀態**：已啟用

### 如果範圍不存在
1. 點擊「**新增範圍**」
2. 填寫以下資訊：
   - **範圍名稱**：`access_as_user`
   - **誰可以同意**：管理員和使用者
   - **管理員同意顯示名稱**：`Teams 可以以使用者身分存取應用程式`
   - **管理員同意描述**：`允許 Teams 以登入使用者的身分呼叫應用程式的 API`
   - **使用者同意顯示名稱**：`Teams 可以以您的身分存取應用程式`
   - **使用者同意描述**：`允許 Teams 以您的身分呼叫應用程式的 API`
   - **狀態**：已啟用
3. 點擊「**新增範圍**」

---

## ✅ 步驟 4：確認授權的用戶端應用程式

### 位置
Azure Portal > Azure Active Directory > 應用程式註冊 > RHEMA 請款系統 > **公開 API > 授權的用戶端應用程式**

### 需要確認的用戶端
1. **用戶端識別碼**：`1fec8e78-bce4-4aaf-ab1b-5451cc387264`（Teams 桌面版）
2. **用戶端識別碼**：`5e3ce6c0-2b1f-4285-8d4b-75ee78787346`（Teams 網頁版）

### 如果用戶端不存在
1. 點擊「**新增用戶端應用程式**」
2. 輸入用戶端識別碼
3. 選擇範圍：`api://teamsapp-test.vercel.app/33abd69a-d012-498a-bddb-8608cbf10c2d/access_as_user`
4. 點擊「**新增**」

---

## ✅ 步驟 5：在 Teams 重新上傳應用程式

### 為什麼需要重新上傳？
因為 manifest.json 中的 URL 已經更新，需要上傳新版本。

### 操作步驟
1. **移除舊的應用程式**（如果有的話）
   - Teams > 應用程式 > 管理您的應用程式
   - 找到「Teams SSO 測試」
   - 移除它

2. **上傳新的應用程式包**
   - Teams > 應用程式 > 上傳自訂應用程式
   - 選擇「為 [您的組織] 上傳」
   - 選擇 `RHEMA-Teams-App.zip`
   - 點擊「新增」

3. **測試應用程式**
   - 在 Teams 中打開應用程式
   - 檢查是否能正常載入
   - 檢查 SSO 登入是否成功

---

## 🔍 檢查清單

完成所有設定後，確認以下項目：

### Azure Portal 設定
- [ ] 重新導向 URI 已儲存：`https://teamsapp-test.vercel.app`
- [ ] 應用程式識別碼 URI 已更新：`api://teamsapp-test.vercel.app/33abd69a-d012-498a-bddb-8608cbf10c2d`
- [ ] 範圍已確認：`api://teamsapp-test.vercel.app/33abd69a-d012-498a-bddb-8608cbf10c2d/access_as_user`
- [ ] 授權的用戶端應用程式已確認

### Teams 應用程式
- [ ] 已重新上傳新的應用程式包
- [ ] 應用程式能正常載入
- [ ] SSO 登入功能正常

---

## 🐛 常見問題

### 問題：Teams 顯示「找不到此 App」

**可能原因：**
1. 應用程式識別碼 URI 未更新
2. manifest.json 中的 URL 與 Azure 設定不一致
3. 應用程式需要重新上傳

**解決方案：**
1. 確認應用程式識別碼 URI 已更新
2. 確認 manifest.json 中的 URL 正確
3. 重新上傳應用程式包

### 問題：SSO 登入失敗

**可能原因：**
1. 重新導向 URI 未正確設定
2. 範圍未正確設定
3. 授權的用戶端應用程式未設定

**解決方案：**
1. 確認重新導向 URI 已儲存
2. 確認範圍已正確設定
3. 確認授權的用戶端應用程式已新增

---

## 📝 重要提醒

1. **應用程式識別碼 URI 必須與 manifest.json 中的 resource 一致**
2. **重新導向 URI 必須與 Vercel 部署 URL 一致**
3. **設定變更後，可能需要等待幾分鐘才會生效**
4. **Teams 應用程式需要重新上傳才能使用新的設定**

---

**完成所有設定後，請重新上傳 Teams 應用程式包並測試！**

