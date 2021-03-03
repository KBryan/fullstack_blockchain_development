# Full Stack Blockchain dApp Development

# Short Summary
It has been debated in the blockchain space. That the biggest hardle to mass adoption of cryptocurrencies is how users experience it. Currently, this is a fragmented experience. I don't claim to solve all these problems. Although, I do make attempts to show the developer where dApp developers need to make different decisions then they would make in traditional client/server design patterns. Our user interface will comprise of purely HTML5 / CSS3 and TypeScript. 

#Requirements
Some prior knowledge of Web Development basics would be beneficial in following these solutions. There will be provided additional resource material for the user if they wish to further their understanding of the subject.<br>
[W3C HTML / CSS / Javascript Primer](https://www.w3schools.com/html/default.asp) <br>
[TypeScript Tutorial Primer](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

# What is TypeScript and Why should we use it ?

TypeScript is an object-oriented programming language developed and maintained by Microsoft. It's a superset of JavaScript, meaning that any valid `JavaScript` code will also run as expected in `TypeScript`. An important point to understand is that if you just know Javascript you can start using TypeScript as it compiles down to native Javascript.

TypeScript has all of the functionality of JavaScript as well as some additional features. It needs to be compiled to plain JavaScript during runtime, therefore you need a compiler to get back the JS Code.<br>

TypeScript uses static typing, meaning that you can give a type to a variable during declaration. And it's something that can't be done with JavaScript because it's a dynamically typed language – it does not know the data type of a variable until it assigns a value to that variable at runtime.

Static type checking makes TypeScript great because it helps to throw an error at compile-time if the variable is unused or reassigned with a different type annotation. However, the error does not block the code from executing (and the JavaScript code will still be generated).

Static typing is optional in TypeScript. If no type is defined but the variable has a value, TypeScript will infer the value as type. And if the variable has no value, the type will be set to any by default.

# Setting up our TypeScript project

TypeScript needs to compile to plain JavaScript. So we need to use a tool to do the compilation. And to have access to that tool, you need to install TypeScript by running this command on the terminal.

```javascript
 yarn add -g typescript
```

Or use npm:
```javascript
npm install -g typescript
```

Note that here I use the -g flag to install TypeScript globally so that I can access it from anywhere.

By installing TypeScript, we have now access to the compiler, and we can compile our code to JavaScript.

# Configuring TypeScript with tsconfig

`tsconfig` is a JSON file that helps configure `TypeScript`. Having a config file is better since it helps control the behavior of the compiler.

To create the config file, you first need to create a new directory named solution0 and browse into the root of the folder. Then, open it on the terminal or an IDE and run this command to generate a new TypeScript configuration file.

```javascript
tsc --init
```
Once the file is generated, we can now explore it on an IDE.

```javascript
tsconfig.json
```

Once the file is generated, we can now explore it on an IDE.
* `tsconfig.json`

```javascript
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "es5",
    "sourceMap": true
  },
  "exclude": [
    "node_modules"
  ]
}
```

target: it specifies the ECMAScript target version when compiling the TypeScript code. Here, we target es5 to support all browsers, you can change it to ES6, ES3(it's the default if no target is specified), ES2020, etc.

module: it defines the module of the compiled code. The module can be Common JS, ES2015, ES2020, etc.

# TypeScript Types

Types provide a way to enhance code quality, and they also make the code easier to understand since it defines the variable types. They are optional, and help define what a given variable should have as its value. They also allow the compiler to catch errors before runtime.

TypeScript has several types such as number, string, boolean, enum, void, null, undefined, any, never, array, and tuple. We won't see all types in this guide, but keep in mind that they exist.

Now, let's see some examples of basic Types.

# Basic TypeScript Types

```typescript
let foo: string = "test"
let bar: number = 1
let baz: string[] = ["This", "is", "a", "Test"]
```

As you can see here, we have three variables with different types. `foo` expects a string, `bar`, a number, and `baz`, an array of a string. If they receive anything else besides the type declared, an error will be thrown by TypeScript.

You can also declare `baz` like this: `let baz: Array<string> = ["This", "is", "a", "Test"]`.

Now, let's try to reassign one of these variables and see how TypeScript behaves.

Now, let's try to reassign one of these variables and see how TypeScript behaves.

```typescript
let foo: string = "test"
foo = 1
```

```typescript
Type '1' is not assignable to type 'string'
```

TypeScript will throw an error because we have already declared foo to expect a string as value. And this error is caught at compile-time which makes TypeScript great and useful.

But you can also declare variables with an implicit type annotation.

```typescript
let foo = "test"
let bar = 1
let baz = ["This", "is", "a", "Test"]
```

TypeScript will try here to infer as much as it can to give you type safety with less code. It will take the value and define it as a type for the variable. And nothing will change regarding errors.

Let's try to reassign these variables to see what will happen.

```typescript
foo = 7
bar = "updated"
baz = [2, true, "a", 10]
```

TypeScript will catch the errors like before, even if variable types are declared implicitly.

When dealing with an object of several properties, it can be tricky and annoying to define the types. But luckily, TypeScript has something to help you along with that use-case. So, let's dive into TypeScript Interfaces and Type aliases in the next section.

# Interfaces and Type aliases

Interfaces and Type aliases help us define the shape of an object-like data structures. They seem like the same thing regarding their structure, but keep in mind that they are different.

However, the consensus amongst developers is to use interface whenever you can since it's in the default tslint ruleset.

Now, let's create an interface and a type alias in the next section to see them in action.

```typescript
interface ITest {
  id: number;
  name?: string;
}

type TestType = {
  id: number,
  name?: string,
}

function myTest(args: ITest): string {
  if (args.name) {
    return `Hello ${args.name}`
  }
  return "Hello World"
}

myTest({ id: 1 })
```

They have to define the form of given data with TypeScript.

Notice that here, I use an optional field name by adding a question mark (?). It lets us make the property name optional. That means if no value is passed to the property name, it will return undefined as its value.

Next, we use the interface ITest as a type for the argument received by the function myTest. And as with variables, functions can also be defined to return a specific type. And here, the return value must be a string otherwise an error will be thrown by TypeScript.

So far, we have covered all the basic knowledge needed to get started with TypeScript. Now we can start building out our shopping dApp.


# Building a Decentralized Shopping dApp

When building a decetralized dApp. You will spend a good amount of time working on the front end to make sure your new users have the best experience possible. A good place to start is to understand how your interface and user experience should work. We are going to build something that will look something similar to the following.

![WireFrame](./img/wireframe.png) <br>

# Creating a Shopping dApp Card

So, let's start by creating three new files in the root of the folder: index.html, style.css, and src/app.ts. And for the configuration of TypeScript, we will use the same tsconfig.json file created earlier.

Now, let's move to the markup part and add some content to the HTML file.

#Markup
* `index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Shopping dApp</title>
  </head>
  <body>
    <main>
      <h1>Shopping dApp</h1>
      <div id="app"></div>
    </main>
    <script src="public/js/app.js"></script>
  </body>
</html>
```

As you can see we have a relatively simple markup. There are two important things to retain though:

* the id `app` of the `div` tag that will be used to append the content using TypeScript, and

* the `script` tag that points to the `public` folder and to be precise the JavaScript file that TypeScript will create for us during compile time.

Besides, the CSS file is a bit long, so I won't cover it – I don't want to waste your time and do want to stay focused on TypeScript. That said, we can now dive into it and start fetching data from the API.

# Display data using TypeScript

We start the TS part by selecting the id app which is the id of the div tag.

* src/app.ts

```typescript
const container: HTMLElement | any = document.getElementById("app")
const items: number = 100

interface IItem {
  id: number;
  name: string;
  image: string;
  type: string;
}
```

Here, we have a type annotation that has not to be covered yet. This is a Union Type which allows having alternative types for a given variable. That means if container is not of type HTMLElement, TypeScript will check again if the value is equal to the type after the pipe (|) symbol and so forth because you can have multiple types.

Next, we have an interface IItem that defines the contents of a IItem object which will be used next in the function responsible for displaying the content.
