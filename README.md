# CNN_CatvsDog
https://www.kaggle.com/c/dogs-vs-cats-redux-kernels-edition
數據集來自 kaggle競賽：Dogs vs. Cats，訓練集有25000張，貓狗各佔一半。測試集12500張，沒有標註是貓還是狗。

數據預處理 file.py
由於我們的數據集的檔案名是以type.num.jpg這樣的方式命名的，比如cat.0.jpg，但是使用 Keras 的 ImageDataGenerator 需要將不同種類的圖片分在不同的文件夾中，因此我們需要對數據集進行預處理。這裡我們採取的方向是創建符號鏈接(symbol link)，這樣的好處是不用複製圖片，佔用不必要的空間。
├── test [12500 images]
├── test.zip
├── test2
│   └── test -> ../test/
├── train [25000 images]
├── train.zip
└── train2
    ├── cat [12500 images]
    └── dog [12500 images]
  
 
特徵向量 pretrain.py
如果是直接在一個巨大的網絡後面加我們的全連接，那麼訓練10代就需要跑十次巨大的網絡，而且我們的卷積層都是不可訓練的，那麼這個計算就是浪費的。所以我們可以將多個不同的網絡輸出的特徵向量先保存下來，以便後續的訓練，這樣做的好處是我們一旦保存了特徵向量，即使是在普通電腦上也能輕鬆訓練。

預測測試集 buildmodle.py
模型訓練好以後，我們就可以對測試集進行預測

總結
提交到 kaggle 以後，得分也是很棒，0.04040，在全球排名中可以排到17/1314。如果要繼續優化模型表現，可以使用更棒的預訓練模型來導出特徵向量，或者對預訓練模型進行微調（fine-tune），或者進行數據增強（data augmentation）等。
