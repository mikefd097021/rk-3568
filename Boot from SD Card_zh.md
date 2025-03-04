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
   如果已掛載，則執行以下命令卸載：
   ```bash
   umount /dev/sdd6
   ```

3. 使用 dd 命令將映像檔寫入對應區塊：
   ```bash
   dd if=<映像檔路徑> of=/dev/sdd6 bs=4M status=progress
   ```

4. 建立掛載用目錄：
   ```bash
   mkdir -p sd_rootfs
   ```

5. 將 rootfs 分區掛載到指定目錄：
   ```bash
   mount /dev/sdd6 sd_rootfs
   ```

6. 調整 rootfs 分區大小：
   ```bash
   resize2fs /dev/sdd6
   ```

7. 驗證分區大小：
   ```bash
   df -h /dev/sdd6
   ```

## 透過sd卡啟動

1. 插入可開機sd卡

2. 如下圖所示，按住指示按鈕後開機


## 注意事項
- 請確保有足夠的權限執行以上命令
- 操作前請確認設備名稱（如 `/dev/sdd6`）是否正確
- 建議在操作前備份重要數據

## 下載