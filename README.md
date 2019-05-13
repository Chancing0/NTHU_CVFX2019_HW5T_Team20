# NTHU_CVFX_HomeWork5_Team20


# Outline

**1.Take multi-view images by yourselves**

**2.image alignment**

**3.Generate the multi-view 3D visual effects**

**4.Exploit creativity to add some image processing to enhance effect**

**5.Compare&Conclusion**

## **1.Take multi-view images by ourselves**
![](https://i.imgur.com/nsvPc3s.gif)
![](https://media.giphy.com/media/RitcFC4ojyl1fRf1DD/giphy.gif)




## **2.image alignment**
### **Experiment 1.1:**
直接使用兩張原圖做alignment的結果，可以看到alignment的效果不錯，抓到全圖特徵點，但卻沒有一個目標物體。
![](https://i.imgur.com/bNahDde.jpg)
![](https://i.imgur.com/sJGodDo.gif)
### **Experiment 1.2:**
我們的做法是，分別將咖啡杯mask起來，來然後使用這兩張mask圖進行alignment，並使用其前10%-50%的特徵點來進行warping，因爲前10%的點會在mask的邊緣上，不是屬於物體上的點，故捨去。理想狀況是特徵點能很好的描述目標物體的内容和輪廓。
![](https://i.imgur.com/ndjjuin.jpg)
![](https://i.imgur.com/Wx3Lap3.gif)









### **Experiment 2:** 
MAX_FEATURES = 200
GOOD_MATCH_PERCENT = 0.15  

為了方便觀察

![](https://i.imgur.com/QFig1Sn.png)


![](https://i.imgur.com/vCSgsoZ.png)

![](https://i.imgur.com/xEaKmYf.png)

![](https://i.imgur.com/cHkeMpR.png)




## **3.Generate the multi-view 3D visual effects**

- #### 因為alignment會有黑邊問題，先使用cv2.rectangle找出沒有收到alignment影像的範圍，

![](https://i.imgur.com/AGgEkr1.png)
上圖ok
![](https://i.imgur.com/OvsxV1c.png)
篩選出不成功案例
![](https://i.imgur.com/QR2gvcx.png)
![](https://i.imgur.com/ECi1Dcl.png)
![](https://i.imgur.com/X7Iwn2D.png)

篩選完挑一組連續的好的最結果，出來

效果不好，因爲影像t的目標物體大小和位置只取決於前一張影像It-1，而與更早的影像It-2和之前的影像無關，造成目標物體位置和大小一直變動。

![](https://media.giphy.com/media/KDQSBGIpN6yoeyMS0n/giphy.gif)


![](https://media.giphy.com/media/Kc7RQMPphWSrj7DmAE/giphy.gif)

- #### 如果是每次都參考前一張對齊好的影像，因爲該影像已輕微形變，則錯誤偏移量會逐次纍積，對齊后的影像會越來越傾斜，導致無法完成更後續影像的對齊。但是效果卻比較符合我們的期望，目標物體的大小和位置都相對保持一致。
![](https://i.imgur.com/TRTtM09.gif)


- #### 使用後製軟體AE

首先設定圖片中深度資訊，然後使用map進行水平方向和垂直方向來調節。

效果如下
![](https://media.giphy.com/media/lNACVBhbrspEX2JsV6/giphy.gif)
AE结果

![origin_image](main.gif)

**若是看不到結果，請點擊[這裡](https://media.giphy.com/media/lNACVBhbrspEX2JsV6/giphy.gif)**

## **4.Exploit creativity to add some image processing to enhance effect**

我們認為live photo效果
1. 最好的情況是把影像當中`本該移動`的物體讓他停止移動。
1. 次好的情況是把影像當中`可以移動也可以不移動`的物體讓他停止移動。（因為這種情況可以被看成camera在全程錄影過程中的位置保持靜止）

- ### live photo 

- ### live photo （using post-process software）




| before process                                                   | after process                                                               |
|------------------------------------------------------------------|-----------------------------------------------------------------------------|
| ![](https://thumbs.gfycat.com/NewRealAdouri-size_restricted.gif) | ![](https://thumbs.gfycat.com/SadJollyIndianspinyloach-size_restricted.gif) |
| 原圖，畫面晃動                                                   | 雖然背景畫面靜止了，但是沒有很明顯的live photo的效果                                              |


| after process                                                           | after process                                                             | after process                                                             |
|-------------------------------------------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------|
| ![](https://thumbs.gfycat.com/AmusingBlueCockatiel-size_restricted.gif) | ![](https://thumbs.gfycat.com/PolishedFloweryLadybug-size_restricted.gif) | ![](https://thumbs.gfycat.com/TameImportantHamadryad-size_restricted.gif) |
| 雖然背景畫面靜止了，植物在移動，但是沒有很明顯的live photo的效果       |      雖然背景畫面靜止了，龍頭的水流在移動，但是沒有很明顯的live photo的效果                                                                     |            雖然背景畫面靜止了，老鷹在移動，但是沒有很明顯的live photo的效果                                                                |


效果最好的情况


| before process                                                              | after process                                                                   |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| ![](https://thumbs.gfycat.com/HollowPerfectDwarfrabbit-size_restricted.gif) | ![](https://thumbs.gfycat.com/TediousHelplessBeardeddragon-size_restricted.gif) |
| 原圖，畫面晃動                                                              | 效果最好的圖，天空的畫面穩定，而海水保持流動                                                  |


## **5.Compare&Conclusion**







