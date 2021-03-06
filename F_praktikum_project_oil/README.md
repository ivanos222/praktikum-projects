# Выбор региона для разработки нефтяных месторождений на основе прогнозирования дохода

## Задача
Даны пробы нефти в трёх регионах, где измерили качество нефти и объём её запасов. Необходимо построить модель машинного обучения, которая поможет определить регион, где добыча принесёт наибольшую прибыль; кроме этого необходимо оценить возможную прибыль и риски. 

Шаги для выбора локации:

- В избранном регионе ищут месторождения, для каждого определяют значения признаков;
- Строят модель и оценивают объём запасов;
- Выбирают месторождения с самым высокими оценками значений. Количество месторождений зависит от бюджета компании и стоимости разработки одной скважины;
- Прибыль равна суммарной прибыли отобранных месторождений.

## Описание проекта
В ходе проекта использовались:
- библиотеки *Pandas* и *Numpy*;
- библиотека *scikit-learn*: *linear_regression* - алгоритм; *mean_squared_error*, *mean_absolute_error* - метрики; *StandardScaler* - для масштабирования; *train_test_split* - для деления на выборки;
- *scipy.stats* для определения процентиля заданной величины в множестве;
- *matplotlib.pyplot* и *seaborn* для визуализации;

Регионы были проименованы, данные загружены и рассмотрены. Данные каждого региона были поделены на обучающие и валидационные выборки в отношении 75:25 (это было требование заказчика), Для каждого из регионов А, B, C была создана модель линейной регрессии, каждая из которых сделала предсказание запасов нефти для скважин в регионе, от которых было взято среднее. Качество предсказаний для каждого региона были оценены, средние значения проанализированы. Вывод: в месторождении B средний запас нефти ниже, чем в A и C, но качество предсказание модели для региона B, в отличие от двух других моделей, высокое.

Затем была произведена подготовка к расчету прибыли: сохранены в качестве переменных полученные от заказчика важные данные о бюджете, стоимости скважины, стоимости барреля, количество разведывательных проб и т.д. Была определена функция расчета прибыли.

После этого был произведен расчет прибыли и рисков. Была определена функция для бутстреппинга, которая принимает на вход уникальные для каждого региона модели и массивы с данными обо всех месторождениях в регионе (признаки и целевой признак), а также количество генерируемых подвыборок (в данном проекте по просьбе заказчика - 1000), и которая выдает распределение вариантов ожидаемой прибыли в виде pd.Series, среднюю ожидаемую прибыль, нижнюю и верхнюю границы доверительного интервала значений ожидаемой прибыли и риск убытков, рассчитанный с помощью *scipy.stats.percentileofscore*. 

Для данных по каждому региону была применена эта функция. Результаты по каждому региону были сведены в таблицу. Кроме того, все результаты, кроме риска убытков (который для каждого региона одинаков и равен нулю), то есть доверительные интервалы и средняя ожидаемая прибыль, были изображены на графиках распределения потенциальной прибыли для каждого региона.

По результатам исследования, моделирования и расчета к разработке рекомендован регион А. 
