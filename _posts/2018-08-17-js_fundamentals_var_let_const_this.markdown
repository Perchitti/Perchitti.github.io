---
layout: post
title:      "JS fundamentals "
date:       2018-08-17 14:00:24 -0400
permalink:  js_fundamentals_var_let_const_this
---

# VAR | LET | CONST | "THIS"

Before we look at variables and "this", let's quickly review scope & hoisting.

# Scope/Hoisting 
**Scope** refers to the current context of code, which determines the accessibility of variables. There are two types of scope, local and global:

> * Global variables are those declared outside of a block
> 
> * Local variables are those declared inside of a block
> 


**Hoisting** is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution.

That is to say, no matter where in your code the functions and variables are *declared*, they are "moved" to the top of their scope.
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

Output:

> 
> 
>  undefined
> 
> 

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


*Tsk Tsk*, Don't forget to **declare** and **initialize** your variables before use. 

INSERT PHOTO?

Time for....
# Var

First up,  the OG "var". 

> The **var** statement declares a variable, optionally initializing it to a value.
> -MDN

Var is becoming an "old script" and is begininng to be replaced by "let" (we will talk about let later) but that doesn't mean var is going anywhere anytime soon, so get to know it. 

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
>  
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

Example in global scope:
​
> ```
> let game = "super mario"
> 
>game
>
> ```
​
Output:
​
>  super mario
> 
>   // game is accessible within the global scope.

Example of local, function-scoped let.

> ```
>  function game() {
>  
> for (var i = 0; i < 5; i++) {
> if (true) {
> let player = 'peach';
> }
> }
> console.log(player)
> }
> 
> game();
> ```

Output:

>  ReferenceError: player is not defined
> 
>  // player is not accessible because it is in a different block from let

The correct way to access player

> ```
>  function game() {
>  
> for (var i = 0; i < 5; i++) {
> if (true) {
> let player = 'peach';
> console.log(player)
> }
> }
> }
> 
> game();
> ```

Output:
>  peach
> 
>  // player is accessible because it is called within the same block
>  


Takeaway:

If let and var were the last pick for dodgeball, I'd pick **let**. (& you should too)
Let can reduce the risk of errors which raises your chances of making it to the dodgeball championship.



# Const

> Constants are block-scoped, much like variables defined using the let statement. The value of a constant cannot change through re-assignment, and it can't be redeclared. -MDN

Const is very straight forward, it is constant, consitent, it will not change. Constants are useful for making it clear to others working within your project that the intended variable should not be reassigned.
*Although const values cannot be reassigned, they are mutable as it is possible to modify the properties of objects delcared with const. 


>```
> const player = 'mario'
> 
> player = 'peach'
> 
> console.log(player)
> ```


Output:
>  Uncaught TypeError: Assignment to constant variable.



Great work! Now that you're familiar with var, let and const let's throw in "this" to mix things up. 


# "this"
Going to be VERY honest with you, *this* is confusing. After you read this short piece, google it for hours, days! Just know, you are not alone and it will take time to understand. Let's begin...

> **this** keyword refers to an object, that object which is executing the current bit of javascript code.

In other words, every javascript function while executing has a reference to its current execution context, called *this*. Execution context means here is how the function is called.

To understand *this* keyword, only we need to know how, when and from where the function is called, does not matter how and where function is declared or defined.

Let's jump into examples

> ```
>  function game() {
>  this.a = 'peach';
>  console.log(a);
>  }
>  game();
>  ```

Output:

> peach
> 

Let's try a different approach

> ```
> var person = {
>     firstName: "Mario",
>     lastName : "Brothers",
>     id       : 1,
>     fullName : function() {
>        return this.firstName + " " + this.lastName;
>     }
> };
> person.fullName();
> ```

Output:

> "Mario Brothers"


Ok 1 more for good luck. 

> ```
> 
> class Player {
> 
>     constructor(name) {
> this.name = name;
>     }
> sayHi() {
> alert(this.name)
> }
> }
> 
> let playerName = new Player("Yoshi");
> playerName.sayHi()
> ```

Output:

> Yoshi

Continue to study *this*. Once you grasp the concept it becomes extrememly beneficial. 



*Bonus notes

**Var** variables can be updated and re-declared within its scope; **let** variables can be updated but not re-declared; **const** variables can neither be updated nor re-declared.



|Variables | Scope | Hoisting | Reassigned? | Redeclared |
| -------- | -------- | -------- | -------- | -------- | -------- |
| ***var***     | Function      | Yes     | Yes     | Yes      | 
| ***let***     | Block    | No   | Yes     | No    | 
| ***const***     | Block      | No     | No    | No      |

