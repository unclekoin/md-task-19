 # Модуль 1, урок 19. ES6. import / export

 ## Задание 1

В заданиях данного урока вы создадите с нуля сервис доната денег на благотворительные нужды.

1. У вас есть пустой проект. [Скачайте его](https://drive.google.com/drive/folders/1aQzVQ_5bkm71IKgTi6CAZTXMLJvVJbgi) и откройте в редакторе кода. 

2. Установите все пакеты при помощи команды `npm install` и запустите проект через `npm start`.

3. Создайте структуру проекта. Для этого в корне проекта создайте папку `src`, а в ней еще две папки:
- `core` для глобальных частей проекта 
- `modules` для основных компонентов (например, списока донатов, форма отправки доната и т.д.)

4. В папке `modules` создайте файл `app.js` и нем необходимо реализовать класс `App`. В классе должен быть метод `run`, который помещает внутрь тега `body` текст “Hello World”.

5. Импортируйте по умолчанию класс `App` (export default) в файл `index.js`, создайте экземпляр класса `App` и вызовите метод `run`.

## Задание 2

1. Реализуйт форму создания донатов. В папке `modules` создайте файл `donate-form.js`. В данном файле вам необходимо создать класс `DonateForm` с методом `render`, который будет возвращать HTML-элемент итоговой формы. Экспортируйте (export) класс `DonateForm`.

2. В классе `DonateForm` вам необходимо реализовать HTML-структуру ниже, используя `document.createElement`. Для разделения логики позволяется создавать свои поля и методы класса. По возможности делайте их приватными, чтобы писать чистый код на ООП и применять принцип инкапсуляции.

```html
<form class="donate-form">
  <h1 id="total-amount">28$</h1>
  <label class="donate-form__input-label">
      Введите сумму в $
      <input
          class="donate-form__donate-input"
          name="amount"
          type="number"
          max="100"
          min="0"
          required=""
      >
  </label>
  <button class="donate-form__submit-button" type="submit">
      Задонатить
  </button>
</form>
```
3. Имротируйте класс `DonateForm` в `app.js`. С помощью метода `run` класса `App` и разметки созданной в классе `DonateForm` поместиту верстку формы внутрь тега `body`.

## Задание 3.

Сейчас вам необходимо будет отрисовать список всех донатов, которые будут делать пользователи сервиса. 



1. В папке `modules` создайте файл `donate-list.js` и в нем реализуйте класс `DonateList`. Конструктор данного класса должен принимать массив `donates`. Данный массив состоит из объектов, у которых есть ключи `date` (дата создания доната) и `amoun`t (сумма доната). Реализуйтк в классе `DonateList` метод `render`, который будет отрисовывать HTML-шаблон приведенный ниже:

```html
<div class="donates-container">
  <h2 class="donates-container__title">Список донатов</h2>
  <div class="donates-container__donates">
      <div class="donate-item">July 6th 2021, 10:28:49 am - <b>4$</b></div>
      <div class="donate-item">July 6th 2021, 10:28:49 am - <b>20$</b></div>
      <div class="donate-item">July 6th 2021, 10:28:49 am - <b>3$</b></div>
      <div class="donate-item">July 6th 2021, 10:28:49 am - <b>1$</b></div>
  </div>
   </div>
```

Элемент ниже отображает информацию о донате:
```html
<div class="donate-item">July 6th 2021, 10:28:49 am - <b>4$</b></div>
```
“July 6th 2021, 10:28:49 am” - заныенме свойства `date` из объекта массива `donates`, а “4$” - значение свойства `amount`.

2. Экспортируйте класс `DonateList` (export), а затем импортируйте его в файл `app.js`.

3. Через метод `run`класса `App` и с помощью `DonateList` вам необходимо поместить всю верстку списка донатов внутрь элемента с тегом `body`.

Для теста отрисовки списка донатов, используйте данный массив donates:

```js
const mockDonates = [
   { amount: 4, date: new Date() },
   { amount: 20, date: new Date() },
   { amount: 3, date: new Date() },
   { amount: 1, date: new Date() },
];
```

### Примечание
* для разделения логики позволяется создавать свои поля и методы в классе  `DonateList`. По возможности делайте их приватными, чтобы писать чистый код на ООП и применять принцип инкапсуляции;
* сейчас у вас текст даты в HTML-элементе доната будет отображаться не как в HTML-шаблоне, это нормально. Данную логику вы разработаете позже.

## Задание 4.

1. Создайте глобальное состояние, в котором будет хранится все важные данные проекта. Для этого в конструкторе класса `App` создайте объект `state` (`this.state`), в котором будут два свойства:

* `donates` - массив донатов, который будет передаваться в конструктор класса `DonateList`. По умолчанию значение должно быть пустым массивом.

* `totalAmount` - общая сумма донатов (тип данных number). По умолчанию значение должно равняться нулю.

2. Передайте массив `donates` из `state` в конструктор класса `DonateList`, а значение свойства `totalAmount` в конструктор класса `DonateForm`. 

3. В конструкторе класса `DonateForm`: 
* добавьте параметр `totalAmount` и инициализируйте его с помощью `this` 
* создайте метод `updateTotalAmount`, который будет принимать параметр `newAmount` и помещать текст состоящий из параметра `newAmount` и знака `$` в элемент с `id` “total-amount”. У вас должно получиться `0$`.

4. В классе `DonateList` создайте метод `updateDonates`, который будет принимать параметр `updatedDonates` (новый массив `donates`). Данный метод должен очищать элемент с классом “donates-container__donates” и отрисовывать в нем новые донаты из массива `updatedDonates`.


5. После создания каждого доната вам необходимо обновлять объект `state` в классе `App` и HTML-элементы. Для обновления состояния создайте метод `createNewDonate` в классе `App`, данный метод принимает параметр `newDonate`, который является новым объектом массива `donates`.

6. В методе `createNewDonate` нужно:
* добавить `newDonate` в массив `donates` объекта `state`
* обновить `totalAmount` объекта `state`
* вызвать метод `updateDonates` класса `DonateList`
* вызвать метод `updateTotalAmount` класса `DonateForm`

7. Передайте метод `createNewDonate` класса `App`, как параметр в конструктор класса `DonateForm` и инициализируйте его в конструкторе при помощи `this`. 

8. В классе `DonateForm` повесьте обработчик событий “submit” на элемент с классом “donate-form”. В данном обработчике вам необходимо: 
* создать новый объект доната с ключами `date` и `amount`
* вызвать метод `createNewDonate`, который вы до этого передали в конструктор 
* после создания каждого доната текстовое поле с классом “donate-form__donate-input” должно быть пустым



### Примечание
Когда вы передаете функцию или метод как параметр в другую функцию или метод, у вас может теряться `this`. Поэтому присвойте this через bind.

### Подсказка: 
`this` будет теряться при передаче метода `createNewDonate` как параметра в конструктор класса `DonateForm`, передайте его, как `this.createNewDonate.bind(this)`. Здесь `bind(this)` привязывает контекст класса `App` к методу `createNewDonate`.

## Задание 5.

Для начала давайте заметим, что у нас все суммы написаны в долларах `$`. А представьте, что придет заказчик и скажет: “А давайте все суммы будут в евро”. С текущей реализацией вам придется исправлять значок доллара на евро во всех возможных файлах, что конечно же неудобно. Для этого есть решение. Создать глобальное значение и использовать его во всем проекте.

1. В папке `core` создайте папку `constants` и создайте файл `settings.js`, в котором будет хранится объект `Settings`. В данном объекте создайте ключ `currency`, у которого будет значение `$`.

2. Экспортируйте `Settings` и затем с помощью import заменить все значки `$` в файлах на `Settings.currency`.

После проделанной работы вы можете спокойно изменять значение свойства currency в объекте Settings, и валюта изменится во всем проекте.

### Условие: 
При импортах необходимо хотя бы 1 раз использовать ключевое слово as. Например, import `{ Object as Obj }`.

## Задание 6.

Проект почти готов и осталось сделать всего несколько важных дел. Сейчас вам необходимо будет создавать вспомогательные функции, которые будут использоваться глобально по проекту.

1. Создайте папку `utils` в `core`. 

2. В `utils` создайте файл `index.js`. В данном файле будут хранится все вспомогательные функции, которые относятся к проекту.

3. Первая вспомогательная функция должна называться `calculateSumOfNumbers`. Она принимает в качестве параметра массив `numbers`, который состоит исключительно из чисел. Функция `calculateSumOfNumbers` считает сумму всех элементов массива и возвращает ее итоговое значение.

4. Вторая функция будет отвечать за конвертацию даты. Назовите функцию `getFormattedTime`. Она принимает один параметр `date`, который является объектом `Date`. Изначально `new Date()` при преобразовании к строке возвращает примерно такое значение `Tue Jul 06 2021 14:00:05 GMT+0300 (Moscow Standard Time)`. Функция `getFormattedTime` должна преобразовывать его к такому значению `July 6th 2021, 2:00:05 pm`. Это можно сделать при помощи библиотеки `momentjs`.

```js
moment(date).format('MMMM Do YYYY, h:mm:ss a')
```
Установите [momentjs](https://momentjs.com/) и реализуйте функцию `getFormattedTime`.

5. Экспортируйту эти функции и используйте в коде.

6. Создайте в файле `app.js` массив `mockDonates` и передайте его как значение в `donates` у объекта `state`.

```js
const mockDonates = [
  { amount: 4, date: new Date() },
  { amount: 20, date: new Date() },
  { amount: 3, date: new Date() },
  { amount: 1, date: new Date() },
];
```

7. Так как у нас есть начальные значения полей `amount` объектов массива `donates`, а `totalAmount` по умолчанию равен 0, то необходимо рассчитать начальную сумму всех донатов с помощью функции `calculateSumOfNumbers` и перезаписать значение `totalAmount`.

8. Используйте функцию `getFormattedTime` для создания контета элементов с классами “donate-item”. До этого текст в данных элементах выглядел следующим образом `Tue Jul 06 2021 14:00:05 GMT+0300 (Moscow Standard Time) - 4$`. С использованием getFormattedTime текст должен стать таким: `July 6th 2021, 2:00:05 pm - 4$`.

### Условие:
* при импортах обязательно используйте конструкцию `import * as`.

