---
# Front matter
title: "Отчёт по лабораторной работе №2"
subtitle: "Шифры перестановки"
author: "Гердт Ольга НФИмд-02-21"

# Generic otions
lang: ru-RU
toc-title: "Содержание"

# Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

# Pdf output format
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
### Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Misc options
indent: true
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучение алгоритмов маршрутной перестановки, решеток и Виженера. И создание программ для их реализации.

# Теоретические сведения

## Шифр маршрутной перестановки

Широкое распространение получили шифры перестановки, использующие  некоторую геометрическую фигуру. Преобразования из этого шифра состоят в том, что в фигуру исходный текст вписывается по ходу одного «маршрута», а затем по ходу другого выписывается с нее. Такой шифр называют **маршрутной перестановкой**.

Например, можно вписывать исходное сообщение в прямоугольную  таблицу, выбрав такой маршрут: по горизонтали, начиная с левого верхнего угла поочередно слева направо и справа налево. Выписывать же сообщение  будем по другому маршруту: по вертикали, начиная с верхнего правого угла и двигаясь поочередно сверху вниз и снизу вверх

Зашифруем, например, указанным способом фразу: 

ПРИМЕРМАРШРУТНОЙПЕРЕСТАНОВКИ

используя прямоугольник размера 7х4: 

П | Р | И | М | Е | Р | М
:-:|:-:|:-:|:-:|:-:|:-:|:-:
  Н   |  Т   |  У   |  Р   |  Ш   |  Р   |  А   
О | Й | П | Е | Р | Е | С 
И | К | В | О | Н | А | Т 

Зашифрованная фраза выглядит так: 

МАСТАЕРРЕШРНОЕРМИУПВКЙТРПНОИ

Теоретически маршруты могут быть значительно более изощренными,  однако запутанность маршрутов усложняет использование таких шифров. 

## Шифр Кардано

Часто так бывает, что талантливый человек входит в историю как автор  какого-то одного открытия, а прочие его заслуги при этом остаются в  тени. Наверное, то же самое можно сказать про Джероламо Кардано.

Даже если вы не разбираетесь в автомобилестроении, то наверняка  слышали о каком-то карданном вале. Это такая деталь, которая передает  крутящий момент от коробки передач или раздаточной коробки к редуктору  переднего или заднего моста. Джероламо придумал этот шарнирный механизм, но, помимо “автомобильного” изобретения, у Кардано было много других  блестящих идей, например о пользе переливания крови. Еще одно  изобретение Кардано — шифрование по трафарету или решетке.

![рис 1](image/01.png "расшифровка по трафарету")

> **Текст записки:** 
>  Сэр Джон высоко ценит Вас и снова повторяет,  что все, что доступно ему, теперь ваше, навсегда. Может ли он заслужить  прощение за свои прежние промедления посредством своего обаяния. 
>  **Шифрованное послание:** 
>  В мае Испания направит свои корабли на войну.

Решетка Кардано может быть двух видов — простая и  симметрично-поворотная. В первом случае для шифрования применяется  трафарет с отверстиями, через которые "фильтруется" полезный текст.  Другой вариант решетки, более интересный, состоит в том, чтобы  использовать симметричный (квадратный) трафарет, который можно применять несколько раз, просто поворачивая его вокруг центра. Поворотная решетка Кардано позволяет записать текст массивом символов так, что результат  будет выглядеть совершенно нечитаемым.

![рис 2](image/02.jpg " решетка Кардано")

Решетка Кардано была очень практичной и удобной. Чтобы прочитать  секретный текст, не нужно было "решать кроссворд" или тратить время на  обучение секретному языку. Этим шифром предпочитали пользоваться многие  известные личности, например кардинал Ришелье и русский драматург и  дипломат Александр Грибоедов.

Таблица накладывается на носитель, и в вырезанные ячейки вписываются буквы, составляющие сообщение. После переворачивания таблицы вдоль вертикальной оси, процесс вписывания букв повторяется. Затем то же самое происходит после переворачивания вдоль горизонтальной и снова вдоль вертикальной осей.

