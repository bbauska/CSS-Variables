# What are CSS Variables and How to Use Them

When writing the CSS code for your site, you can make use of CSS Custom Properties (Variables) to 
speed up the development process. You can use variables to define properties (size, color), which 
can then be applied to several elements.

That way, it is possible to have more control over the code and the design. Altering the value of 
a variable in one place overrides the value of that property everywhere it is invoked. 

This post will explain how to use CSS Variables and some practical applications. 

Let’s start!

## Declaring a Variable

Variables can have global or local scope. To define a variable globally, you use the :root selector.

```
:root {
    --base-font-size: 1.1rem;
} 
```

The :root selector matches the root of the document, that is <html> in our particular case. 

To declare a CSS Custom Property (Variable), you start with two dashes (–). Variables are case sensitive, for example:

```
--base-font-size and --Base-Font-Size are two different variables.
```

To define a variable locally, you use the selector of the element in which you want to use the variable.

```
#first-container {
    --background: #ccc;
}
```

Once you have defined the variable, it is necessary to invoke it. 
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## The var() function
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
The var() function is used to insert the value of the defined CSS Variable. The function replaces 
itself with the value of the variable. Let’s take a look at an example: 

### The HTML Code
Copy and paste this code into your code editor. 
Save the file as index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="/style.css">
	<title>CSS Variables</title>
</head>
<body>
	<div class="wrapper">
    	<div class="container-1">
        	<p class="first">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iste doloribus dolorum eaque veritatis quia quod?</p>
        	<button type="button">Click here!</button>
    	</div>
    	<div class="container-2">
        	<p class="second">Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero, dolorem. Reprehenderit mollitia quos quia qui.</p>
        	<button type="button">Click here!</button>
    	</div>
    	<div class="container-3">
        	<p class="third">Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi dolor reprehenderit, ad sunt aperiam officiis!</p>
        	<button type="button">Click here!</button>
    	</div>
	</div>
</body>
</html>
```

### The CSS Code
Create a file called style.css (in the same directory of index.html).

#### Paste the code below and save the file.

```
/* Global styles */
.wrapper, div {
   padding: 1rem;
}

div {
   margin: 1rem auto;
}

/* DEFINITION OF VARIABLES */
:root {
   /* Color palette */
   --primary: #007bff;
   --success: #28a745;
   --warning: #ffc107;
   --white: #f9f9f9;
   --light-grey: #d8d8d8;

   /* Borders */
   /* It is possible to use an already declared variable within the definition of another variable */
   --border-primary: 1px solid var(--primary);
   --border-success: 1px solid var(--success);
   --border-warning: 1px solid var(--warning);
}

/* VARIABLES */
/* Wrapper */
.wrapper {
   background-color: var(--light-grey);
}

/* First Container */
.container-1 {
   /* The var() function replaces itself with the value of the variable */
   border: var(--border-primary);
   color: var(--primary);
   background-color: var(--white);
}

.container-2 {
   /* The var() function replaces itself with the value of the variable */
   border: var(--border-success);
   color: var(--success);
   background-color: var(--white);
}

.container-3 {
   /* The var() function replaces itself with the value of the variable */
   border: var(--border-warning);
   color: var(--warning);
   background-color: var(--white);
}

.container-1 button {
   background-color: var(--primary);
   color: var(--white);
}

.container-2 button {
   background-color: var(--success);
   color: var(--white);
}

.container-3 button {
   background-color: var(--warning);
   color: var(--white);
}<

button {   border-radius: 5px;
}
```

There are some things to notice here:

Creating a color palette is a straightforward process.
It is possible to use a variable inside the definition of another variable, like the color in the definition of 
the border variables.
Variables are inherited, the color property of the .container-* element affects its direct children. In this case, 
the &lt;p&gt; element. To override a variable, you declare it inside its container, making it more specific.

#### Edit the CSS code:

```
button {
	border-radius: 5px;
	/* Overriding a global variable */
	--primary: #021b35;
}
```

### Variables and Media Queries

Variables can also be inherited and overridden in the CSS media queries.

#### Add this code to the variables:

```
:root {
	/* Color palette */
	--primary: #007bff;
	--success: #28a745;
	--warning: #ffc107;
	--white: #f9f9f9;
	--light-grey: #d8d8d8;


	/* Borders */
	/* It is possible to use an already declared variable within the definition of another variable */
        --border-primary: 1px solid var(--primary);
	--border-success: 1px solid var(--success);
	--border-warning: 1px solid var(--warning);
	/* Width of the wrapper 1000px / 90% on smaller devices */
	--wrapper-width: 1000px;
}
```

We have defined a base width for the wrapper element. We can now apply these variables to the .wrapper width property. 

#### Add this code to the end of the CSS file:

```
.wrapper {
	width: var(--wrapper-width);	margin: 0 auto;
}
```

To define a media query for devices with screens less than 1100px wide, we write the following media query. 

#### Edit the CSS code:

```
@media screen and (max-width: 1100px) {
	.wrapper {
    	--wrapper-width: 90%;
	}
}
```

The new variable definition inside the media query overrides its value. Notice also, that the variable is available in the DOM, which means, it can be retrieved and manipulated with JS. That is not possible with variables within CSS preprocessors.

## Summary
Variables are useful to organize and manage small and large amounts of CSS. They reduce repetition and therefore prevent mistakes. CSS Variables are dynamic, meaning, they can be altered in the runtime. It is easy to theme a site or application dynamically with CSS variables. They provide the ability to assign values to a CSS property with a customized name. Variables follow the standard cascading rules, so it is possible to define the same property at different specificity levels.

I hope you liked this tutorial. Thanks for reading!    

# DOM Tree

Happy holidays! I didn't get a pine tree for Christmas this year so I decided to compensate by creating a digital counterpart out of HTML form elements.

[Check out the live demo](http://hakim.se/experiments/css/domtree).

[Check out the live demo](http://bauska.org/domtree).

# License

MIT licensed

Copyright (C) 2017 Hakim El Hattab, http://hakim.se
