# SOLID

Принципы SOLID определяют, как выкладывать кирпичами стены, образующие комнаты, а принципы организации компонентов — как размещать
комнаты в зданиях. 

### Single responsibility principle (принцип единственной ответственности)

Архитектура приложения должна выделять осмысленные абстракции в приложении которые имеют только одну причину для изменения.
Так класс (функция) отвечающий за обработку данных должен измениться только вслед меняющейся бизнес логики.  

### Open-closed principle (принцип открытости/закрытости)

Класс (функция) должен быть открыт для расширения и закрыт на изменения.
Расширение функциональности не влечёт изменение кода.

### Liskov substitution principle (принцип подстановки Лисков)

Функции, которые используют базовый тип, должны иметь возможность использовать подтипы базового типа, не зная об этом.
`Используй общий интерфейс а не наследуй один от другого`

### Interface segregation principle (принцип разделения интерфейса)

Много интерфейсов, специально предназначенных для клиентов, лучше, чем один интерфейс общего назначения.
Сущность не должна зависить от интерфейсов которые не используют.

### Dependency inversion principle (принцип инверсии зависимостей)

`направлен на уменьшения [зацеплёности](https://ru.wikipedia.org/wiki/Зацепление_(программирование)) кода`

Модули верхних уровней не должны импортировать сущности из модулей нижних уровней. Оба типа модулей должны зависеть от абстракций.
Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.
