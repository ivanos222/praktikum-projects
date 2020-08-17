# Предсказание коэффициента восстановления золота
## Описание проекта

Есть данные с параметрами химического состава сырья на разных этапах очистки золотой руды. Нужно обучить модель для предсказания коэффициента восстановления золота из золотосодержащей руды. Качество модели опрделеяется метрикой **Итоговый sMAPE**, рассчитывающейся по формуле:

$$
sMAPE_{итоговый} = 25\% \times sMAPE_{rougher} + 75\% \times sMAPE_{final} 
$$

где индексы rougher и final означают этапы обработки руды, для которых расчитывается **sMAPE**.

Показатель **sMAPE** для обоих этапов - rougher и final - рассчитывается по формуле:

$$
sMAPE = {{{1}\over {N}} \sum_{i=1}^N {|{y - \hat y|}\over{(|y| + |\hat y|) / 2}} \times 100\% }
$$

где:  
$ y $ - целевой признак;  
$ \hat y $ - предсказание целевого признака;  
$ N $ - количество объектов.  

Целевым признаком в нашем случае является для обоих этапов является показатель **Recovery** - показатель эффективности обогащения.