В частном случае квадратной таблицы, для получения новых позиций для вписывания букв, можно поворачивать квадрат на четверть оборота.

Чтобы прочитать закодированное сообщение, необходимо наложить решётку Кардано нужное число раз на закодированный текст и прочитать буквы, расположенные в вырезанных ячейках.

Такой способ шифрования сообщения был предложен математиком Джероламо Кардано в 1550 году, за что и получил своё название.

## Шифр Виженера

Шифр Виженера (фр. Chiffre de Vigenère) — метод полиалфавитного шифрования буквенного текста с использованием ключевого слова.

Интересно, что человек, давший имя этому шифру, никакого отношения к  нему не имел. На самом деле его автором был итальянский математик  Джованни Батиста Беллазо. Его труды и изучил Блез де Виженер во время  своей двухлетней дипломатической миссии в Риме. Вникнув в простой, но  эффективный принцип шифрования, дипломат сумел преподнести эту идею,  показав ее комиссии Генриха III во Франции.

Суть нового принципа шифрования заключалась в том, что величина  сдвига для замещения букв была переменной и определялась ключевым словом или фразой. Долгое время этот метод считался неуязвимым для  разгадывания, и даже авторитеты в области математики признавали его  надежность. Так, легендарный автор приключений “Алисы в зазеркалье” и  “Алисы в стране чудес”, писатель-математик Льюис Кэрролл в своей статье  «Алфавитный шифр» прямо и категорично называет шифр Виженера  “невзламываемым”. Эта статья вышла в детском журнале в 1868 году, но  даже спустя полвека после статьи Чарльза Латуиджа Доджсона (это  настоящее имя автора сказок про Алису) научно-популярный американский  журнал Scientific American продолжал утверждать, что шифр Виженера  невозможно взломать.

Для расшифровки шифра Виженера использовалась специальная таблица, которая называлась tabula recta.

![рис 3](image/03.png "tabula recta для латинского алфавита")

> Квадрат Виженера, или таблица Виженера, также известная как tabula  recta, может быть использована для шифрования и расшифровывания.

В шифре Цезаря каждая буква алфавита сдвигается на несколько позиций; например в шифре Цезаря при сдвиге +3, A стало бы D, B стало бы E и так далее. Шифр  Виженера состоит из последовательности нескольких шифров Цезаря с  различными значениями сдвига. Для зашифровывания может использоваться  таблица алфавитов, называемая tabula recta или квадрат (таблица)  Виженера. Применительно к латинскому алфавиту таблица Виженера  составляется из строк по 26 символов, причём каждая следующая строка  сдвигается на несколько позиций. Таким образом, в таблице получается 26  различных шифров Цезаря. На каждом этапе шифрования используются  различные алфавиты, выбираемые в зависимости от символа ключевого слова. Например, предположим, что исходный текст имеет такой вид:

```
ATTACKATDAWN
```

Человек, посылающий сообщение, записывает ключевое слово («`LEMON`») циклически до тех пор, пока его длина не будет соответствовать длине исходного текста:

```
LEMONLEMONLE
```

Первый символ исходного текста («A») зашифрован последовательностью  L, которая является первым символом ключа. Первый символ зашифрованного  текста («L») находится на пересечении строки L и столбца A в таблице  Виженера. Точно так же для второго символа исходного текста используется второй символ ключа; то есть второй символ зашифрованного текста («X»)  получается на пересечении строки E и столбца T. Остальная часть  исходного текста шифруется подобным способом.

```
Исходный текст:       ATTACKATDAWN
Ключ:                 LEMONLEMONLE
Зашифрованный текст:  LXFOPVEFRNHR
```

# Выполнение работы

## Реализация шифра маршрутной перестановки на языке Python

