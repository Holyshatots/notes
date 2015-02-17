# Javascript

## Cheat sheet

```
// Declare string car
var car = "Fiat";
// NOTE: Do not declare like:
var x = new String();
// because it complicates code and slows down execution speed


// Object
var car = {type:"Fiat", model:500, color:"white"};
// Get an property of the object
car.type;
// or
car["type"];


// Array
var car = ["Fiat", "BMW", "othercar"];
// Access elements
var name = car[0];
// NOTE: Remember javascript arrays begin on 0
// Adding Array Elements
car[car.length] = "new car";


// Function
var bestFunction = function(param1, param2) {
	// Do stuff
};
// OR
function myFunction(param1, param2) {
	// stuff and code
}


// Events
<button onclick='displayDate()'>The time is?</button>
/* Common events:
	- onchange
	- onclick
	- onmouseover
	- onmouseout
	- onkeydown
	- onload

// For loop
var i;
for(i = 0; i < l; i++) {
	// code
}

	
// Comparisons
0 == ""; // true
0 === ""; // false
// The === operator converts to matching types before comparison so it should be used


// DOM
<p id="demo"></p>
<script>
document.getElementById("demo").innerHTML = "Hello world";
</script>


// jQuery
$(this).hide() // hide the current element
$("p").hide() // hide all <p> elements
$(".test").hide() // hides all elements with class="test"
$("#test").hide() // hides the element with id="test"

$(document).ready(function(){
	// puts jQuery code in here to make sure the document is finished loading
}

```


## Strings

Common methods:

charAt()
concat()
indexOf()
lastIndexOf()
match()
replace()
search()
slice()
split()
substr()
substring()
toLocaleLowerCase()
trim()