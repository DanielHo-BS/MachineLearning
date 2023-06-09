# Kaggle：House Price-Regression

使用的方式為**DNN** by ``keras``  
以`Python`撰寫，程式請參考 main.ipynb

## [Code](./Main.ipynb)

## 步驟

1.資料前處理  
2.模型建構  
3.效果評估  
4.改進

### 資料前處理

```text
載入csv檔後，進行特徵相關性的分析  
發現與sale相關的特徵關聯性較低，將其移除  
使用其他 18個特徵  
進行正規化處理 x=(x- mean) / std  
```

![image](images/corr_price.png)

### 模型建構

```python
model = keras.Sequential(name='model-1')
model.add(layers.Dense(512, kernel_regularizer=keras.regularizers.l2(0.001), activation='relu',
              input_shape=(X_train.shape[1],)))
model.add(layers.Dropout(0.3))
model.add(layers.Dense(256, kernel_regularizer=keras.regularizers.l2(0.001), activation='relu'))
model.add(layers.Dense(128, kernel_regularizer=keras.regularizers.l2(0.001), activation='relu'))
model.add(layers.Dense(64, kernel_regularizer=keras.regularizers.l2(0.001), activation='relu'))
model.add(layers.Dense(32, kernel_regularizer=keras.regularizers.l2(0.001), activation='relu'))
model.add(layers.Dense(1))
#使用L2正規化+Dropout 避免overfitting
#batch_size=256, epochs=500
```

### 效果評估

```text
    loss=keras.losses.MeanSquaredError()
    metrics=[keras.metrics.MeanAbsoluteError()
    #使用MSE與MAE進行評估
```

![image](images/MAE.png)

![image](images/MSE.png)  
  
### 改進

```text
嘗試訓練多個小型model，進行ensemble model
對時間相關的特徵做特徵工程  
```

### 成果

```text
Kaggle：Private Leaderboard(55/159)  
```

 ![image](images/1.png)
