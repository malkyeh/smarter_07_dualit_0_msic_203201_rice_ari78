# 全時期水稻生長UAV光譜影像資料集
## 下載須知  
---
因資料集主要為高解析度無人機影像，影像數量多且容量龐大  
故以外部檔案鏈結形式提供資料下載  

依照資料**蒐集日期**與**資料形式**分別存為個別下載鏈結列表  
列表以`.TXT`文字檔格式儲存  

**文字檔格式與範例**   

  - 命名規則為`[蒐集日期]_[資料形式].txt`  
  - 日期格式為`YYYY-MM-DD`   
  - 資料形式為`RawImagery`或`MosaicImagery`之字串  
  - 範例 `2022-03-22_RawImagery.txt`  

資料下載可透過python簡易撰寫下載器 `downloader.py`  
*(目前僅測試在UNIX/Linux環境運行)*  
用法為 **`downloader.py -i [文字檔位置]`**  
例如 `downloader.py -i ./2022-03-22_RawImagery.txt`  
  
## 資料描述  
---
### 原始影像(RawImagery)  
原始影像為透過無人飛行載具蒐集之空拍影像  
本計畫分別使用可見光與多光譜相機  
進行水稻全生長週期進行拍攝  

**可見光 (Visible)**  
原始影像集內之`RGB`資料夾係由可見光相機拍攝之影像  
影像資料格式為**R、G、B三通道**，各**8位元灰度**(0~255)內容  
並以JPEG壓縮格式儲存，其副檔名為`.jpg`  

**多光譜 (Multispectral)**  
原始影像集內之`6band`資料夾係由多光譜相機拍攝之影像  
本計畫使用相機系統為 [AgEagle Aerial Systems Inc.][ageagle] 生產之 [MicaSense Altum][altum]  
具備五個獨立3.2百萬像素全域快門相機與一個長波紅外(熱影像)相機  

影像為6張一組，命名規則為`IMG_[影像編號]_[波段].tif`，其波段資料如下：  

|編號|光譜|影像畫素|原始資料位元|  
|:-:|:-|:-:|:-:|  
|1|  藍 Blue                                            |  2064 x 1544  |  12 bits|  
|2|  綠 Green                                         |  2064 x 1544  |  12 bits|  
|3|  紅 Red                                             |  2064 x 1544  |  12 bits|  
|4|  近紅外 NIR                                      |  2064 x 1544  |  12 bits|  
|5|  紅邊 Red Edge                                |  2064 x 1544  |  12 bits|  
|6|  長波紅外(熱影像) LWIR (Thermal)  |  160 x 120      |  14 bits|  
*痾... 這個MD竟然不能畫表格*

各波段影像皆以**16位元灰度**(0~65535)之`.tif`格式影像儲存  

### 鑲嵌影像(MosaicImagery)  
鑲嵌影像命名規則：`[日期]_[場域與坵塊編號]_[相機系統]_[飛行高度]_[資料類別].tif` 詳細資訊如下:  

  - 日期格式為`YYYY-MM-DD`  
  - 場域與坵塊編號目前僅收錄霧峰農試所78號田，因此為`ARI78`  
  - 相機系統 可見光為`RGB`、多光譜為`6band`  
  - 飛行高度為數字加上高度單位`m`，例如`40m`  
  - 資料類別分別為鑲嵌正射影像`Ortho`、數值高程模型`DSM`  

鑲嵌影像使用之地理坐標參考系統皆為`TWD97 / TM2 Zone 121 (EPSG:3826)`  
為橫麥卡托二度分帶投影坐標系統  
X軸起點為中央經線 121°E 西移250000m 向東計算  
Y軸起點為緯度0° 向北計算  
單位皆為公尺m  

影像可由軟體[ArcGIS][1]、[QGIS][2]開啟瀏覽  
或以[OSGeo][3]基金會開發之[GDAL/OGR][4]套件操作資料  

[ageagle]: https://ageagle.com/
[altum]: https://support.micasense.com/hc/en-us/articles/360010025413-Altum-Integration-Guide
[1]: https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview
[2]: https://qgis.org/en/site/
[3]: https://www.osgeo.org/
[4]: https://www.osgeo.org/projects/gdal/