```
# задание 1. Маршрутное шифрование.
def marhsrutshifr():
    text = input("Ввведите текст: ").replace(' ', '')
    print("Длина текста без пробелов: ", len(text))
    n = int(input("Введите число столбцов n "))
    m = int(input("Введите число строк m "))
    parol = input("Введите слово-пароль: ")
    lists = [['a' for i in range(0, n)] for j in range(m)]
    it = 0
    for i in range(m):
        for j in range(n):
            if it < len(text):
                lists[i][j] = text[it]
                it += 1
    lis = list()
    for i in range(n):
        lis.append(parol[i])
    lists.append(lis)
    prrint(lists)
    result = ""
    spisok = sorted(lists[len(lists) - 1])
    for i in spisok:
        print(i, " = ", lists[len(lists)-1].index(i))
        for j in range(len(lists)):
            if j==len(lists)-1:
                continue
            result += lists[j][lists[len(lists)-1].index(i)]
    print(result)
```

## Реализация шифра решеткой на языке Python

```
# функция для поворота матрицы
def rot90(matrix):
    return[list(reversed(col)) for col in zip(*matrix)]

# функция удаления чисел из матрицы
def udalenie(largelist, inn, k):
    for i in range(k * 2):
        for j in range(k * 2):
            if largelist[i][j] == inn:
                largelist[i][j] = " "
                return

# задание 1. Шифр Кардано
def cardangrille():
    k = int(input("Введите число k: "))
    s=1
    lists = [[i for i in range(k)] for i in range(k)]
    for i in range(k):
        for j in range(k):
            lists[i][j] = s
            s += 1
    print(lists)
    lists1 = rot90(lists)
    lists2 = rot90(lists1)
    lists3 = rot90(lists2)
    largelist = [[1 for i in range(2*k)] for i in range(2*k)]
    for i in range(k):
        for j in range(k):
            largelist[i][j] = lists[i][j]
    i1 = 0
    j1 = 0
    for i in range(0, k):
        for j in range(k, k*2):
            largelist[i][j] = lists1[i1][j1]
            j1 += 1
        j1 = 0
        i1 += 1
    i1 = 0
    j1 = 0
    for i in range(k, k*2):
        for j in range(k, k * 2):
            largelist[i][j] = lists2[i1][j1]
            j1 += 1
        j1 = 0
        i1 += 1
    i1 = 0
    j1 = 0
    for i in range(k, k * 2):
        for j in range(0, k):
            largelist[i][j] = lists3[i1][j1]
            j1 += 1
        j1 = 0
        i1 += 1
    prrint(largelist)
    text = "криптографиянаукаозащитеинформации"
    largelist_a = [[" " for i in range(2*k)] for i in range(2*k)]
    s = 0
    li = [i for i in range(1,k**2+1)]
    for inn in li:
        udalenie(largelist, inn, k)
    ind = 0
    
    for i in range(k * 2):
        for j in range(k * 2):
            if largelist[i][j] == largelist_a[i][j] and len(text) > 0:
                largelist_a[i][j] = text[0]
                text = text[1:]
    largelist = rot90(largelist)
    for i in range(k * 2):
        for j in range(k * 2):
            if largelist[i][j] == largelist_a[i][j] and len(text) > 0:
                largelist_a[i][j] = text[0]
                text = text[1:]
    if len(text) > 0:
        largelist = rot90(largelist)
        for i in range(k * 2):
            for j in range(k * 2):
                if largelist[i][j] == largelist_a[i][j] and len(text) > 0:
                    largelist_a[i][j] = text[0]
                    text = text[1:]
    if len(text) > 0:
        largelist = rot90(largelist)
        for i in range(k * 2):
            for j in range(k * 2):
                if largelist[i][j] == largelist_a[i][j] and len(text) > 0:
                    largelist_a[i][j] = text[0]
                    text = text[1:]
    prrint(largelist_a)
    stri = input("Введите пароль: ")
    
    if len(stri) > k*2:
        stri = stri[:k*2]
    elif len(stri) < k*2:
        while len(stri) != k*2:
            stri += "я"
    largelist_a.append(list(stri))
    prrint(largelist_a)
    result = ""

    spisok = sorted(largelist_a[len(largelist_a) - 1])
    for i in spisok:
        print(i, " = ", largelist_a[len(largelist_a) - 1].index(i))
        for j in range(len(largelist_a)):
            if j==len(largelist_a)-1:
                continue
            result += largelist_a[j][largelist_a[len(largelist_a) - 1].index(i)]
    print(result.replace(" ", ""))
```

