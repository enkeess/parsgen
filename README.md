### Генератор синтаксических анализаторов на основе рекурсивного обхода L-графов

### Website

Ссылка на веб-сайт проекта с интерактивной средой [parsgen](http://parsgen.ru/)

### Входные данные

#### Требования ко входному файлу генератора

- Имя главного графа должно быть `_main`
- Имена подграфов должны начинаться с символа `_` (Пример: `_C`, `_smsg_graph`, ...)
- Поле `mark` может иметь значение `null`
- Поле `dir` должно содержать одно из 2-х слов : `OPEN` или `CLOSE`, для открывающих и закрывающих скобок соотвественно.

Формальное описание графа в .json формате

```sh
 {
    "graph" : [
       {
            "name" : "_string",
            "start" : "string",
            "end"   : ["string"],
            "states": [
                {
                    "name" : "string",
                    "transitions" : [
                        {
                            "to"     :  "string",
                            "mark"   :  {
                                "dir" : "OPEN" or "CLOSE",
                                "id"  : "string"
                            },
                            "labels" : [ "string" ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

### Структура выходных файлов

Набор классов/заголовочных файлов для получения синтаксического анализатора:

- `STATE_NAME(.h/.cpp)` -- enum-множество состояний
- `Dependencies(.h/.cpp)` -- внутреннее представление входного графа.
- `Mark(.h/.cpp)` -- класс скобочных пометок
- `Transition(.h/.cpp)` -- класс дуг-перехода
- `State(.h/.cpp)` -- класс состояний
- `Scanner(.h/cpp)` -- класс лексического анализа
- `Parser(.h/.cpp)` -- класс синтаксического анализа
- `Makefile` -- make сборщик

### Запуск генератора

```sh
git clone https://github.com/enkeess/parsgen.git
cd parsgen
make
./parsgen path
```

Пример вызова:

```sh
./parsgen /Users/User/Documents/example/json/ex_1.json
```

Все генерируемые файлы сохраняются в папке `build` рабочей директории

### Запуск сгенерированного синтаксического анализатора

```sh
cd build
./parser path
```

### Самостоятельная компиляция синтаксического анализатора

```sh
cd build
make
./parser path
```

Пример вызова:

```sh
./parser /Users/User/Documents/example/input/input.txt
```

### что предстоит сделать

- добавить проверку корректности введенных данных (например надо включить проверку недостижимых состояний)
- добавить проверку критерия применимости рекурсивного спуска
- корректно обрабаывать случай перехода по пустой строке
