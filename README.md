# РАЗРАБОТКА СИСТЕМЫ МАШИННОГО ОБУЧЕНИЯ.
Отчет по лабораторной работе #3 выполнил:
- Колчанов Константин Викторович
- РИ-110949
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |


## Цель работы
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity.

1. Создан новый проект.
![Unity](https://sun9-north.userapi.com/sun9-81/s/v1/ig2/g9iVH3GN3Pxne5Ca3zUs-DoYbE-E2QE6mfFGVMK5R6wybzzzmtcFwz9g7AI-X588AXtXyLLGe-l_JpEWL5LX4KEY.jpg?size=975x587&quality=96&type=album)

2. Последовательно добавлены .json – файлы.
![.json](https://sun9-east.userapi.com/sun9-44/s/v1/ig2/Uz5KrkY6XvHZDBMAE8U_RpSXVIbxoGAc6FBh3n1xBZciX-2_O2hBJSpfD7KaOvXt4qhnVxNAMOGgT3-XcMB9WdC6.jpg?size=796x684&quality=96&type=album)

3. Написана серия команд для создания и активации нового ML-агента, а также для скачивания необходимых библиотек.
![console](https://sun9-north.userapi.com/sun9-80/s/v1/ig2/AhYmp36cMItNKWS9OIREtAuAaTY-Z9EHNPVJjx_1aydgeW5HOY9eirX5LaplTdYNKC4dtlq9MKA7NoAngjFbFgAA.jpg?size=973x504&quality=96&type=album)
![console](https://sun9-west.userapi.com/sun9-8/s/v1/ig2/pRN_rE77ll1TnJT3cDLwTa4KIFpEuXSS-CvfKBXf3ZJ8zfFY4wD-N6E9Wt5_VhCkJPN-oX3GiV14XSP8KpDRFTYR.jpg?size=972x505&quality=96&type=album)
![console](https://sun3.userapi.com/sun3-16/s/v1/ig2/3wkBPyylSALel92Zeul-o5bncokcmr6ee6Gl9CuFWAnLZvlz0tQupFg1SPBey8cmldkCJV4ebUXDvhBtII4cjif3.jpg?size=974x510&quality=96&type=album)

4. Создание на сцене плоскости, куба и сферы, а также настройка павраметров.
![Unity](https://sun9-west.userapi.com/sun9-12/s/v1/ig2/ugqe8HZkaCBigamSMVE9SMT7CNFMCRG84ylzF1mxNsiLqf0_rg90IP0U7CtLqrAcNyiMslATfo_o6XeEaqvhg9fA.jpg?size=1280x680&quality=96&type=album)

5. В корень проекта добавьте файл конфигурации нейронной сети.
![rollerball_config](https://sun9-east.userapi.com/sun9-20/s/v1/ig2/JX0ke02tNGrXkjVvc36oPR8uuAry9COoWBio7TYt3FH3neC_k8qG--u71NZHeXACN7QzuiaXxqBPjOANJJdqLMhs.jpg?size=1117x632&quality=96&type=album)

6. запустите сцену, проверьте работу ML-Agent’a.
![console](https://sun9-east.userapi.com/sun9-73/s/v1/ig2/svE8YZSzxshsUvS0BAQ-YPJjWaY6OGj9OQhhmKamE5ESWzDqi-wIPIF2Ati7fyQC_Y4ALxETQPNTfIh4nvzVOWOF.jpg?size=973x506&quality=96&type=album)

7. Сделайте 3, 9, 27 копий модели «Плоскость-Сфера-Куб».
![Unity](https://sun9-east.userapi.com/sun9-34/s/v1/ig2/iDN-YlQGq_lAuKa8MNRFDoicgFR74IoD7sBiGcmdgAOeGJEOhuWXABQdNVQtR292p1A85gHf8GLxY5Nxjng88kLE.jpg?size=685x492&quality=96&type=album)

8. Сделайте вывод.

За меньшее время достигаются более точные показатели во время обучения нейросети.

## Задание 2
### Подробно опишите каждую строку файла конфигурации нейронной сети. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных сфере. 

trainer_type: ppo - Тип обучения с поощрением

batch_size - Количество опытов на каждой итерации градиентного спуска. Это всегда должно быть в несколько раз меньше, чем buffer_size. Если вы используете непрерывное пространство действий, это значение должно быть большим (порядка 1000). Если вы используете дискретное пространство действий, это значение должно быть меньше (порядка 10 секунд).
 
buffer_size - Количество опыта, который необходимо собрать перед обновлением модели политики. Соответствует тому, сколько опыта должно быть собрано, прежде чем мы приступим к какому-либо изучению или обновлению модели. Это должно быть в несколько раз больше, чем batch_size. Обычно больший размер буфера соответствует более стабильным обновлениям обучения.
 
learning_rate - Начальная скорость обучения для градиентного спуска. Соответствует силе каждого шага обновления градиентного спуска. Обычно это значение следует уменьшить, если тренировка нестабильна, а вознаграждение не увеличивается последовательно.
 
beta - Сила регуляризации энтропии, которая делает политику "более случайной". Это гарантирует, что агенты должным образом исследуют пространство действий во время обучения. Увеличение этого значения обеспечит выполнение большего количества случайных действий. Это должно быть скорректировано таким образом, чтобы энтропия  медленно уменьшалась вместе с увеличением вознаграждения. Если энтропия падает слишком быстро, нужно увеличить бета-версию. Если энтропия падает слишком медленно, уменьшить бета.
  
epsilon - 
Влияет на то, насколько быстро политика может развиваться во время обучения. Соответствует допустимому порогу расхождения между старой и новой политиками при обновлении с градиентным спуском. Установка этого значения небольшим приведет к более стабильным обновлениям, но также замедлит процесс обучения.
  
lambd - Параметр регуляризации (лямбда), используемый при расчете Обобщенной оценки преимущества (GAE). Это можно рассматривать как то, насколько агент полагается на свою текущую оценку стоимости при расчете обновленной оценки стоимости. Низкие значения соответствуют большей зависимости от текущей оценки ценности (что может быть большой погрешностью), а высокие значения соответствуют большей зависимости от фактических вознаграждений, полученных в окружающей среде (что может быть высокой дисперсией). Параметр обеспечивает компромисс между ними, и правильное значение может привести к более стабильному процессу обучения.
  
num_epoch - Количество проходов, которые необходимо выполнить через буфер опыта при выполнении оптимизации градиентного спуска.Чем больше размер пакета, тем больше это допустимо сделать. Уменьшение этого параметра обеспечит более стабильные обновления за счет более медленного обучения.

learning_rate_schedule - Определяет, как скорость обучения меняется с течением времени. 

normalize - Применяется ли нормализация к входным данным векторного наблюдения. Эта нормализация основана на текущем среднем значении и дисперсии векторного наблюдения. Нормализация может быть полезна в случаях со сложными задачами непрерывного управления, но может быть вредна при более простых задачах дискретного управления.

hidden_units - Количество единиц в скрытых слоях нейронной сети. Соответствует количеству единиц в каждом полностью подключенном слое нейронной сети. Для простых задач, где правильным действием является простая комбинация входных данных наблюдения, это должно быть небольшим. Для задач, где действие представляет собой очень сложное взаимодействие между переменными наблюдения, это должно быть больше.
  
num_layers - Количество скрытых слоев в нейронной сети. Соответствует количеству скрытых слоев, присутствующих после ввода наблюдения или после кодирования CNN визуального наблюдения. Для простых задач меньшее количество слоев, скорее всего, будет обучаться быстрее и эффективнее. Для более сложных задач управления может потребоваться больше уровней.
  
gamma - Коэффициент дисконтирования для будущих вознаграждений, поступающих от окружающей среды. Это можно рассматривать как то, насколько далеко в будущем агент должен заботиться о возможных вознаграждениях. В ситуациях, когда агент должен действовать в настоящем, чтобы подготовиться к вознаграждению в отдаленном будущем, это значение должно быть большим. В тех случаях, когда вознаграждение более немедленное, оно может быть меньше. Должно быть строго меньше 1.
  
strength - Фактор, на который можно умножить вознаграждение, получаемое от окружающей среды. Типичные диапазоны будут варьироваться в зависимости от сигнала вознаграждения.

max_steps - максимальное количество проходов

time_horizon - временные рамки 

summary_freq - суммированная частота 

Decision Requester - запрос на принятие решения вызывает CollectObservation, а затем получает последнее действие в OnActionReceived, основанное на этом новом собранном наблюдении. С действиями из TakeActionBetweenDecisions он только снова вызовет OnActionReceived без сбора новых наблюдений и выведет последнее действие, которое он получил от NN.

Behavior Parameters - Параметры поведения — У каждого Агента должно быть определенное поведение. Поведение определяет, как Агент принимает решения. Максимальный шаг — Определяет, сколько шагов моделирования может произойти до окончания эпизода Агента.

## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета.


## Выводы
Игровой баланс — в играх субъективное «равновесие» между персонажами, командами, тактиками игры и другими игровыми объектами.Для создания качественного игрового процесса гейм-дизайнеры обычно настраивают баланс игры итеративно:
1.Выполняют нагрузочный тест тысячами плейтестинговых сессий, в которых участвуют тестеры
2.Учитывают их отзывы и изменяют дизайн игры
3.Повторяют этапы 1 и 2, пока результатом не будут довольны и тестеры, и гейм-дизайнеры
Этот процесс не только занимает много времени, но и неидеален — чем сложнее игра, тем проще незначительным недосмотрам привести к дисбалансу. Когда в играх есть множество различных ролей с десятками взаимосвязанных навыков, всё это сильно усложняет нахождение нужного баланса. При ипользовании системы машинного обучения нейросети время сокращается, а также приводит к более точным, проверенным и необходимым показателям.
