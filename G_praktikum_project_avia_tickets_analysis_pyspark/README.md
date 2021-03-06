# Аналитика для авиакомпании с помощью PySpark

## Задача
Некая российская авиакомпания, выполняющая внутренние пассажирские перевозки, хочет понять предпочтения пользователей, покупающих билеты на разные направления.

Необходимо изучить спрос пассажиров на рейсы в города, где проходят крупнейшие культурные мероприятия ("фестивали"). Для этого в нашем распоряжении есть БД из пяти связанных между собой таблиц и одной несвязанной. Необходимо сформулировать ряд запросов, импортировать результаты трех запросов в Jupyter Notebook посредством PySpark и произвести анализ. 

Результаты запросов выгружены в .csv. Более подробное описание трех запросов и задач, которые необходимо выполнить с их помощью:
**query_1.csv** — результат первого запроса. В нём содержится такая информация:

- *model* — модель самолета;
- *flights_amount* — количество рейсов для каждой модели самолетов в сентябре 2018 года.

**query_3.csv** — результат третьего запроса. В нём содержится такая информация:

- *city* — город;
- *average_flights* — среднее количество рейсов, прибывающих в город за день в сентябре 2018 года.

 Для этих двух наборов данных нужно проверить типы данных на корректность, вывести топ-10 городов по количеству рейсов, построить графики для моделей самолётов и количества рейсов; городов и количества рейсов; топ-10 городов и количества рейсов; сделать выводы по каждому из графиков.

**query_last.csv** — результат последнего запроса. В нём следующая информация:

- *week_number* — номер недели;
- *ticket_amount* — количество проданных билетов за неделю;
- *festival_week —* проходит ли на этой неделе фестиваль;
- *festival_name —* название фестиваля.

С помощью последнего запроса необходимо __проверить гипотезу: _«Средний спрос на билеты во время фестивалей не отличается от среднего спроса на билеты в обычное время»___.

## Описание 
В начале необходимо было произвести в базе данных ряд запросов, с частью из которых необходимо затем продолжить работу средствами Pyton. Использованные в последствии запросы приведены в тетради.

Далее были задействованы библиотеки *Pandas*, *NumPy*; *PySpark* для работы с запросами на PostgreSQL; *Matplotlib* для визуализации; *scipy.stats* для проверки статистической гипотезы.

Запросы загружены и изучены с помощью *pyspark*.

C помощью *Pandas* и *Matplotlib* визуализированы запрошенные заказчиком разбивки. Обращаем внимание на то, что в сентябре 2018 года более 75% рейсов выполнили самолеты трех моделей: Bombardier CRj-200, Cessna 208 Caravan и Сухой Superjet-100, а также на увеличенный пассажиропоток в Москве. Тем не менее, какие-то весомые выводы о предпочтениях покупателей сделать на основе этого сложно.

Далее проверяется гипотеза. Проводится короткая предобработка с помощью *PySpark* и *NumPy*. Пороговое значение *alpha* задается равным 0.05. Гипотеза проверяется с помощью U-теста Манна-Уитни, подходящего для проверки двух малых выборок. 

В результате теста __гипотеза отвергается__.
