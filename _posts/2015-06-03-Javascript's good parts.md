---
title:  "Javascript's good parts"
date:   June 3, 2015
categories: javascript good parts
published: false
---

- In JavaScript, arrays are objects, functions are objects, regular expressions are objects, and, of course, objects are objects.
- An object is a container of properties, where a property has a name and a value. A property name can be any string, including the empty string.
- An object literal is a pair of curly braces surrounding zero or more name/value pairs

var empty_object = {};
var stooge = {
    "first-name": "Jerome",
    "last-name": "Howard"
};

- Objects in JavaScript are class-free
- The || operator can be used to fill in default values:

var middle = stooge["middle-name"] || "(none)";
var status = flight.status || "unknown";

- Objects are passed around by reference. They are never copied:

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

- Every object is linked to a prototype object from which it can inherit properties. All objects created from object literals are linked to Object.prototype, an object that comes standard with JavaScript.





