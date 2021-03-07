Лабораторная работа 1.  
====

### Немного информации о цели лабараторной работы.
В данной лабораторной работе нужно было подготовить работоспособное окружение для решения задачи классификации изображений из набора данных Oregon Wildlife с использованием
нейронных сетей глубокого обучения. Набора данных Oregon Wildlife включает 12000 изображений дикой природы. Для обучения двумерной сверточной нейронной сети использовалось 50 эпох, каждая из который разделелна на части(батч) включающее 512 изображений.  

# 2. С использованием примера[1] обучить представленную реализацию нейронной сети для решения задачи классификации изображений Oregon-Wild-Life
* **Описание архитектуры:**   
* 
* Размерность входного изображения (224x224x3): 
```
inputs = tf.keras.Input(shape=(RESIZE_TO, RESIZE_TO, 3))
```

* Слой 2D свертки размером 222х222х8
```
x = tf.keras.layers.Conv2D(filters=8, kernel_size=3)(inputs)
```

* Операция подвыборки размером 111х111х8
```
x = tf.keras.layers.MaxPool2D()(x)
```

* Преобразование многомерного тензора в одномерный размером 111*111*8 = 98568
 ```
 x = tf.keras.layers.Flatten()(x)
 ```
 
 * Полносвязный Dense слой
```
outputs = tf.keras.layers.Dense(NUM_CLASSES, activation=tf.keras.activations.softmax)(x)
```

 ### Графики обучения для нейронной сети с одним сверточным слоем:
 
Синяя линия - на валидации  
Оранжевая линия - на обучении  

 ***Линейная диаграмма точности:*** 
<img src="./epoch_categorical_accuracy v2.svg">

 ***Линейная диаграмма потерь:*** 
 
<img src="./epoch_loss v1).svg">

### Анализ результатов:

Смотря на графики можно сказать, что наблюдается переобучение, что вызвано отсутстивем нормальный условий и малым размером обучающей выборки. 
