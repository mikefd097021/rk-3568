# SD Card 開機指南

## 製作可開機sd卡

### 準備工作
- 請確保已下載 SDDiskTool 工具和系統映像檔
- 準備一張 SD 卡（建議容量 >= 32GB）
- 將 SD 卡接入電腦

### 操作步驟

1. 啟動 SDDiskTool 工具程式
   > 💡 第一次使用時可能需要管理員權限

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/01.png?raw=true" alt="啟動 SDDiskTool">
   </div>

2. 選擇 SD 卡裝置
   > ⚠️ 請仔細確認選擇的是正確的 SD 卡裝置，避免損壞其他儲存裝置

3. 勾選 SD Boot 功能
   > 這個步驟很重要，它將使 SD 卡變為可開機狀態

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/02.png?raw=true" alt="啟用 SD Boot">
   </div>

4. 載入韌體檔案
   > 點選 Firmware 欄位旁的按鈕，選擇系統映像檔（sdupdate.img）

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/03.png?raw=true" alt="選擇韌體位置">
   </div>

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/04.png?raw=true" alt="載入韌體檔案">
   </div>

5. 開始製作開機卡
   > 確認所有設定後，點選 Create 開始製作
   > 
   > ⚠️ 製作過程中請勿移除 SD 卡

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/05.png?raw=true" alt="開始製作">
   </div>

### 注意事項
- 製作過程會清除 SD 卡中的所有資料，請提前備份重要資料
- 若製作失敗，請檢查：
  1. SD 卡是否正確插入
  2. 選擇的裝置是否正確
  3. 韌體檔案是否完整
  4. 嘗試使用管理員權限執行

## 寫入與調整 rootfs 步驟

1. 如下圖所示，找到 rootfs 所在區塊（`/dev/sdd6`）

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/1.png?raw=true" alt="rootfs區塊位置">
   </div>
   
2. 確認分區掛載狀態
   ```bash
   mount | grep /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/2.png?raw=true" alt="操作截圖">
   </div>

   如果已掛載，則執行以下命令卸載：
   ```bash
   umount /dev/sdd6
   ```
   
   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/3.png?raw=true" alt="操作截圖">
   </div>

3. 使用 dd 命令將映像檔寫入對應區塊：
   ```bash
   dd if=<映像檔路徑> of=/dev/sdd6 bs=4M status=progress
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/4.png?raw=true" alt="操作截圖">
   </div>

4. 建立掛載用目錄：
   ```bash
   mkdir -p sd_rootfs
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/5.png?raw=true" alt="操作截圖">
   </div>

5. 將 rootfs 分區掛載到指定目錄：
   ```bash
   mount /dev/sdd6 sd_rootfs
   ```

6. 調整 rootfs 分區大小：
   ```bash
   resize2fs /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/6.png?raw=true" alt="操作截圖">
   </div>

7. 驗證分區大小：
   ```bash
   df -h /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/7.png?raw=true" alt="操作截圖">
   </div>

### 注意事項
- 請確保有足夠的權限執行以上命令
- 操作前請確認設備名稱（如 `/dev/sdd6`）是否正確
- 建議在操作前備份重要數據

## 透過sd卡啟動

1. 插入可開機sd卡

2. 如下圖所示，按住指示按鈕後開機

## 下載

### 系統映像檔
| 項目 | 內容 |
|------|------|
| 檔案名稱 | sdupdate.img |
| SHA256 校驗碼 | e5952745f70e8ade64298275c975e2bf3d6994f10b319bbc3efb50883d15f0f3 |
| 下載連結 | 請連絡相關人員索取 |

### 寫入工具
| 項目 | 內容 |
|------|------|
| 檔案名稱 | SDDiskTool_v1.69.rar |
| 下載連結 | [Google Drive](https://drive.google.com/file/d/1r7RXZHWlw9ci0WIcBxocYn9qbAhL48nu/view?usp=sharing) |
| 密碼 | 請連絡相關人員索取 |

