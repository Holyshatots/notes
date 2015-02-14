# ColdFusion in "a week"

## Variables

Setting a variable ThisIs to fun.

`<cfset ThisIs = "fun" /> `

Look at the contents of a variable. By surrounding the variable in #s, 
it will evaluate contents of the variable. 

`<cfdump var="#Thisis#" />`

Examples of # usage.

`<cfdump var = "1 + 2" /><br />`

This will print out 1 + 2.

`<cfdump var = "#1 + 2#" /><br />`

This will print out 3.

### The Left Side of the Statement : <cfset ThisIs

The left side is the variable name. 

- Must start with a letter
- Can have numbers
- No spaces
- No special characters

### The right side of the statement: "fun">

The right side is the contents of the variable. Anything put into this
zone will be evaulated. 

Examples:

Print out the current date

` <cfset DateToday = now() /> `

Mix execution and strings

`<cfset DateToday = "Today is: #now()#" />`

Concatenation

`<cfset DateToday = "Today is: " & now() />` 

### Outputting a variable

To display the contents of a variable use `cfoutput`. 

Example usage:

```
<cfset DateToday = "Today is: #now()#" />
<cfoutput>#DateTdoay#</cfoutput>
```

To inspect or verift the contents of a variable while writing/debugging use `cfdump`. 

Example usage:

```
<cfset DateToday = "Today is: #now()#" />
<cfdump var = "#DateToday#" />
<cfset DateArray = [dateFormat(now(), "short"), dateFormat(dateadd('d',1,now()), "short"), dateFormat(dateadd('d',2,now()), "short")] />
<cfdump var = "#DateArray#" />
<cfset DateStruct = { today=dateFormat(now(), "short"), tomorrow=dateFormat(dateadd('d',1,now()), "short"), later=dateFormat(dateadd('d',2,now()), "short")} />
<cfdump var = "#DateStruct#" />
```

## Data Types

### Strings/Numbers

__Is Simple__: Yes

To set a string or number use  `cfset`.
To append strings and numbers, use & operator.

Examples:

```
<cfset aString = "hi" />
<cfset aNumber = 42 />
<cfset aStringAndANumber = aString & aNumber />

aString: <cfoutput>#aString#</cfoutput>
aNumber: <cfoutput>#aNumber#</cfoutput>
aStringAndANumber: <cfoutput>#aStringAndANumber#</cfoutput>
```

To set a large block of strings, use `cfsavecontent`.

```
<cfsavecontent variable = "EmailContent">
	Hi
	
	We want to send you a hoverboard.
	Let us know if you will accept this free offer.

	-Us
</cfsavecontent>

<cfoutput>#EmailContent#</cfoutput>
```

### Dates

__Is Simple__: Kind of

Can be set with built in functions or typed in.

```
<cfset DateToday = now() />
<cfset NewYearDay = "1/1/2013" />
```

### Arrays

Is Simple: No

Arrays are an ordered series of data. 

#### Array Creation

```
<cfset ThingsILike = ["Warm Sandy Beaches", "Tropical Drinks", 42] />
```

Or an alternate way

```
<cfset ThingsIlike = arrayNew(1) />
```

#### Adding items to an Array

NOTE: Arrays in ColdFusion start at 1, not 0

`<cfset ThingsILike[1] = "Warm Sandy Beaches" />`

or an alternate way

```
<cfset ArrayAppend( ThingsILike, "Tropical Drinks") />
<cfset ArrayAppend( ThingsILike, 42) />
<cfdump var = "#ThingsILike#" />
```

#### Displaying the contents of an array

```
<cfset ThingsILike = ["Warm Sandy Beaches", "Tropical Drinks", 42] />
<cfloop array = "#ThingsILike#" index="thing">
	<cfoutput>#thing#</cfoutput>
</cfloop>

### Structs

__Is Simple__: No

Structs are collections of data, stored with a key/name. 

#### Struct creation

`<cfset FruitBasket = structNew() />`

#### Adding items to a Struct: Bracket notation

```
<cfset FruitBasket = {} />
<cfset FruitBasket["Apple"] = "Like" />
<cfset FruitBasket["Banana"] = "Like" />
<cfset FruitBasket["Cherry"] = "Dislike" />

<cfdump var = "#FruitBasket#" />
```

#### Adding items to a Stuct Dot Notation

```
<cfset FruitBasket = {} />
<cfset FruitBasket.Apple = "Like" />
<cfset FruitBasket.Banana = "Like" />
<cfset FruitBasket.Cherry = "Dislike" />

<cfdump var = "#FruitBasket#" />
```

#### Struct Creation and population in one statement

```
<cfset fruitBasket = {
	"Apple" = "Like", 
	"Banana" = "Like",
	"Cherry" = "Dislike"
} />
```

#### Displaying the contents of a struct

```
<cfloop collection ="#FruitBasket#" item="fruit">
	<cfoutput>I #FruitBasket[fruit]# #fruit#</cfoutput><br />
</cfloop>
```

#### Queries

__Is Simple__: No

Queries are recordsets. Recordsets contain a series of columns with 0 or more rows. 

```
<cfquery name="FruitQuery" datasource="fruit">
	SELECT Name, Price
	FROM FruitStore
	WHERE Price < 7
</cfquery>

<cfloop query="FruitQuery">
	#FruitQuery.Name# costs #FruitQuery.Price# <br />
</cfloop>
```

There are some properties to get specific information about the data inside the query. 

- `Queryname.recordcount` 
- `Queryname.columnlist` = What columns does this query have? 
- `Queryname.currentrow` = What is the current row inside `cfoutput` or `cfloop`?

## Commenting

A ColdFusion comment is not displayed and only a person with access to the source code can see the content inside of the comment

HTML Comment:

` <!-- I am a HTML comment -->`

ColdFusion Comment:

`<!--- I am a ColdFusion Comment --->`

```
<cfscript
	// I am a ColdFusion comment in CFScript for a single line
	/*
		I am  a multi-line
		ColdFusion comment in CFScript
	*/
</cfscript
```

## ColdFusion Tags vs. ColdFusion Script

ColdFusion can be written using either tags or in coldfusion script. Both will be interpreted equally.

### Setting a variable

```
<cfset variable = "value" />
<cfscript>
	variable = "value";
</cfscript>
```

### Looping over an array

``` 
<cfset FruitArray = ["apple", "banana", "cherry] />
<cfloop from="1" to="#arrayLen(FruitArray)#" index="i">
	<cfoutput>#FruitArray[i]#</cfoutput>
</cfloop>

<cfscript>
	FruitArray = ["apple", "banana", "cherry"];
	for(i=1; i<=arrayLen(FruitArray); i++) {
		writeOutput(FruitArray[i]);
	}
</cfscript>
```



