
## Введение

### Слайд 1

Уважаемая комиссия!

Представляю вашему вниманию выпускную квалификационную работу бакалавра на тему: "Решение прямой задачи бокового каротажного зондирования методами численного моделирования".

Актуальность темы обуславливается тем, что
геофизические исследования скважин
электрическими методами используются для
реконструкции пространственного распределения
УЭС, которое связано с нефтенасыщением.

## Постановка задачи

### Слайд 2

Были две задачи:
1. Научиться считать палетки с любыми параметрами (без ограничений времени),
2. Максимально ускорить расчет для оценки возможности решения обратной задачи БКЗ в реальном времени.

Актуальность:
* Задачи электрокаротажа нелинейны, а обратная
задача определения параметров по измерениям
некорректна (неоднозначна). Решение задач в
полных постановках весьма ресурсоемко и плохо
подходит для промышленного применения
* На практике возникает необходимость в палетках с такими параметрами,
которые не опубликованы. Поэтому была поставлена задача разработки метода решения прямой задачи БКЗ, которая позволила бы задавать необходимые
параметры модели для построения палеток
* Краевую задачу в математической постановке прямой задачи БКЗ можно численно решить имеющимися средствами, но это решение не подходит, потому что оно неэффективно, следовательно, не оставалось другого выхода, кроме как придумать свое решение

Математическая постановка.
Излучающий электрод поместим в начало координат и введем обозначение I для силы протекающего через него тока.

Краевая задача, где u -- потенциальное поле, rho -- удельное электрическое сопротивление, дельта -- обобщенная функция дельта-функция Дирака, Omega --- бесконечная область пространства, дельта Omega --- граница области Omega, точки которой находятся на бесконечности.

### Слайд 3

В качестве модельных рассматривались задачи для многослойных осесимметричных моделей системы скважина–пласт: задача рассматривается в цилиндрической системе координат (r, z), где r > 0 — радиальная координата, z — осевая координата, по которой область однородна (единственный однородный пласт бесконечной мощности). В начале координат размещается источник тока силой 1.

На графиках расстояние от центра скважины по оси абсцисс и УЭС среды по оси ординат.

Модель первая -- трёхслойная осесимметричная модель с зоной проникновения.
Изображены в порядке возрастания радиальной координаты зона скважины, зона проникновения, зона пласта.

Модель вторая -- четырехслойная осесимметричная модель с промытой зоной с анизотропией пласта.
Изображены зона скважины, промытая зона, переходная зона, зона пласта.

## Способ решения

### Слайд 4

Инструменты:
* Язык программирования Python c программными пакетами для параллельных вычислений
и интерфейсами для модулей triangle и FEniCS.
* FEniCS — популярная вычислительная платформа с открытым исходным
кодом (LGPLv3) для решения уравнений в частных производных (ДУЧП). Основано на методе конечных элеметнов
* Библиотека для триангуляции triangle
* Компьютер: операционная система Ubuntu (18.04 LTS), процессор (Intel Pentium 4415U 2.30 ГГц) с 4 логическими процессорами (1 физический процессор × 2 ядра в физическом процессоре × 2 потока в каждом ядре)

### Слайд 5

Построение расчетной сетки с заданием узлов и графа для триангуляции расчетной области с помощью библиотеки triangle.

Подбиралась расчетная сетка из комбинаций вариантов пунктов:
* Варианты регулярных расположений узлов на расчетной области из комбинаций параметров:
  * кол-во лучей, исходящих из начала координат в расчетной области, равноотстоящие по углу, на которых лежат узлы;
  * варианты регулярных расположений узлов, лежащих на лучах

* Варианты графов, с отрезками которых стороны треугольников триангуляции не пересекаются

* Варианты расположения узлов на границах зон

* Включение дополнительных узлов при триангуляции

Решение методом конечных элементов на расчетной сетке с лагранжевыми конечными элементами.
  * различные степени полинома лагранжевых конечных элементов

### Слайд 6

Оптимальное решение получено со следующей схемой численного решения:
* лучи, исходящие из начала координат в расчетной области, равноотстоящие по углу
* узлы на лучах, равноотстоящие в логарифмическом масштабе;
* вторая степень полинома лагранжевых элементов
* узлы на пересечениях границ зон с лучами, исходящие из начала координат, и концентрическими окружностями, значения радиусов которых равноотстоящие в логарифмическом масштабе, с центрами в начале координат в расчетной области

Изображена расчетная сетка для второй модели в двух масштабах.

## Результаты

### Слайд 7

Табличных данных по БКЗ для сравнения нет, есть только палетки. Поэтому и сравнивали известные и расчетные палетки моделей.

На графиках длина градиент-зонда по оси абсцисс, кажущееся сопротивление зонда по оси ординат.

Рассчитано 151 точек, расположенные от 10^-1 до 10^3 с логарифмическим шагом 10^(1/30).

21 расчетных кривых в палетке первой модели, 15 кривых -- вторая модель.

## Анализ результатов

### Слайд 8

Указаны оценки времени расчета --
наименьшее время из 7 выборок времен расчета,
кол-ва узлов расчетной сетки моделей.

Расчетное время для первой модели больше, чем для второй, потому что в расчетной палетке для первой модели больше расчетных кривых.

В данном случае мы следили за двумя параметрами: гладкостью
решения и сравнением ”на глаз” с известной палеткой. Поскольку принятая
методика решения обратной задачи БКЗ основано на использованием палеток
на ”сравнении на глаз”, то такой критерий годится.

## Заключение

### Слайд 9

* Освоены пакеты программ для параллельных вычислений: вычислительная платформа для автоматического решения ДУЧП FEniCS,  для векторных вычислений Numpy
* Разработаны прототипы программ для численного решения прямой задачи БКЗ для двух известных моделей прискважинной зоны
* Сравнены расчетная и известная палетки. Наблюдается совпадение, означает, что способ решения верный и точный
* Показана применимость метода решения прямой задачи БКЗ с приемлимой точностью

## Возможные вопросы

***Почему решение краевой задачи в математической постановке
прямой задачи БКЗ неэффективно уже имеющимися
средствами?***

В данной задаче возникают затруднения,
связанные с тем, что искомый потенциал поля имеет особенность (уходит на
бесконечность) в окрестности источника тока. Это приводит к необходимости
сгущения расчётной сетки в этой окрестности, но сильное сгущение приводит
к чрезмерному росту числа узлов сетки и, как следствие, сильному росту
времени, требуемому на решение. Имеющиеся средства не учитывают данную вещь, поэтому форма расчетной сетки не оптимальна, следовательно необходимо большее кол-во узлов для расчета, следовательно большее время расчета.

***Почему минимальное из 7 выборок?***

Заманчивая идея рассчитать среднее и стандартное отклонение от вектора результатов времени вычисления и сообщить о них. Однако это не очень полезно. В типичном случае самое меньшее значение дает нижнюю границу для того, насколько быстро компьютер может выполнить данный фрагмент кода; Более высокие значения в векторе результатов, как правило, вызваны не изменчивостью скорости исполнения кода на Python, а другими процессами, запущенные в операционной системе, влияющими на точность отсчета. Так что меньшее значение, вероятно, единственное число, которое должно заинтересовать. После этого следует смотреть на весь вектор и применять здравый смысл, а не статистику.
