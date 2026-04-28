## Запросы:
### Сафаров
#### 1. Сравнить две вселенные — Marvel и DC — по cредней частоте поялвений персонажей. Найти суммарное кол-во появлений в обеих вселенных и показать максимальные и минимальные кол-во появлений. 

#### 2. Код:
~~~
select universe,sum(appearances),max(appearances),min(appearances),avg(appearances) from superheroes
where universe in ('marvel', 'dc')
group by universe
~~~


### Нягу
#### 1. Выбрать первых 10 супергероев вселенной марвел с черными глазами, у которых номер находится в диапазоне от 100 до 500. Для каждого вывести: id, имя, принадлежность, цвет глаз, волос, кол-во появлений, год появления и вселенную.Сгруппировать по имени и id, отсортировать по году от самого старого к новому.

#### 2. Код:
```
Select id, name, align, eye, hair, appearances, year, universe from superheroes
Where universe = 'marvel' and eye like '%Black%' and id between 100 and 500
group by name, id
order by year asc
limit 10
```
### Губарьков
#### 1. Необходимо составить запрос, который будет выводить сколько хороших персонажей появилось с 1990 по 2013 году и отсортировать по убыванию, ограничив первыми 20

#### 2. Код:
```
Select year, Count(*) as good_count from superheroes
where align like '%Good%' and year between 1990 and 2013
group by year
order by good_count desc
limit 20
```



### Куковский
#### 1. Найди мне 15 злодеев мужского пола из вселенной ДС, которые появлялись чаще всего, но не менее 14 раз (14 включительно), созданные в период с 1965 по 2000 год, имеющие зеленый и синий цвет глаз и различные виды светлых волос.

#### 2. Код:
```
select * from superheroes
where universe like '%dc%' and align like '%Bad%' and appearances >= 14 AND
hair like '%Blond%' and eye in ('Green Eyes', 'Blue Eyes')
and year between 1965 and 2000 and gender like '%Male%'
order by year, appearances desc
limit 15
```


### Яковлева
#### 1. Найди первых 19 самых не популярных по появлению героинь в диапазоне от 454-1812,  без коричневого цвета волос и глаз. Из любой вселенной. Чтобы они были НЕ плохие и НЕ нейтральные.

#### 2. Код: 
```
select * from superheroes
where gender like '%Female%' and appearances between 454 and 1812 and align not in ('Bad Characters', 'Neutral Characters')
group by id,hair,eye
having eye not like '%Brown%' and hair not like '%Brown%'
order by appearances
limit 19
```

 
### Персидский
#### 1. Запрос находит 13 супергероев с самым большим количеством появлений, показывает их  долю от общего числа всех появлений всех героев составляет каждый из них.

#### 2. Код:
```
SELECT id, name, align, appearances, universe, 100.0 * appearances / (Select sum(appearances) from superheroes) as part_of_appear FROM superheroes
Where appearances <= (Select Max(appearances) from superheroes)
limit 13
```

### Цыбулин
#### 1. Найди первых семь супергероев во вселенной Marvel по году их первого появления в комиксах. Для каждого укажи имя, принадлежность (например, хороший, плохой или вообще нейтральный), цвет глаз, их пол и год с псевдонимом год дебюта(появление). Учти, что у всех этих героев должны быть чёрные глаза, а их индефицирующий номер в базе находится в промежутке от 100 до 500. Сгруппируй данные так, чтобы имя героя и его номер шли вместе. Отсортируй итоговый список по возрастанию года — от самого раннего появления к самому позднему.

#### 2. Код:
```
Select id, name, align, eye, gender, year as year_of_appearing, universe from superheroes
where universe like '%marvel%' and eye like '%Black Eyes%' and id between 100 and 500 and gender like '%Male%'
group by id, name
order by year asc
limit 7
```

### Несмашный
#### 1. Выбрать первых 25 супергероев из вселенной марвел с голубыми глазами. Для каждого вывести: минимальное, максимальное и среднее кол-во появлений, пол, цвет глаз и вселенную. Сгруппировать по имени и id.

#### 2. Код:
```
select name,align,eye,gender,universe,min(appearances),max(appearances),avg(appearances) from superheroes
Where universe = 'marvel' and eye like '%Blue%' and gender like '%Male%'
group by name,id
order by name
limit 25
```

### Шнайдер
#### 1. выведи 20 нейтральных женских персонажей блондинок из marvel с голубыми глазами которые появлялись за 1990 по 2010 год отсортируя их по убыванию появлений

#### 2. Код:
```
Select name,align,gender,eye,hair,appearances,year,universe from superheroes
Where universe = 'marvel' and gender like '%Female%' and align like '%Neutral%' and hair like '%Blond%' and eye like '%Blue%' and year between 1990 and 2010
order by appearances desc
limit 20
```

### Сергеев
#### 1. Покажи года, в которых даже самый редко появляющийся женский персонаж всё равно появлялся чаще, чем женские персонажи в среднем по всем годам. Для каждого такого года покажи минимум и максимум появлений

