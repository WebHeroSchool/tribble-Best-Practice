# JavaScript Best Practice Guide

**Привет-привет :) В этом набольшом гайде я расскажу о некоторых практиках при написании Java Script кода, которые считаются лучшими.**

**Поехали!**

### 1. Поменьше глобальных переменных
Это нужно для того, чтобы уменьшить риск нежелательного взаимодействия с "с другими приложениями, виджетами или библиотеками". (с) Douglas Crockford  
Поэтому вместо этого:
```
	var name = 'Шерлок';  
	var lastName = 'Холмс';  
	  
	function doSomething() {...}  
	 
	console.log(name); // Шерлок -- or window.name
``` 
Лучше сократим число глобальных переменных, записав следующим образом:
```
	var DudeNameSpace = {  
	   name : 'Шерлок',  
	   lastName : 'Холмс',  
	   doSomething : function() {...}  
	}  
	console.log(DudeNameSpace.name); // Шерлок
```
### 2. Не бойся комментировать
Это может быть полезно как для ваших коллег, которые будут делать ревью кода или работать с ним, так и вам самим - потому что через пару месяцев вы вполне можете забыть, за что отвечала та или иная часть кода. Поэтому комментируйте важное.  
Пример:
```
	// Перебирает массив и выводит каждый элемент.    
	for(var i = 0, len = array.length; i < len; i++) {  
	   console.log(array[i]);  
	}
```

### 3. Сначала - объявление
Считается хорошей практикой объявлять все переменные в начале скрипта или функции. Это позволяет сделать код чище и собирает локальные переменные в одном месте.  
Пример:
```
// Сначала объявление
var firstName, lastName, price, discount, fullPrice;

// Потом использование
firstName = "John";
lastName = "Doe";

price = 19.90;
discount = 0.10;

fullPrice = price - discount;
```

### 4. Не используй new Object() и т.п.
Вместо этого используй: 
* {} вместо new Object()
* "" вместо new String()
* 0 вместо new Number()
* false вместо new Boolean()
* [] вместо new Array()
* function (){} вместо new Function()  
Пример: 
```
var x1 = {};           // новый объект
var x2 = "";           // новая строка
var x3 = 0;            // новый номер
var x4 = false;        // новый boolean
var x5 = [];           // новый массив
var x7 = function(){}; // новая функция
```

### 5. Отслеживайте дублирующий код
Может получиться такая ситуация, когда части кода, переменные и т.п. у вас повторяются. Отслеживайте эти моменты и удаляйте их или переписывайте, чтобы избежать путаницы и ошибок.  
Так **не**  надо:
```
let x = 5;
let y = 6;
let x = x*2
let y = y*2
```  
А вот так - надо:
```
let  x = 5;
let  y = 6;

function double (value){
return value*2;
}
double (x);
double(y);
```

### 6. Избегайте многоуровневых функций
Иными словами, не нужно злоупотреблять вложенными функциями, когда они наслаиваются друг на друга и создают мешанину из кода.  
Плохой пример:
```
function1 (a,b) {
  function2 {
    function3 {
    //слишком тяжело проследить и скорее всего может быть реализовано по-другому
    }
  }
}
```

### 7. Давайте имена со смыслом
Что имеется ввиду? Лучше пусть имя переменной или функции будет немного длиннее, но его будет легче найти. Использование имен, которые раскрывают суть (более или менее) делает чтение кода заметно легче.  
Как **не надо**:
```
// Либо не говорящие названия, либо слишком обобщенные
let d
let elapsed
const ages = arr.map((i) => i.age)
```  
Как **надо**:
```
// Длиннее, но смысл понятнее
let daysSinceModification
const agesOfUsers = users.map((user) => user.age)
```
Обрати внимание, что слишком увлекаться тоже не нужно. Слишком сложные, "закрученные" имена не меньше усложнят чтение, чем бессмысленные. Постарайся найти баланс между смысловым "наполнением" имени и простотой. 

### 8. Используй промисы
Там, где это возможно, используй промисы. Тогда вместо сложной цепочки асинхронных функций, ты сможешь создать более простой и чистый код благодаря промисам.  
Как **не надо**:
```
asyncFunc1((err, result1) => {
  asyncFunc2(result1, (err, result2) => {
    asyncFunc3(result2, (err, result3) => {
      console.lor(result3)
    })
  })
})
```  
Как лучше:
```
asyncFuncPromise1()
  .then(asyncFuncPromise2)
  .then(asyncFuncPromise3)
  .then((result) => console.log(result))
  .catch((err) => console.error(err))
```

### 9. === вместо ==
В случае, если вам нужно провести сравнение двух операндов, лучше использовать === и !==, а не == и !=. Операторы строгого сравнения не позволят появиться ошибке: если операнды   разных типов, то всегда будет возвращаться false.  
Пример:
```
	console.log("3" === 3);           // false
	console.log(true === 1);          // false
	console.log(null === undefined);  // false
```
*При этом обратим внимание, что:*
``` 
	null == undefined;    // true
```

### 10. Попробуйте без JS
Наконец, попробуйте для начала проверить, как работает ваш сайт без Java Script. Когда убедитесь, что все удовлетворительно работает, можете накрутить дополнительные фишки, добавить возможности.  
Этот совет может показаться странным, но порой люди в самом деле отключают Java Script, и чтобы все не уехало - лучше сначала протестировать сайт без него.