# Тестування векторні представлень слів та інших текстових об'єктів

Даний репозиторій містить скріпти, вхідні та вихідні дані для тестування моделей векторних представлень слів натренованих на україномовних корпусах


## Вхідні дані

`test/test_vocabulary.txt` - словарний тест, підготовлений Тетяною Кодлюк

`http://lang.org.ua/corpora/` - корпуси україномовних текстів

`http://lang.org.ua/models/` - word embeddings models

## Вихідні дані

`results/Models_scores.csv` - результати тестування моделей, де вибрани числова метрика - Accuracy

# Опис алгоритму

Простим способом оцінити модель векторних представлень тексту є безпосереднє використання цих моделей для передбачення синтаксичних та семантичних відношень між словами. Наприклад

`король відноситься до королеви як батько до ...` (матері)

 `Лондон відноситься до Англії як Рим до ...` (Італії)

`стрункий відноситься до стрункіший як бідний до ...` (бідніший)

Цей підхід називають методом Аналогічного міркування. Його запровадив Т. Міколов з його колегами. 

Підготовлений нами словник з 23971 запитань містить 12 основних тематик, які представленні такими відношеннями

теперішній час до минулого

країна до національності

країна до столиці

країна до національної валюти

країна до регіону

однина до множини

дієслово до іменника

прикметник до прислівника

ступені порівняння прикметників (1 та 2)

антоніми

родинні зв'язки

Модель тестується по кожній тематиці окремо, а також по всіх загалом (all)

Відповідь вважається правильною, якщо вона зустрічається в перших `n` словах (по замовчуванні n = 4)

Слова з деяких запитань можуть бути відсутні у словнику моделі, тому розраховано два види Accuracy:

`Accuracy1 = відношення числа правильних відповідень, до загального числа запитань, які присутні у словнику моделі`

`Accuracy2 = відношення числа правильних відповідень, до загального числа запитань`

За результатами тестування, які відображені в `results/Models_scores.csv` можна вибрати найбільш оптимальну модель до вашого типу задач. Якщо тематика запитань не впливає на ваше дослідження, пропонуємо відфільтрувати таблиці по полі `Type_of_question = all`, та порівняти результати моделей відносно усіх запитань. 

Даний скріпт `Models_evaluation.py` можна використовувати для тестування власноруч створений моделей. Для цього достатьо запустити його командою:

`python Models_evaluation.py <path_to_models_folder> <vocabulary.txt> n output_file`