#### 2. Код:
```
🤡🖕
```

### Кривицкий
#### 1. Найди первых 15 супергероев во вселенной marvel по их номеру, который варьируется между 200 и 300, также  по имени, глазам, волосам, появлением, вселеной, дополнительные условия для поиска, у героев голубые глаза, вселеная marvel и светлые волосы, а также сгруппируй имя и номер и отсортируй по волосам.

#### 2. Код:
```
select * from superheroes
Where id between 200 and 300 and eye like '%Blue%' and universe like '%marvel%' and hair like '%Blond%'
group by name,id
order by hair
limit 15
```

### Агарков
#### 1. Вывести имена и мировоззрение супергероев, у которых цвет глаз совпадает с максимальным  значением цвета глаз среди всех записей в таблице, продублировав количество их появлений в двух столбцах с разными заголовками, затем отсортировать список по убыванию количества появлений и ограничить вывод первыми десятью записями.

#### 2. Код:
```

```

### Исроилов
#### 1. Найди первых 15 злодеев из марвел, появившиеся между 1960 и 2000 годах и имеющие черные волосы. Отсортируй их появления по убыванию. Доп условие: показывать только тех, чье появление больше среднего по значению.

#### 2. Код:
```
select * from superheroes
where align like '%Bad%' and universe = 'marvel' and year between 1960 and 2000
group by id,hair
having hair like '%Black%'
order by appearances desc
limit 15
```


### Вагин
#### 1. Найди 10 самых редко появляющихся мужских персонажей в промежутке с 1936 по 2004 годов. Cгруппируй их по вселенным marvel и dc, а также по типу хороший, плохой. Что бы были видны их имена, года, тип персонажа(хороший или плохой), количество появлений, пол, цвет глаз, а также что бы указывалась вселенная(marvel, dc).

#### 2. Код:
```
select name,year,align,appearances,gender,eye,universe from superheroes
where year between 1936 and 2004
and universe = 'dc' or universe = 'marvel' and align = 'Good Characters' or align = 'Bad Characters' and gender like '%Male%'
order by appearances asc
limit 10
```


### Магомедбегов
#### 1. Выведи имена персонажей, их пол, количество появлений и год первого появления. Добавь условие: показывай только тех персонажей, у которых количество появлений больше среднего значения появлений для их пола. Отфильтруй результат: оставь только мужских и женских персонажей, которые появились после 1980 года. Отсортируй список по убыванию количества появлений и покажи первые 10 записей.

#### 2. Код:
```

```


### Бубнив
#### 1. Выведи имена персонажей, цвет их глаз, количество появлений и год первого появления. Добавь условие: показывай только тех персонажей, у которых количество появлений больше среднего значения появлений для персонажей с таким же цветом глаз. Отфильтруй результат: оставь только персонажей с необычными цветами глаз: красные, желтые, золотые, белые или фиолетовые. Исключи тех, у кого цвет глаз не указан или пустой. Отсортируй список по убыванию количества появлений и покажи первые 15 записей.

#### 2. Код:
```

```


### Исмаилов
#### 1. Мне нужна таблица про 7 плохих женских супергероев с наибольшим количеством появлений начиная от самого популярного и заканчивая не популярными, при улсовии что все женские супергерои будут иметь белый цвет волос.  Вдобавок я хочу знать какие герои появились в период с 1950 по  2010 года.

#### 2. Код:
```
select * from superheroes
where gender like '%Female%' and hair like '%White%' and  align like '%Bad%' and year between 1950 and 2010
order by appearances desc
limit 7
```


### Гусейнов
#### 1. Я хочу увидить 10 супергероев которые чаще всего попадались в комиксах по возрастанию, год появлений чтобы был самый поздний, у всех супергероев должны быть карий цвет глаз и цвет волос блонд, персонажи могут быть как хорошие так и плохие.

#### 2. Код:
```
select name, align, eye, hair, year, appearances from superheroes
where eye like '%Brown%' and hair like '%Blond%' and appearances <= (select max(appearances) from superheroes) AND align not like '%Neutral%'
order by year desc
limit 10
```


<!--### Чесноков
#### 1. Найди айди, имя, принадлежность к стороне, глаза (как цвет глаз),  волосы (как цвет волос), пол, появления, год (как год создания) и вселенную из супергероев начиная с 1960 года. Там не должно быть черноволосых, они должны иметь от 100 и более появлений, но не больше 1000 появлений, должны быть женщинами, из DC и не злодеями, отсортируй по году, принадлежности и волосам и ограничься только 25 первыми из них

#### 2. Код:
```
Select id, name, align, eye as eye_color, hair as hair_color, gender, appearances, year as year_of_creation, universe from superheroes
where year >= 1960 and hair not like '%Black%' and appearances between 100 and 1000
group by align, id
having align not like '%Bad%' and universe = 'dc' and gender like '%Female%'
order by year, align, hair 
limit 25
```
-->
