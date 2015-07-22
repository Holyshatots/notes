---
layout: note
title: ColdFusion Day 3
date: 2015-02-14 15:57:24 -0700
categories: ColdFusion
---

# Day 3: Looping

## Tag-based Looping

```
<cfloop from="1" to "5" index="i">
	#i#<br />
</cfloop>
```

The loop will increase from 1 to 5. It defaults to counting by 1, but can be overidden by using `step`.

Looping over an array:

```
<cfset myArray = ['Jeff', 'John', 'Steve', 'Julianne'] />

<cfloop from="1" to "#arrayLen(myArray)#" index="i">
	#i#:#myArray[i]#<br />
</cfloop>
```
Or

In this case index refers to current item in the array that it is on.

```
<cfloop array="#myArray#" index="item">
	#item<br />
</cfloop>
```

Looping over a list:

```
<cfset myList = 'Jeff,John,Steve,Juliane' />
<cfloop list="#myList#" index="item">
	#item#<br />
<cfloop>
```
