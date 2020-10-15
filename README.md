# implicit-recsys-lightfm

**Data description in russian**

interactions.csv — файл хранит данные по взаимодействию товаров и покупателей. Среди данных есть "холодные" товары и покупатели. В колонке row хранятся идентификаторы покупателя. В колонке col идентификаторы товара. В колонке data - значение взаимодействия.

**_Данные по товарам_**

item_asset.csv - файл хранит качественную характеристику товара. row - идентификатор товара, data - значение характеристики. col - порядковый номер фичи при выгрузке данных (смысла не несет, можно избавиться от этого столбца)

item_price.csv - файл хранит цену товара (уже нормализована). row - идентификатор товара, data - нормализованное значение цены. col - порядковый номер фичи при выгрузке данных (смысла не несет, можно избавиться от этого столбца)

item_subclass.csv - файл хранит значения категорий, к которым относится товар. row - идентификатор товара, col - номер категории, data - признак отношения к категории

**_Данные по пользователям_**

user_age.csv - файл хранит данные по возрасту пользователей. row - идентификатор пользователя, data - значение возраста (уже нормализованное), col - порядковый номер фичи при выгрузке данных (смысла не несет, можно избавиться от этого столбца)

user_region.csv - файл хранит one-hot encoded значения региона пользователя. row - идентификатор пользователя, col - номер one-hot feature региона, data - признак региона.

Task description:

    Task is to recommend 10 items for users
    Metrics is MAP@10
    It's asked to split data in train and test in 80/20

My notes:
    
    For MAP@K order is important but here's no given order so first of all I'll look at mean precision@10
    I'll use split from lightfm.cross_validation module because there're no any info how to do it
    There're cold users and items. They do not impact on quality of metrics on test data. Since task is still to recommend  10 items for users, I'll take the most 10 popular items and recommend them for cold users. This strategy is also justified due to the case that user's features make lightfm be worse and quality of user's feature is quite bad (what I mean will be visible furthere)
    
Also it can be that we'd like to recommend some new items for current users (and new ones) or find similar items for curent ones, etc. but it's not these cases now.

In real case recsys strong depends on business requirements (should we add new items and how, what recommend to new users and why, can cold users or items appear or not, etc) and the best thing to test is A/B
