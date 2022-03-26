# **Задача №2 "Исследование JVM через VisualVM"**

## **Загрузка классов**

**1. Вывод консоли: "14:58:41.910650200: loading io.vertx"** - начало выполнения метода загрузки классов библиотеки io.vertx.


* на графике Classes видно, что до этого времени количество загруженных класов было почти неизменно:

![](/resources/14%2C58%2C41_Classes.jpg "Classes: start loading io.vertx")

* свободен весь объем Metaspace:

![](/resources/14%2C58%2C41_Metaspace.jpg "Metaspace: start loading io.vertx")

* размер Heap также практически не изменялся до старта этого метода:

![](/resources/14%2C58%2C41_Heap.jpg "Heap: start loading io.vertx")

**2. Вывод консоли: "14:58:42.527867700: loaded 529 classes"** - сообщение выводится перед завешением метода после окончания закрузки классов библиотеки.

* количество загруженных классов увеличилось с 2109 до 2936:

![](/resources/14%2C58%2C42_Classes.jpg "Classes: loaded io.vertx")

* объем занятой памяти Metaspace вырос до 15Мб:

![](/resources/14%2C58%2C42_Metaspace.jpg "Metaspace: loaded io.vertx")

* размер кучи изменился с 15Mб до 36Мб:

![](/resources/14%2C58%2C42_Heap.jpg "Heap: loaded io.vertx")

**3. Вывод консоли: "14:58:45.546090800: loading io.netty"** - начало работы с библиотекой io.netty.

* количество загруженных классов не изменилось - 2936:

![](/resources/14%2C58%2C45_Classes.jpg "Classes: start loading io.netty")

* объем занятой памяти Metaspace также без изменений:

![](/resources/14%2C58%2C45_Metaspace.jpg "Metaspace: start loading io.netty")

* непонятно почему увеличился размер Heap до 52Мб:

![](/resources/14%2C58%2C45_Heap.jpg "Heap: start loading io.netty")

**4. Вывод консоли: "14:58:46.811645900: loaded 2117 classes"** - завершение просмотра классов библиотеки io.netty.

* количество загруженных классов 4751:

![](/resources/14%2C58%2C46_Classes.jpg "Classes: loaded io.netty")

* занятая память Metaspace увеличилась еще на 6Мб за счет подгруженных классов:

![](/resources/14%2C58%2C46_Metaspace.jpg "Metaspace: loaded io.netty")

* в области Heap наблюдается освобождение памяти - вероятно, поработал сборщик мусора:

![](/resources/14%2C58%2C46_Heap.jpg "Heap: loaded io.netty")

**5. Вывод консоли: "14:58:49.820228300: loading org.springframework"** - старт загрузки классов из org.springframework.

* классов к тому времени загружено 5017:

![](/resources/14%2C58%2C49_Classes.jpg "Classes: start loading org.springframework")

* занято в Metaspace 21Мб:

![](/resources/14%2C58%2C49_Metaspace.jpg "Metaspace: start loading org.springframework")

* в память Heap догрузилось 5Мб:

![](/resources/14%2C58%2C49_Heap.jpg "Heap: start loading org.springframework")

**6. Вывод консоли: "14:58:50.210846200: loaded 869 classes"** - завершение и выход из метода loadToMetaspaceAllFrom().

* общее количество загруженных классов увеличилось до 5909:

![](/resources/14%2C58%2C50_Classes.jpg "Classes: loaded org.springframework")

* в Metaspace занято 32Мб:

![](/resources/14%2C58%2C50_Metaspace.jpg "Metaspace: loaded org.springframework")

* в Heap, напротив, наблюдается освобождение памяти - вероятно работа уборщика:

![](/resources/14%2C58%2C50_Heap.jpg "Heap: loaded org.springframework")

## **Создание объектов**

Classloader добавил один класс, и количество класов не менялось до окончания программы. Размер области Metaspace, также, изменений практически нет до самого окончания программы.

![](/resources/14%2C58%2C53_Classes.jpg) ![](/resources/14%2C58%2C53_Metaspace.jpg)

## Рассмотрим динамику загрузки Heap.

**1. Вывод консоли: "14:58:53.219670200: creating 5000000 objects" и "14:58:53.719641900: created"** - создание 5 000 000 экземпляров тестового класса. Размер занятой памяти увеличился до 193Мб:

![](/resources/14%2C58%2C53_Heap.jpg)

**2. Вывод консоли: "14:58:56.750846: creating 5000000 objects" и "14:58:57.207239: created"** - размер занятой памяти увеличился уже до 448Мб. 

![](/resources/14%2C58%2C56_Heap.jpg) ![](/resources/14%2C58%2C57_Heap.jpg)

**3. Вывод консоли: "14:59:00.300941700: creating 5000000 objects" и "14:59:00.691507400: created"** - размер занятой памяти увеличился уже до 718Мб.

![](/resources/14%2C59%2C00_Heap.jpg)