# Проект на тему: "Heritage statistics"
## Применение в задачах культурологии: ##
С помощью применения в моем проекте библиотеки Pandas я могу расширить возможности поисковой базы минкульта РФ и найти в базе объектов культурного наследия РФ:
а) объекты конкретного региона с созданием таблицы по требуемым позициям;
б) расширить возможности поиска по базе данных (популярность и частота, дата создания, сортировка по убыванию/возрастанию, количество конкретного типа объекта в регионе) что поможет мне в моей исследовательской работе, связанной с ОКН


### БИБЛИОТЕКА PANDAS ###
Pandas — это библиотека Python для обработки и анализа структурированных данных, её название происходит от «panel data» («панельные данные»). Панельными данными называют информацию, полученную в результате исследований и структурированную в виде таблиц. Для работы с такими массивами данных и создан Pandas.
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/ohPUaT8CRuenSFQO2GP4_Screen%20Shot%202017-09-20%20at%209.01.09%20AM.png)


### ПРИМЕР РАБОТЫ КОДА (c данными о смертности людей от разных причин по 204 странам с 2000 по 2019 гг с сайта)  ###
## Ссылка на тетраль с результатми работы кода: [тут](https://colab.research.google.com/drive/1UqIDkUsdg0aYzTCIoiGF0UTJqpOAvQOP#scrollTo=kITJLWJ1mfbZ) ##


## 1.загрузка библиотеки Pandas ##
```
import pandas as pd 
`````
создание датафрейма из словаря
```
dict_city = {"City" : ["Moscow", "Saint-Petersburg", "Novosibirsk"], 
            "Population" : [12678079,   5398064,  1625631]}
df = pd.DataFrame(dict_city)
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/1.png)

сохранение датафрейма на компьютер в формате xlsx
```
df.to_excel("cities.xlsx")
`````
создание датафрейма из списка списков
```
lists_city = [["Moscow", "Saint-Petersburg", "Novosibirsk"], 
[12678079,   5398064,  1625631]]

pd.DataFrame(lists_city)
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/2.png)

транспонирование (меням столбцы и строки местами)
```
pd.DataFrame(lists_city).T
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/3.png)

создание датафрейма из файла 
в кавычках нужно прописать путь к файлу на своем компьютере
его можно скачать по ссылке https://drive.google.com/file/d/16fM_JEC5GAkYEDaDgzROrBm8loi9RZRZ/view 
в файле данные о смертности людей от разных причин по 204 странам с 2000 по 2019 гг с сайта 
http://ghdx.healthdata.org/gbd-results-tool
```
df = pd.read_csv("/Users/sherlock/Downloads/IHME-GBD_2019_DATA-ff08d9bc-1/IHME-GBD_2019_DATA-ff08d9bc-1.csv", encoding = "utf-8") 
`````
первые 5 строк датафрейма
```
df.head()
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/4.png)

первые 15 строк датафрейма
```
df.head(8)
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/5.png)

последние 5 строк датафрейма
```
df.tail()
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/6.png)

информация о датафрейме
```
df.info() 

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 257040 entries, 0 to 257039
Data columns (total 10 columns):
 #   Column    Non-Null Count   Dtype  
---  ------    --------------   -----  
 0   measure   257040 non-null  object 
 1   location  257040 non-null  object 
 2   sex       257040 non-null  object 
 3   age       257040 non-null  object 
 4   cause     257040 non-null  object 
 5   metric    257040 non-null  object 
 6   year      257040 non-null  int64  
 7   val       257040 non-null  float64
 8   upper     257040 non-null  float64
 9   lower     257040 non-null  float64
dtypes: float64(3), int64(1), object(6)
memory usage: 19.6+ MB
`````
показывает, сколько в датафрейме строк и столбцов
```
df.shape

(257040, 10)
`````
статистическая информация по столбцам (уникальные значения, среднее, стандартное отклонение, минимальное, квартили, максимальное)
```
df.describe() 
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/7.png)

статистика включает не только числовые столбцы, но и строки 
(unique - сколько уникальных значений, top - какое самое популярное значение, freq - как часто встречается самое популярное) 
```
df.describe(include = 'all')
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/8.png)

удаление пустых значений (missing values, NA)
```
df.dropna(inplace=True)
`````
выбор столбца, способ 1
```
df["measure"]


0         Deaths
1         Deaths
2         Deaths
3         Deaths
4         Deaths
           ...  
257035    Deaths
257036    Deaths
257037    Deaths
257038    Deaths
257039    Deaths
Name: measure, Length: 257040, dtype: object
`````
выбор столбца, способ 2
```
df.measure


0         Deaths
1         Deaths
2         Deaths
3         Deaths
4         Deaths
           ...  
257035    Deaths
257036    Deaths
257037    Deaths
257038    Deaths
257039    Deaths
Name: measure, Length: 257040, dtype: object
`````
выбор сразу нескольких столбцов
```
df[["location","sex","year"]]
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/9.png)

выбирает все строки, а столбцы от "location" до "val"
```
df.loc[:, "location":"val"]
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/10.png)

