---
layout: post
title:      "JS fundamentals, VAR | LET | CONST | "THIS""
date:       2018-08-17 18:00:23 +0000
permalink:  js_fundamentals_var_let_const_this
---


Let's quickly review scope & hosting.

# Scope/Hoisting 
**Scope** refers to the current context of code, which determines the accessibility of variables. There are two types of scope, local and global:

> * Global variables are those declared outside of a block
> 
> * Local variables are those declared inside of a block
> 


**Hositing** is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.

AKA no matter where in your code the functions and variables are *declared*, they are "moved" to the top of their scope.
*Hoisting only moves the delcaration, assignments are left in place* (BTW these are not physically moved)

MDN says it best, 
> the variable and function declarations are put into memory during the *compile* phase, but stay exactly where you typed them in your code.


**Hoisting Example Using Global Scope**

> ```
> console.log(bowser);
> 
> var bowser = "The king of the castle"
> 
> ```

What is the expected output?

> ```
> 
>  undefined
> 
> ```

Why?!

Imagine in hoisting this is actually how it is interpreted...

> ```
> 
> var bowser;
> 
> console.log(bowser);
> boswer = "The king of the castle"
> 
> ```


*Tisk Tisk*, Don't forget to **declare** and **initalise** your variables before use. 

INSERT PHOTO?

Time for....
# Var

First up,  the OG "var". 

> The **var** statement declares a variable, optionally initializing it to a value.
> -MDN

Var is becoming an "old script" and is begininng to be replaced by "let" (we will talk about let later) but that doesn't mean var is going anywhere anytime soon so get to know it. 

Var in global scope:

> ```
> var game = "super mario"
> 
>game
>
> ```

Output:

>  super mario
> 
>   // game is accessible within the global scope.


Example of local, function-scoped var.

> ```
>  function game() {
> for (var i = 0; i < 5; i++) {
> if (true) {
> var player = 'peach';
> }
> }
> console.log(player)
> }
> 
> game();
> ```

Output:

>  peach
> 
>  // player is accessible  within the function because it is function-scoped


Now let's see a global and local var...

>```
>      //*Initialize a global variable*  
> var player = "mario";
> 
> function character() {
>       // *Initialize a local, function-scoped variable*
> var player = "yoshi";
> console.log(player);
> }
> 
>        //* Log the global and local variable*
>        
> console.log(player);
> character();
 >console.log(player);
 >```


Output:

> mario <br>
> yoshi <br>
> mario
> 
> // The local variable  "yoshi" is function-scoped. That means it is not accessible from the global scope.

 Head spinning? Great! Let's move on. 

# Let
Variables declared by *let* have their scope in the block for which they are defined, as well as in any contained sub-blocks. In this way, *let* works very much like var. Although, unlike var it does not create a property on the global object regardless of where you define it.

When you declare a variable by *let* that variable’s scope will be the block in which it is declared. The block can be that of a function, if statement, switch statement, while statement, or any other block that exists in javascript. In conclusion: the value of the variable defined by *let* will not escape the block that it is declared in. 


> The let statement declares a block scope local variable, optionally initializing it to a value. -MDN





|Variables | Scope | Hoisting | Reassigned? | Redeclared |
| -------- | -------- | -------- | -------- | -------- | -------- |
| ***var***     | Function      | Yes     | Yes     | Yes      | 
| ***let***     | Block    | No   | Yes     | No    | 
| ***const***     | Block      | No     | No    | No      |

