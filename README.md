# All important Interview Questions and Answers

## Table of Contents

- [HTML](#html)
- [CSS](#css)
- [JavaScript](#javascript)
- [Angular](#angular)
- [NodeJs](#nodejs)
- [MySQL](#mysql)
- [JavaScript basic programs](#javascript-basic-programs)

<!-- Start HTML -->

## **HTML**

### Q 1. What is HTML ?

HTML stands for **_HyperText Markup Language_**. It is a standard text formatting language used for developing web pages released in 1993. HTML is a language that is interpreted by the browser and it tells the browser what to display and how to display.

![Box model](src/assets/images/html_release_year.png)

### Q 2. What are Tags, Elements and Attributes ?

- **Tags:** Tags are the starting and ending parts of an HTML element. They begin with < symbol and end with > symbol. Whatever is written inside < and > are called tags.\
  `<a></a>`
- **Elements:** Elements enclose the contents in between the tags. They consist of some kind of structure or expression. It generally consists of a start tag, content, and an end tag.\
  `<a>This is the content</a>`
- **Attributes:** Attribute is used to provide extra or additional information about an element.\
  `<a href="#">This is the content</a>`

### Q 3. What is Semantic Elements ?

Semantic HTML elements are those that clearly describe their meaning in a human- and machine-readable way

- `<header>`
- `<nav>`
- `<footer>`
- `<section>`
- `<article>`

### Q 4. What are HTML APIs ?

- **Geolocation -** It is used to get the geographical position of a user\
- **Drag and Drop -** In HTML, any element can be dragged and dropped.
- **Web Storage -** With web storage, web applications can store data locally within the user's browser.\
  `LocalStorage` and `SessionStorage`
- **Web Workers -** A web worker is a JavaScript running in the background, without affecting the performance of the page.
- **SSE -** Server-Sent Events (SSE) allow a web page to get updates from a server.

### Q 5. What are the difference between Cookie, Local storage and Session storage ?

|                | Cookie       | Local storage | Session storage        |
| -------------- | ------------ | ------------- | ---------------------- |
| **Capacity**   | 4KB          | 10MB          | 5MB                    |
| **Expiration** | Manually set | Never         | On tab/browser close   |
| **Read**       | Client       | Client        | Both Client and Server |

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

<!-- Start CSS -->

## **CSS**

### Q 1. What is CSS ?

CSS stands for **_Cascading Style Sheets_**. It is a style sheet language which is used to describe the look and formatting of a document written in **_HTML_**.

### Q 2. What is the Box model in CSS ?

The CSS box model is a container that contains multiple properties like content, padding, border and margin. It is used to create the design and layout of web pages.

![Box model](src/assets/images/css_box_model.png)

### Q 3. What are Pseudo class and Pseudo element ?

- **Pseudo class** is used to define the special state of an element like when the user is hovering over the link.
  - :hover
  - :active
  - :focus
  - ```css
    a:hover {
      color: #FFOOFF;
    }
    ```
- **Pseudo element** is used to add style to specified parts of an element. Example: Using style before or after an element
  - ::before
  - ::after
  - ::first-letter
  - ```css
    p::first-line {
      color: #ffOOOO;
    }
    ```

### Q 4. What is a z-index ?

It is used to define the order of elements if they overlap on each other.\
Syntax

> z-index: auto | number | initial | inherit;

- auto: The stack order is equal to that of the parent(default).
- number: The stack order depends in the number.
- initial: Sets the property to its default value.
- inherit: Inherits the property from the parent element.

<div align="center"><img src="src/assets/images/css_z_index.png" height="400"/></div>

### Q 5.

### Q 6.

### Q 7.

### Q 8.

### Q 9.

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##

<!-- Start JavaScript -->

## **JavaScript**

### Q. Array Methods

| Method           | Description                                                            |
| ---------------- | ---------------------------------------------------------------------- |
| **. pop()**      | Removes the last element of an array, and returns that element         |
| **. shift()**    | Removes the first element of an array, and returns that element        |
| **. push()**     | Add new elements to the end of an array, and returns the new length    |
| **. unshift()**  | Adds new elements to the start of an array, and returns the new length |
| **. join()**     | Returns a new string by concatenating all of the elements in an array  |
| **. sort()**     | Sorting the array elements based on some condition                     |
| **. reverse()**  | Reversing the order of the elements in an array                        |
| **. slice()**    | Pulling a copy of a part of an array into a new array                  |
| **. toString()** | Converting the array elements into strings                             |

### Q. String Methods

> Ex: _Hello_

| Method                 | Description                                                                         |
| ---------------------- | ----------------------------------------------------------------------------------- |
| **. toLowerCase()**    | _hello_ - Converting strings to lower case                                          |
| **. toUpperCase()**    | _HELLO_ - Converting strings to upper case                                          |
| **. length()**         | _5_ - Count the characters                                                          |
| **. charAt(2)**        | _l_ - Returning the character at a particular index of a string                     |
| **. concat(' world')** | _Hello world_ - Joining multiple strings into a single string                       |
| **. indexOf('e)**      | _1_ - Providing the index of the first appearance of a given text inside the string |

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##

<!-- Start Angular -->

## **Angular**

### Q 1. What is Angular

### Q What are the building blocks of angular

### Q What are the Angular lifecycle hooks.

### Q What are data binding and how amy types are there

### Q What is directive and how amy types are there

### Q What is pipe and types of pipes

### Q Difference between Pupre and Impure pipe.

### Q What are filters

### Q What is async pipe

### Q How do you share data between components.

### Q What is view encapsulation

### Q What is route and types of routes.

### Q what is interceptor

### Q what is interface

### Q What is lazyloading

### Q What is AOT and JIT

### Q What is Observables and promises

### Q What is RXJS and list some operators

### Q What is the difference between Subject, Behavior subject, Replay subject

### Q What is NGRX

### Q What is standalone component

### Q What is Async/await

### Q What are the decorators

### Q Mention some advantages of Angular

### Q What are Template and Reactive forms

### Q What is dependency injection

### Q What is angular change ditection

### Q Difference between ng-template, ng-container, and ng-content

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##

<!-- Start NodeJS -->

## **NodeJS**

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##

<!-- Start MySQL -->

## **MySQL**

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##

<!-- Start JavaScript basic programs  -->

## **JavaScript basic programs**

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##

<!-- Formatting -->

<!-- [Back to top](#table-of-contents) -->
<!-- <div ><b><a href="#table-of-contents">↥ Back to top</a></b></div> -->
