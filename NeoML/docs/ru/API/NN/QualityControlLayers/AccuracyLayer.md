# Класс CAccuracyLayer

<!-- TOC -->

- [Класс CAccuracyLayer](#класс-caccuracylayer)
    - [Настройки](#настройки)
        - [Сброс статистики](#сброс-статистики)
    - [Обучаемые параметры](#обучаемые-параметры)
    - [Входы](#входы)
    - [Выходы](#выходы)

<!-- /TOC -->

Класс реализует слой, считающий долю правильно классифицированных объектов.

## Настройки

### Сброс статистики

```c++
void SetReset( bool value );
```

Включает и отключает сброс статистики между запусками. По умолчанию **включен**.

## Обучаемые параметры

Слой не имеет обучаемых параметров.

## Входы

Слой имеет 2 входа.

На первый вход подается блоб с ответами сети размера:

- `BatchLength * BatchWidth * ListSize` равно числу объектов;
- `Height`, `Width` и `Depth` равны `1`;
- `Channels` равен `1` для бинарной классификации или числу классов (больше `1`) для многоклассовой.

На второй вход подается блоб с правильной разметкой, имеющий те же размеры, что и блоб первого входа. 

- если `Channels` у блоба первого входа равен `1`, правильная разметка должна содержать `1` для объектов одного класса и `-1` для другого;
- если `Channels` больше `1`, правильная разметка должна содержать `1` для правильного класса и `0` для всех остальных.

## Выходы

Единственный выход содержит блоб размера `1`, который содержит долю правильно классифицированных объектов среди всех объектов.

Если `SetReset()` выключен, то слой **накапливает** статистику между запусками.
