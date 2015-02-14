# Day 2: Decision Making and Scopes

## Decision Making

If/else

```
<cfif expression>
	//Markup
<cfelse>
	//More markup
</cfif>
```

If/elseif

```
<cfif expression>
	// markup
<cfelseif another_expression>
	// more markup
<cfelse>
	// more markup
</cfif>
```

CFML and CFScript Operators
- IS, EQUAL, EQ
- IS NOT, NOT EQUAL, NEQ
- GT, GREATER THAN, LT, LESS THAN, GTE, LTE
- CONTAINS
- DOES NOT CONTAIN

Example usage:

```
<cfif myValue EQ 'ColdFusion'>
	//code
</cfif>
```

Script-based example:

```
if(myValue == 'ColdFusion'){
	//code
} else if (myValue != '.NET') {
	x = 277;
} else
	//code
}
```

There are also a series of boolean operators as follows:

- AND / &&
- OR / ||
- NOT / !
- XOR, EQV
- IMP - implication

Example of compound expression:

```
<cfif structKeyExists(myStruct, 'age') AND myStruct.age LTE 7>
	//code
</cfif>

NOTE: ColdFusion compound expressions work from left to right


