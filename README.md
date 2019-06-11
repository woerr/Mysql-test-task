# Mysql-test-task

### Задание 1.

Ускорит выполнение MySql запросов (Устранить причины их медленного выполнения)
- таблицы находятся в папке [sql](https://github.com/woerr/Mysql-test-task/tree/master/sql):

 ```mysql
 SELECT * FROM isometric i JOIN design_drawings dd ON i.iso_code = dd.iso_number;
 ```
 
 ```mysql
 SELECT dd.iso_code,s.member_id,COUNT(*) FROM design_drawings dd
   LEFT JOIN specfication s ON s.draw_id = dd.id
 GROUP BY dd.iso_code,s.member_id
 ```




### Задание 2.
Создать БД для хранения книг, используя правильную, на Ваш взгляд структуру таблиц. 

Должна быть информация Название, автор, год, кол-во страниц, описание. 

Написать запрос(ы), которые бы выводили статистику по книгам:
 
  1) Общее кол-во книг в базе
  2) Кол-во уникальных авторов в базе
  3) Сколько имеет книг каждый автор.

В ответе должны быть указаны:
- Запросы на создание таблиц(ы) 
- Запросы со статистикой по 3-м пунктам, указанным выше.


### Задание 3.
Ниже приведен список таблиц, с нужной структурой и расшифровкой по каждому полю. Данные можно использовать любые.

- Категории
```mysql
CREATE TABLE `photo_category` (
 `id` int(11) NOT NULL AUTO_INCREMENT,
 `title` varchar(255), -- название
 `is_published` tinyint(1), -- флаг 1/0 - опубликовано/не опубликовано
 `ordi` int(11), -- порядок сорировки, простое число от 1 до ...
 PRIMARY KEY (`id`)
) ENGINE=MyISAM AUTO_INCREMENT=1 DEFAULT CHARSET=utf8
```

- Галереи
```mysql
CREATE TABLE `photo_gallery` (
 `id` int(11) NOT NULL AUTO_INCREMENT,
 `c_id` int(11), -- ID категории 
 `title` varchar(255), -- название
 `is_published` tinyint(1), -- флаг 1/0 - опубликовано/не опубликовано
 `ordi` int(11), -- порядок сорировки, простое число от 1 до ...
 PRIMARY KEY (`id`),
) ENGINE=MyISAM AUTO_INCREMENT=1 DEFAULT CHARSET=utf8
```

- Фотографии
```mysql
CREATE TABLE `photo_image` (
 `id` int(11) NOT NULL AUTO_INCREMENT,
 `g_id` int(11), -- ID галереи
 `title` varchar(255), -- название фотографии
 `is_published` tinyint(1), -- флаг 1/0 - опубликовано/не опубликовано
 `is_main_foto` tinyint(1), -- флаг 1/0 - главная фотография/обычная. 
 `ordi` int(11) DEFAULT NULL, -- порядок сорировки, простое число от 1 до ...
 PRIMARY KEY (`id`),
) ENGINE=MyISAM AUTO_INCREMENT=1 DEFAULT CHARSET=utf8
```


Дано ID категории(Любое).
Нужно написать запрос (один!), который бы получал все галереи этой категории, для каждой из которых получал ID главной фотографии, а если таковой нет — то ID какой-нибудь входящей в категорию (все равно, лишь бы было фото).
