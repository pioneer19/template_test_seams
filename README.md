### TDD со швами через аргументы шаблонов

Суть модульного тестирования - в проверке работы кода
в изоляции от зависимостей.
В языках без особых запросов к производительности это
часто делается с помощью внедрения зависимостей через
интерфейсы с виртуальными функциями. В C++ этого хочется
избежать (не всегда девиртуализация пройдет успешно,
а inline там вообще сделать почти без шансов). В этом
проекте изоляция кода делается с помощью реализации 
внутри шаблона, который параметризуется разными типами
для production использования и для тестов. Таким образом в production тестируемый
код будет обладать той же производительностью, как если
никаких тестов и изоляции зависимостей не было бы
(в том числе с полноценным inline кода).

В этом проекте тестируется класс `HelloWorld`.

```bash
$ tree  src/
src/
├── hello_world.cpp      # инстанциирование production методов шаблонного класса
├── hello_world.h        # инстанциирование типа (класса) из шаблона
├── hello_world_tmpl.h   # объявление template<typename...> class HelloWorld
├── hello_world_tmpl.ipp # методы шаблонного класса HelloWorld
├── main.cpp             # использование HelloWorld в production
└── test_file.cpp        # тесты для HelloWorld
```

Использование `HelloWorld` почти не отличается, как если бы
это был обычный класс с заголовком в `.h` и реализацией
в `.cpp` (хотя они там и генерируются из шаблонов).
Инстанциирование шаблонов при компиляции происходит **один** раз в `.cpp` файле.

#### Другие варианты швов для тестирования

Внедрить интерфейс можно через
1. конструктор
2. сеттеры
3. производный класс
4. service locator/фабрику
