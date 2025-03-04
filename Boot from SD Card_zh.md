# SD Card 開機指南

## 製作可開機sd卡



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

## 透過sd卡啟動

1. 插入可開機sd卡

2. 如下圖所示，按住指示按鈕後開機


## 注意事項
- 請確保有足夠的權限執行以上命令
- 操作前請確認設備名稱（如 `/dev/sdd6`）是否正確
- 建議在操作前備份重要數據

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

