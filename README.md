# 異獸紀行：穿越時代的獵人（APP 套件）

## A. 最快：當作 PWA 安裝（不需任何編譯）
1. 把 `www/` 整個資料夾放到任何 https 網站（GitHub Pages、Netlify、Cloudflare Pages 皆可）。
2. 用手機 Chrome（Android）或 Safari（iOS）開啟網址 → 選單「加入主畫面／安裝應用程式」。
3. 之後以全螢幕、橫向、可離線的 APP 方式遊玩（已含 manifest、service worker、圖示）。

## 0. 用 GitHub Actions 自動出 APK / 上線 PWA（推薦，不用裝 Android Studio）
1. 把整個資料夾推到你的 GitHub repo（分支 `main`）。
2. **APK**：Actions →「Build Android APK」會自動執行（也可手動 Run workflow）。完成後在該次執行頁面底部 Artifacts 下載 `yishou-jixing-apk`，傳到手機安裝（需允許「安裝未知來源應用程式」）。推 tag（如 `v1.0.0`）時還會附到 Releases。
3. **PWA 網頁**：Settings → Pages → Source 選 *GitHub Actions*，之後修改 `www/` 就會自動部署到 `https://<帳號>.github.io/<repo>/`。
4. 產出的是 debug 簽章 APK，可安裝試玩；上架 Play 商店需另行設定正式簽章與 AAB。

## B. 打包成 Android APK / AAB（Capacitor）
需求：Node 18+、JDK 17、Android Studio（含 Android SDK）。
```
npm install
npx cap add android
npx cap sync android
npx cap open android      # 在 Android Studio 按 Run 或 Build > Build APK
```
- 想固定橫向：編輯 `android/app/src/main/AndroidManifest.xml`，在 `<activity>` 加上 `android:screenOrientation="sensorLandscape"`。
- 上架前請把 `capacitor.config.json` 的 `appId` 改成你自己的套件名稱（例如 com.yourname.yishou）。
- 更新遊戲內容：改 `www/index.html` 後執行 `npx cap sync android` 再重新建置。

注意：本套件的 Capacitor 部分尚未在實機建置驗證（雲端環境無 Android SDK）；PWA 部分已在瀏覽器實測 service worker 與 manifest 皆正常。
