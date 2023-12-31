# Задача 4. Парсер CSV

[![Testing](https://github.com/ptrvsrg/CSV-parser/actions/workflows/cmake.yml/badge.svg)](https://github.com/ptrvsrg/CSV-parser/actions/workflows/cmake.yml)

### Subtask 1. Print tuple
Используя рекурсивные шаблоны реализовать оператор для печати std:tuple:

    auto operator<<(std::basic_ostream<CharT, Traits>& os, std::tuple<Types...> const& t)


### Subtask 2. Simple CSV parser
#### CSV format
Табличные данные могут быть представлены как текстовый файл с разделителем `\n` между строками и символом `,` для разделения ячеек внутри строки. Считаем что данные символы не встречаются внутри данных.

#### CSVParser
Написать класс, делающий возможным следующую потоковую работу с CSV:

    int main()
    {
        ifstream file("test.csv");
        CSVParser<int, string> parser(file, 0 /*skip first lines count*/);
        for (tuple<int, string> rs : parser)
            cout << rs << endl;
    }

Потоковая обработка подразумевает lazy (ленивое) чтение строк. Таким образом необходимо реализовать [InputIterator](http://en.cppreference.com/w/cpp/concept/InputIterator) для чтения данных в CSV файле.

### Subtask 3. Improved CSV parser
Добавить следующие возможности:
+ Поддержка экранирования данных
+ Конфигурация парсера: что считать разделителем между строками и колонками и какой символ использовать для экранирования (по умолчанию двойные кавычки)
+ Обработка ошибок: выкидывать исключение с информаций о месте в файле (строка, колонка), где произошла ошибка разбора данных
