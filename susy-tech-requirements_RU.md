# SuSy: техническое требование

### Аннотация

Этот документ представляет технические детали для SuSy и рекомендации о том, как реализовать конкретные интерфейсы. * Основные принципы интерфейсов * и * абстракций * не должны нарушаться.

---
### Оглавление

Этот документ состоит из нескольких частей. Мы погрузимся только в жизненно важные части системы.
1. Участие Gravity Node.
2. Уникальность и специфика SuSy Extractor.
3. Будущее расширение приложения.

---
#### 1. Участие гравитационного узла

Строго говоря, приложение SuSy соответствует всем требованиям, установленным Gravity Protocol. Это включает в себя наличие определенных небул (по крайней мере 2) и 2 конкретных экстракторов для каждой из них.

По сравнению с * обычной Gravity Protocol нодой* Стоит отметить, что * приложение SuSy * отличается от него *** только наличием определенных небул и экстракторов ***. SuSy соответствует ограничениям леджера (кор), и зависимость с ним *** жизненно важна ***.

Gravity Node существует и работает * под капотом * SuSy.

#### 2. Уникальность и специфика SuSy Extractor.

Что касается поведения Extractor, SuSy стремится установить для него определенные обязанности, такие как:
1. *Управление состоянием платежа в обоих чейнах (цель и источник).*
2. Подтверждение / отклонение результатов
3. Наблюдение за очередью платежей (какой платеж будет действовать в точные сроки).

Основная цель, которую должен достичь экстрактор SuSy, - это управление состоянием в обеих чейнах.

![SuSy экстрактор](https://i.imgur.com/GuQD90A.png)

По замыслу мы должны следовать этим утверждениям:
A) Обеспечить второй уровень логики на верхнем доступном контроллере транспорта данных (HTTP).
Б) Инкапсулировать работу с pulse tx. Строго говоря, заблокируйте средства в цепи «А» и разблокируйте в цепи «В».
C) Предоставить маршруты для обязательных обзорных данных, таких как «тег подачи данных» и «описание»
D) Предоставить маршрут (только один) для доступа к состоянию передачи, обрабатывать в соответствии с параметрами (цепочка, идентификатор сети, адрес отправителя).
E) Pulse TX должна быть инкапсулирована (*пользователь ничего не знает о internal ledger*)

Экстрактор работает в основном на ***получении*** и ***доставке*** текущей информации о платежах по конкретным чейнам. Получатели информации конкретного чейна должны реализовываться с использованием ***различных адаптеров*** для конкретной цепочки блоков, потому что API отличается. Адаптеры внутри экстрактора сочетают в себе ***совместимость с несколькими*** чейнами.

Здесь делается вывод, что SuSy *** имеет только один экстрактор ***. *** Совместимость с несколькими чейнами *** предполагает *** несколько экземпляров одного экстрактора ***. Такая цель достигается *** переключением адаптеров ** внутри экстрактора *** во время работы ***. * (пример в спецификации) *.
