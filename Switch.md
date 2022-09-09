### Альтернатива if/else и switch: литералы объектов в JavaScript

Сложные условия в JS всегда были источником лишнего кода. Однако использование литералов объектов в JavaScript может избавить вас от этой проблемы. Давайте разберёмся, как это работает.
Литерал объекта в JavaScript — это список пар ключ-значение, перечисленных через запятую и обёрнутый фигурными скобками.
Допустим у нас есть функция, которая принимает на вход рифмованную фразу на английском сленге кокни и возвращает её значение. Если использовать конструкцию if/else, то код будет выглядеть следующим образом:
```angular2html
function getTranslation(rhyme) {
  if (rhyme.toLowerCase() === "apples and pears") {
    return "Stairs";
  } else if (rhyme.toLowerCase() === "hampstead heath") {
    return "Teeth";
  } else if (rhyme.toLowerCase() === "loaf of bread") {
    return "Head";
  } else if (rhyme.toLowerCase() === "pork pies") {
    return "Lies";
  } else if (rhyme.toLowerCase() === "whistle and flute") {
    return "Suit";
  }

  return "Rhyme not found";
}
```
Выглядит так себе. Этот код не только плохо читается, но и использует повторяющийся вызов функции toLowerCase().
Чтобы уменьшить количество кода, мы можем использовать дополнительную переменную или конструкцию switch.
```angular2html
function getTranslation(rhyme) {
  switch (rhyme.toLowerCase()) {
    case "apples and pears":
      return "Stairs";
    case "hampstead heath":
      return "Teeth";
    case "loaf of bread":
      return "Head";
    case "pork pies":
      return "Lies";
    case "whistle and flute":
      return "Suit";
    default:
      return "Rhyme not found";
  }
}
```
Такой код выглядит чище, но это не предел. К тому же, в случае использования более сложных условий, можно случайно пропустить break и спровоцировать баги.

#### Альтернатива
Мы можем достичь той же функциональности используя объект. Вот пример, который выглядит гораздо аккуратнее:
```angular2html
function getTranslationMap(rhyme) {
  const rhymes = {
    "apples and pears": "Stairs",
    "hampstead heath": "Teeth",
    "loaf of bread": "Head",
    "pork pies": "Lies",
    "whistle and flute": "Suit",
  };

  return rhymes[rhyme.toLowerCase()] ?? "Rhyme not found";
}
```
Мы используем объект, ключи которого выполняют роль условий, а значения — результатов. Затем, с помощью квадратных скобок, мы проверяем наличие нужной строки. Так как полученная строка может быть null или undefined, то мы используем оператор Nullish coalescing (??). Таким образом мы избавляемся от null-значения, но не исключаем случай, что результат может быть равен нулю или false.
```angular2html
function stringToBool(str) {
  const boolStrings = {
    "true": true,
    "false": false,
  };

  return boolStrings[str] ?? "String is not a boolean value";
}
```
Это немного надуманный пример, но он иллюстрирует то, как использование ?? помогает избежать багов.

#### Сложная логика
Для организации более сложных условий вы можете использовать в качестве значений свойств функции.
```angular2html
function calculate(num1, num2, action) {
  const actions = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
    multiply: (a, b) => a * b,
    divide: (a, b) => a / b,
  };

  return actions[action]?.(num1, num2) ?? "Calculation is not recognised";
}
```
В этом коде мы выбираем необходимую функцию по ключу, а затем вызываем её с двумя аргументами. Так как мы используем опциональную цепочку, то функция вызовется только, если она существует. В противном случае вернётся дефолтное значение.

#### Вывод
Каждая условная конструкция имеет свою область применения. Для литералов объектов в JavaScript это длинные списки условий и сложные условия, которые можно реализовать с помощью функций.