выбирает строки от 100 до 110 (правый край, то есть число 110, в методе iloc включается), столбцы от "location" до "val"
```
df.loc[100:110, "location":"val"] 
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/11.png)

выбирает только те строки в столбце "sex", где указаны оба пола ("Both")
```
df[df["sex"] == "Both"] 
`````
несколько условий сразу
```
df[(df["sex"] == "Both") & (df["cause"] == "Cardiovascular diseases") & (df["year"] == 2019)]
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/12%20!!.png)

сортирует датафрейм по столбцу "val", ascending означает по возрастанию, ascending = False - по убыванию
```
cardio.sort_values(by = ["val"], ascending=False, inplace=False, na_position='last', ignore_index=False)
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/13.png)

ищет строки, где либо Russia, либо Russian Federation (соблюдается одно из условий)
```
df[(df["location"] == "Russia") | (df["location"] == "Russian Federation")] 
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/14.png)

строки содержат упоминание HIV (ВИЧ)
```
df[df["cause"].str.contains("HIV")]
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/15.png)

строки НЕ содержат упоминание ВИЧ
```
df[df["cause"].str.contains("HIV") == False]
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/16.png)

удаляет столбец measure
```
df.drop("measure", axis=1, inplace = True)
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/1000.png)
создает новый столбец, в котором будут округленные значения из столбца val

удаляет столбцы metric, age, upper, lower
```
df.drop(["metric","age","upper","lower"], axis=1, inplace = True)
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/17.png)
создает новый столбец, в котором будут округленные значения из столбца val
```
df["val_round"] = df["val"].round(decimals = 1) 
`````
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/18.png)

меняет название столбца
```
df.rename(columns = {"val": "value"}, inplace = True)
`````
сохранение датафрейма в csv на компьютер
```
df.to_csv("deaths_2000-2019.csv")
`````

ССЫЛКА НА ТЕТРАДЬ С РЕЗУЛЬТАТАМИ РАБОТЫ КОДА: [тут](https://colab.research.google.com/drive/1UqIDkUsdg0aYzTCIoiGF0UTJqpOAvQOP#scrollTo=kITJLWJ1mfbZ)

### Как работать с библиотекой pandas в моем проекте? ###
Загружаем библиотеку:
```
{import pandas as pd}
```

Загружаем базу данных реестр объектов культурного наследия РФ :
```
from google.colab import drive
drive.mount('/content/gdrive', force_remount=True)

df = pd.read_csv("/content/gdrive/MyDrive/data-50-structure-6.csv.zip")
```

В базе делаем выборку по только нужным нам параметрам (объект,регион,категория,дата,вид):
```
heritage = df[["Объект","Регион","Категория историко-культурного значения","дата создания","Вид объекта"]] 
heritage
```

Дальше оставляем в таблице только интересующую нас Ярославскую область :
```
heritage[heritage["Регион"] == "Ярославская область"]
```

```
yar = heritage[heritage["Регион"] == "Ярославская область"]
yar
```

Теперь исследуем только тип объекта церкви и только регионального значения в Яр области: 
```
yar[(yar["Регион"] == "Ярославская область") & (yar["Объект"] == "Церковь") & (yar["Категория историко-культурного значения"] == "Регионального значения")]
```
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-10-21%20%D0%B2%202.40.16.png)

Также с помощью пандас можем узнать самый популярный объект в Яр области - это тип Селище тип Федерального значения, оно встречается 127 раз 
```
yar.describe(include = 'all')
```
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/top%20seliche.png)

Мы можем вывести все памятники которые были созданы после конкретного года 
```
yar[(yar["дата создания"] >= "1501")]
```
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/1501.png)

Сортируем даты создания по убыванию с помощью 
ascending = False 
```

yar.sort_values(by = ["дата создания"], ascending=False, inplace=False, na_position='last', ignore_index=False)
```
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/%D1%83%D0%B1%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5.png)

Узнаем сколько каждого объекта есть в регионе 
с помощью :
```
yar['Объект'].value_counts()
```
![здесь будет картинка](https://github.com/mshnktn/heritage-statictics/blob/main/%D1%8E%D0%BD%D0%B8%D0%BA.png)

ССЫЛКА НА КОД: [тут](https://colab.research.google.com/drive/1E1Lb2WRMMC2EX6InEjfMbIKw2CgH79I-?usp=sharing)

# **Анализ результатов и выводы:** #

## Благодаря пандас я узнала/создала: ##

1.Самый популярный вид объекта наследия в выбранном регионе; 2.Частоту встречаемости каждого объекта в регионе 3.Таблицу только с нужными мне колонками 4.Всем этим расширила функционал поисковой системы по данной базе мин культа РФ. Найденные данные имеют полезность в моём исследовании "Актуализация историко-культурного наследия Ярославской области в современных культурных практиках", большая часть которой уделяется датировке, видам и популярности ОКН. 