## Реализация шифра Виженера на языке Python

```
# задание 1. Шифр Вижинер
def form_dict():
    d = {}
    iter = 0
    for i in range(0,127):
        d[iter] = chr(i)
        iter = iter +1
    return d

def encode_val(word):
    list_code = []
    lent = len(word)
    d = form_dict()

    for w in range(lent):
        for value in d:
            if word[w] == d[value]:
               list_code.append(value)
    return list_code

def comparator(value, key):
    len_key = len(key)
    dic = {}
    iter = 0
    full = 0

    for i in value:
        dic[full] = [i,key[iter]]
        full = full + 1
        iter = iter +1
        if (iter >= len_key):
            iter = 0
    return dic


def full_encode(value, key):
    dic = comparator(value, key)
    print('Compare full encode', dic, "\n")
    lis = []
    d = form_dict()

    for v in dic:
        go = (dic[v][0]+dic[v][1]) % len(d)
        lis.append(go)
    return lis


def decode_val(list_in):
    list_code = []
    lent = len(list_in)
    d = form_dict()

    for i in range(lent):
        for value in d:
            if list_in[i] == value:
               list_code.append(d[value])
    return list_code

def full_decode(value, key):
    dic = comparator(value, key)
    print('Deshifre=', dic,)
    d = form_dict()
    lis =[]

    for v in dic:
        go = (dic[v][0]-dic[v][1]+len(d)) % len(d)
        lis.append(go)
    return lis

def vijer():
    word = "Hello world"
    key = "key"
    print("Слово: ", word)
    print("Ключ: ", key, "\n")
    key_encoded = encode_val(key)
    value_encoded = encode_val(word)
 
    print("Value= ",value_encoded)
    print("Key= ", key_encoded)

    shifre = full_encode(value_encoded, key_encoded)
    print("Шифр= ", "".join(decode_val(shifre)),  "\n")

    decoded = full_decode(shifre, key_encoded)
    print("Decode list=", decoded, "\n")
    decode_word_list = decode_val(decoded)
    print("Дешифровка= ","".join(decode_word_list))

```

## Контрольный пример

![Работа алгоритма маршрутной перестановки](image/04.png "Работа алгоритма маршрутной перестановки"){ #fig:001 width=70% height=70%}

![Работа алгоритма решетки](image/05.png "Работа алгоритма решетки"){ #fig:002 width=70% height=70%}

![Работа алгоритма Виженера](image/06.png "Работа алгоритма Виженера"){ #fig:003 width=70% height=70%}

# Выводы

Составлены программы шифрования с использованием алгоритмов:

* маршрутное шифрование
* шифрование с помощью решеток
* таблица Вижнера

# Список литературы{.unnumbered}

1. [Маршрутная перестановка](https://science.wikia.org/ru/wiki/%D0%A8%D0%B8%D1%84%D1%80_%D0%BF%D0%B5%D1%80%D0%B5%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B8)
2. [Шифры из прошлого: тайнопись и загадки докомпьютерной эпохи](https://3dnews.ru/916293/shifri-iz-proshlogo-taynopis-i-zagadki-dokompyuternoy-epohi)
2. [Решётка Кардано](https://wiki2.org/ru/%D0%A0%D0%B5%D1%88%D1%91%D1%82%D0%BA%D0%B0_%D0%9A%D0%B0%D1%80%D0%B4%D0%B0%D0%BD%D0%BE)
3. [Шифр Виженера](https://wiki2.org/ru/%D0%A8%D0%B8%D1%84%D1%80_%D0%92%D0%B8%D0%B6%D0%B5%D0%BD%D0%B5%D1%80%D0%B0)
