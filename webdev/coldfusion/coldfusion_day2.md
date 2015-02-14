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

Example of a switch statement

```
<cfswitch expression="#myVar#">
	<cfcase value="1">
		//code
	</cfcase>
	<cfcase value ="9, 10">
		//code
	</cfcase>
	<cfdefaultcase>
		// finally
	</cfdefaultcase>
</cfswitch>
```

Example of a switch statement in cfscript:

```
switch (myVar) {
	case 1:
		writeOutput('Value was 1');
		break;
	case 9:
		writeOutput('Value was 9');
		break;
	default:
		writeOutput('Value was not 1 or 9');
}
```

ColdFusion offers the use of ternary operators like below:

```
x = (myVar == 1) ? 1 : 277;
```

which is equivalent to

```
switch(myVar == 1) {
	x = 1;
} else {
	x =277;
}
```

## Scopes

Variables are grouped together in scopes. Each scope has its own purpose and lifecycle.

The following are major scopes available:

- Variables : Default scope available in ColdFusion templates. Available only during the execution of the template
- URL: All variables in the query string or sent to ColdFusion via an HTTP GET request are in the URL scope. URL variables are available for the current request.
- Form: All variables posted from a form (HTTP POST) are available in teh Form scope. Form variables are available for the current request.
- CGI: CGI variables sent from the browser are placed into the CGI scope. CGI variables are available for the current request.
- Server: Developers may choose to utilize the server scope to share data across application running within the context of the current ColdFusion instance of cluster. This scope persists across requests and is available until the server shuts down. 
- Application: Application variables are shared amongst all connected clients for the current named application. This scope is also used for objects instantiated using the singleton pattern. This scope is availabe across request for the life of the pplication, which may terminate on server shutdown, application malfunction, or application timeout. 
- Session: Developers use session variables to store a single visitor's data across requests. This scope is only available to the current session, and will persist until server or application terminator, or session timeout. 
- Request: The request scope contains data passed into a ColdFusion function. The arguments scrop is mutually exclusive with the local function scope, and may not contain the same variable names as the local scope. This scope is available during  the current execution of a function, and is private to the current function context.
- Attributes: This scope contains variables passed in as attributes to a ColdFusion custom tag. The data in this scope is availabe during the execution lifespan of a custom tag. Rfer to the ColdFusion Livedocs for additional scopes available to custom agas, as well as how scopes are handled i nested custom tags. 
- Local (function): The Local scope may be referenced explicitly, or defined using the var keyword. Variables in this scope are private to the current funciton context. This scope is mutally exclusive with the arguments scope, and may not contain the same variable names as the arguments scope. 

To reference scoped variables, preface the variable pointer with the scope in dot-notation. For example, to access a variable named `myVar` in the `Application` scope, we would write `application.myVar`. 
It is best practice to scope all variables but is not necessary.
If the scope is not provided, ColdFusion will search for the variable in the scopes in the following order:

1. Arguments
2. Local (function-local, UDFs and CFCs only)
3. Thread local (inside threas only)
4. Query ( not a true scope; variables in query loops
5. Thread
6. Variables
7. CGI
8. CFFile
9. URL
10. Form
11. Cookie
12. Client

Some scopes are not included in this and have to be explicitly scoped. Those are the following:

- This (public scope of a ColdFusion component)
- Request
- Application
- Session
- Server

 
