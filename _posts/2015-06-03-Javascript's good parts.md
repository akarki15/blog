---
title:  "Notes from javascript the good parts"
date:   June 3, 2015
categories: javascript good parts
published: true
---

- In JavaScript, arrays are objects, functions are objects, regular expressions are objects, and, of course, objects are objects.
- An object is a container of properties, where a property has a name and a value. A property name can be any string, including the empty string.
- An object literal is a pair of curly braces surrounding zero or more name/value pairs

{% highlight javascript %}
var empty_object = {};
var stooge = {
    "first-name": "Jerome",
    "last-name": "Howard"
};
{% endhighlight %}

- Objects in JavaScript are class-free
- The \|\| operator can be used to fill in default values:

{% highlight javascript %}
var middle = stooge["middle-name"] || "(none)";
var status = flight.status || "unknown";
{% endhighlight %}

- Objects are passed around by reference. They are never copied:

{% highlight javascript %}
var x = stooge;
x.nickname = 'Curly';
var nick = stooge.nickname;
    // nick is 'Curly' because x and stooge
    // are references to the same object
var a = {}, b = {}, c = {};
    // a, b, and c each refer to a
    // different empty object
a = b = c = {};
    // a, b, and c all refer to
    // the same empty object
{% endhighlight %}

- Every object is linked to a prototype object from which it can inherit properties. All objects created from object literals are linked to Object.prototype, an object that comes standard with JavaScript.

- Functions in JavaScript are objects. Objects are collections of name/value pairs having a hidden link to a prototype object. Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype). 

- Function objects are created with function literals:

{% highlight javascript %}
// Create a variable called add and store a function
// in it that adds two numbers.
var add = function (a, b) { return a + b;};
{% endhighlight %}

- Function name is optional. When it doesn't have a name, it is called an "anonymous function". Above example is an anoymous function; it is just assigned to a variable but it doesn't have a name. 

- JS Variable Scope example: 

{% highlight javascript %}
// Source: http://javascriptissexy.com/javascript-variable-scope-and-hoisting-explained/
// If you don't declare your local variables with the var keyword, they are part of the global scope​
​var name = "Michael Jackson";
​
​function showCelebrityName () {
	console.log (name);
}
​
​function showOrdinaryPersonName () {	
	name = "Johnny Evers";
	console.log (name);
}
showCelebrityName (); // Michael Jackson​
​
​// name is not a local variable, it simply changes the global name variable​
showOrdinaryPersonName (); // Johnny Evers​
​
​// The global variable is now Johnny Evers, not the celebrity name anymore​
showCelebrityName (); // Johnny Evers​
​
​// The solution is to declare your local variable with the var keyword​
​function showOrdinaryPersonName () {	
	var name = "Johnny Evers"; // Now name is always a local variable and it will not overwrite the global variable​
	console.log (name);
} 
{% endhighlight %}

- Curly brackets don't start a new scope. Prettty bad if you ask me (having come from Java background).
{% highlight javascript %}
for (var i = 1; i <= 10; i++) {
	console.log (i); // outputs 1, 2, 3, 4, 5, 6, 7, 8, 9, 10;​
};
​
​// The variable i is a global variable and it is accessible in the following function with the last value it was assigned above ​
​function aNumber () {
console.log(i);
}
​
​// The variable i in the aNumber function below is the global variable i that was changed in the for loop above. Its last value was 11, set just before the for loop exited:​
aNumber ();  // 11​
{% endhighlight %}
- Variable Hoisting: Variable *declarations* are hoisted to the top of the scope (could be local/functional or global). Example: 
{% highlight javascript %}
function showName () {
console.log ("First Name: " + name);
​var name = "Ford";
console.log ("Last Name: " + name);
}
​
showName (); 
​// First Name: undefined​
​// Last Name: Ford​
​
​// The reason undefined prints first is because the local variable name was hoisted to the top of the function​
​// Which means it is this local variable that get calls the first time.​
​// This is how the code is actually processed by the JavaScript engine:​
​
​function showName () {
	var name; // name is hoisted (note that is undefined at this point, since the assignment happens below)​
console.log ("First Name: " + name); // First Name: undefined​
​
name = "Ford"; // name is assigned a value​
​
​// now name is Ford​
console.log ("Last Name: " + name); // Last Name: Ford​
}
{% endhighlight %}
- *Function Declaration Overrides Variable Declaration When Hoisted*
- Both function declaration and variable declarations are hoisted to the top of the containing scope. And function declaration takes precedence over variable declarations (but not over variable assignment). As is noted above, variable assignment is not hoisted, and neither is function assignment. As a reminder, this is a function assignment: var myFunction = function () {}.
Here is a basic example to demonstrate:

{% highlight javascript %}
// Both the variable and the function are named myName​
​var myName; 
​function myName () {
console.log ("Rich");
}
​
​// The function declaration overrides the variable name​
console.log(typeof myName); // function
 // But in this example, the variable assignment overrides the function declaration​
​var myName = "Richard"; // This is the variable assignment (initialization) that overrides the function declaration.​
​
​function myName () {
console.log ("Rich");
}
​
console.log(typeof myName); // string 
{% endhighlight %}

- It is important to note that function expressions, such as the example below, are not hoisted.
{% highlight javascript %}
var myName = function () {
console.log ("Rich");
} 
{% endhighlight %}
- In strict mode, an error will occur if you assign a variable a value without first declaring the variable. Always declare your variables.


