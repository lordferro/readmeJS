<!-- Псевдомассив arguments -->
Доступ к списку всех аргументов можно получить при помощи специальной переменной arguments, которая доступна только внутри функции и хранит все аргументы как псевдомассив.

Псевдомассив - коллекция, со свойством length и возможностью обратиться к элементу по индексу, но отсутствием большинства методов для работы с массивом.

Рассмотрим пример использования arguments в функции, которая умножает любое количество аргументов:

function multiply() {
  let total = 1;

  for (const argument of arguments) {
    total *= argument;
  }

  return total;
}

console.log(multiply(1, 2, 3)); //  6
console.log(multiply(1, 2, 3, 4)); //  24
console.log(multiply(1, 2, 3, 4, 5)); //  120

<!-- Сделать массив из псевдо массива -->
const arg = Array.from(arguments)

<!-- Современный метод (rest) -->
const fn = function(...args) {
  console.log(args) <!--  это будет полноценный массив из значений переданных в функцию. [1, 2, 3] -->
}
fn(1, 2, 3);
<!-- Добавить переменные (до rest) -->
const fn = function(a, b,...args) {
  console.log(args) <!--  это будет [1, 2, 3], а переменные создадуться а=0, b=00 -->
}
fn(0,00, 1, 2, 3);

_____________________________
<!-- Преобразование псевдомассива -->
Обычно псевдомассив необходимо преобразовать в полноценный массив, так как у псевдомассива нет методов массива, например slice() или includes(). На практике применяют несколько основных способов.

Используя метод Array.from(), который создаст массив из псевдомассива.

function fn() {
  // В переменной args будет полноценный массив
  const args = Array.from(arguments);
}

Используя операцию ... (rest), она позволяет собрать произвольное количество элементов, в нашем случае аргументов, в массив и сохранить его в переменную. Собираем все аргументы используя операцию rest прямо в подписи функции.

function fn(...args) {
  // В переменной args будет полноценный массив
}
______________________________
<!-- Паттерн «Ранний возврат» -->
function withdraw(amount, balance) {
  // Если  условие выполняется, вызывается console.log
  // и выход из функции. Код идущий после тела if не выполнится.
  if (amount === 0) {
    console.log("Для проведения операции введите сумму больше нуля");
    return;
  }

  // Если условие первого if не выполнилось, его тело пропускается
  // и интерпретатор доходит до второго if.
  // Если условие выполняется, вызывается console.log и выход из функции.
  // Код идущий после тела if  не выполнится.
  if (amount > balance) {
    console.log("Недостаточно средств на счету");
    return;
  }

  // Если ни один из предыдущих if не выполнился,
  // интерпретатор доходит до этого кода и выполняет его.
  console.log("Операция снятия средств проведена");
}

withdraw(0, 300); // "Для проведения операции введите сумму больше нуля"
withdraw(500, 300); // "Недостаточно средств на счету"
withdraw(100, 300); // "Операция снятия средств проведена"
________________________________-
