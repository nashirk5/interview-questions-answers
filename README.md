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

### Q 1. What is HTML?

HTML stands for **_HyperText Markup Language_**. It is a standard text formatting language used for developing web pages released in 1993. HTML is a language that is interpreted by the browser and it tells the browser what to display and how to display.

### Q 2. What are Tags, Elements and Attributes?

- **Tags:** Tags are the starting and ending parts of an HTML element. They begin with < symbol and end with > symbol. Whatever is written inside < and > are called tags.\
  `<a></a>`
- **Elements:** Elements enclose the contents in between the tags. They consist of structure or expression. It generally consists of a start tag, content, and an end tag.\
  `<a>This is the content</a>`
- **Attributes:** Attribute is used to provide extra or additional information about an element.\
  `<a href="#">This is the content</a>`

### Q 3. What are Semantic Elements?

Semantic HTML elements are those that clearly describe their meaning in a human- and machine-readable way

- `<header>`
- `<nav>`
- `<footer>`
- `<section>`
- `<article>`

### Q 4. What are HTML APIs?

- **Geolocation -** It is used to get the geographical position of a user\
- **Drag and Drop -** In HTML, any element can be dragged and dropped.
- **Web Storage -** With web storage, web applications can store data locally within the user's browser.\
  `LocalStorage` and `SessionStorage`
- **Web Workers -** A web worker is a JavaScript running in the background, without affecting the performance of the page.
- **SSE -** Server-Sent Events (SSE) allow a web page to get updates from a server.

### Q 5. What is the difference between Cookie, Local storage and Session storage?

|                | Cookie       | Local storage | Session storage        |
| -------------- | ------------ | ------------- | ---------------------- |
| **Capacity**   | 4KB          | 10MB          | 5MB                    |
| **Expiration** | Manually set | Never         | On tab/browser close   |
| **Read**       | Client       | Client        | Both Client and Server |

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

<!-- Start CSS -->

## **CSS**

### Q 1. What is CSS?

CSS stands for **_Cascading Style Sheets_**. It is a style sheet language, which is used to describe the look and formatting of a document written in **_HTML_**.

### Q 2. What is the Box model in CSS?

The CSS box model is a container that contains multiple properties like content, padding, border and margin. It is used to create the design and layout of web pages.

![css_box_model](src/assets/images/css_box_model.png)

### Q 3. What are Pseudo class and Pseudo element?

- **Pseudo class** is used to define the special state of an element like when the user is hovering over the link.
  - :hover
  - :active
  - :focus
  - ```css
    a: hover {
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

### Q 4. What is a z-index?

It is used to define the order of elements if they overlap with each other.\
Syntax

> z-index: auto | number | initial | inherit;

- auto: The stack order is equal to that of the parent(default).
- number: The stack order depends on the number.
- initial: Sets the property to its default value.
- inherit: Inherits the property from the parent element.

![css_z_index](src/assets/images/css_z_index.png)

### Q 5. Explain CSS Absolute and Relative position property?

position: relative places an element relative to its current position without changing the layout around it, whereas position: absolute places an element relative to its parent’s position and changing the layout around it

- **Absolute:** Position absolute places an element relative to its parent’s position and changing the layout around it.
- **Relative:** Position relative places an element relative to its current position without changing the layout around it.

![css_positions](src/assets/images/css_positions.png)

### Q 6. How to center align a div inside another div?

```html
<div class="”outer”">
  <div class="”inner”">your content</div>
</div>
```

```css
/* First method */
.outer {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Second method */
.outer {
  display: grid;
  place-content: center;
}
```

### Q 7. How can we make our website responsive using CSS?

Media query is used to create a responsive web design. It means that the view of a web page differs from system to system based on screen or media types.

- Width and height of the viewport
- Width and height of the device
- Orientation
- Resolution

Syntax

```css
/* @media not|only mediatype and (mediafeature and|or|not mediafeature) */
@media only screen and (max-width: 600px) {
  /* CSS-Code; */
}
```

### Q 8. How to change the color for even and odd list items?

```css
/* Change the background color odd in list ex. 1,3,5,7  */
tr:nth-child(odd) {
  background-color: lightblue;
}

/* Change the background color even in list ex. 2,4,6,8  */
tr:nth-child(even) {
  background-color: lightgreen;
}

/* Change the background color to specific item in a list  */
tr:nth-child(4) {
  background-color: lightcoral;
}
```

### Q 9. What is CSS flexbox, and what are its properties?

It is also called a flexible box model. It is basically a layout model that provides an easy and clean way to arrange items within a container. Flexbox is different from the block model which is vertically biased and the inline which is horizontally biased. Flexbox was created for small-scale layouts and there’s another standard called grids which are geared more towards larger-scale layouts, It works similar to the way to Twitter bootstrap grid system works. Flexbox is responsive and mobile-friendly. To start with flexbox firstly create a flex container. To create a flex container set the display property to flex.

**Flex Properties:**

- **flex-direction:** row, column, row-reverse, column-reverse
- **flex-wrap:** wrap, nowrap, wrap-reverse
- **flex-flow:** This property is used for setting both flex-direction and flex-wrap properties in one statement
- **justify-content** center, flex-start, flex-end, space-around, space-between
- **align-items** This is used for aligning flex items
- **align-content** This is used for aligning the flex lines

### Q 10. What is CSS Grid?

It is a CSS property that offers a grid-based layout system, with rows and columns, making it easier to design web pages without floats and positioning.

Syntax:

> grid:none|grid-template-rows / grid-template-columns|grid-template-areas|\
> grid-template-rows / [grid-auto-flow] grid-auto-columns|[grid-auto-flow]
> grid-auto-rows / grid-template-columns|initial|inherit;

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##

<!-- Start JavaScript -->

## **JavaScript**

<!-- ### Q. Array Methods

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
| **. indexOf('e)**      | _1_ - Providing the index of the first appearance of a given text inside the string | -->

<div align="right"><b><a href="#table-of-contents">↥ Back to top</a></b></div>

##

<!-- Start Angular -->

## **Angular**

### Q 1. What is Angular?

Angular is an open-source single-page web application framework built on TypeScript, which makes it easy to build web, and mobile applications.

### Q 2. What are the Angular lifecycle hooks?1

1. **ngOnChanges():** This hook is called whenever one or more input properties of the component change. This method/hook receives a SimpleChanges object that contains the previous and current values of the property.
2. **ngOnInit():** It initializes the component and sets the input properties of the component.
3. **ngDoCheck():** This is for the detection and to act on changes that Angular can't detect.
4. **ngAfterContentInit():** This is called in response after Angular projects external content into the component's view.
5. **ngAfterContentChecked():** This is called in response after Angular checks the content projected into the component.
6. **ngAfterViewInit():** This is called in response after Angular initializes the component's views and child views.
7. **ngAfterViewChecked():** This is called in response after Angular checks the component's views and child views.
8. **ngOnDestroy():** This is the cleanup phase just before Angular destroys the directive/component.

### Q 3. What are the building blocks of angular?

1. Components
2. Modules
3. Services
4. Metadata
5. Decorators
6. Directives
7. Data Binding
8. Pipes
9. Dependency Injection
10. Templates

### Q 4. What is Component?

Components are the basic building blocks, which control a part of the UI. A component is defined with a **@Component** decorator. Every component consists of three parts.

- **Template:** which loads the view for the component
- **Stylesheet :** which defines the look and feel for the component
- **Class :** a class contains the business logic for the component

```typescript
import { Component, OnInit } from '@angular/core';
@Component({
  selector: 'app-test',
  templateUrl: './test.component.html',
  styleUrls: ['./test.component.css']
})
export lass TestComponent implements OnInit {
  constructor() {}
  ngOnInit() {
  }
}
```

### Q 5. What is Module?

A module is a place where we can group components, directives, services, and pipes. A module is defined with a **@NgModule** decorator. By default, modules are of two types.

- **Root Module:**
- **Feature Module:**

> _Every application can have only one root module whereas, it can have one or more feature modules._

```typescript
import { BrowserModule } from "@angular/platform-browser";
import { NgModule } from "@angular/core";

import { AppComponent } from "./app.component";
import { TestComponent } from "./test/text.component";

@NgModule({
  declarations: [AppComponent, TestComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

### Q 6. What is Service?

Services are objects which get instantiated only once during the lifetime of an application. The main objective of a service is to share data, functions with different components of an Angular application. A service is defined with a **@Injectable** decorator.

```typescript
import { Injectable } from "@angular/core";
@Injectable({
  providedIn: "root",
})
export class TestServiceService {
  constructor() {}
}
```

### Q 7. What is Metadata?

Metadata is used to decorate a class so that it can configure the expected behavior of the class. The metadata is represented by decorators

### Q 8. What is Decorators?

Decorators are design patterns used to decoration of a class without modifying the source code.

There are four main types of angular decorators:

1. **Class Decorators:** e.g. @Component and @NgModule

```typescript
import { NgModule, Component } from "@angular/core";
// Component
@Component({
  selector: "my-component",
  template: "<div>This is a class component!</div>",
})
export class MyComponent {
  constructor() {
    console.log("This is a class component!");
  }
}

// Module
@NgModule({
  imports: [],
  declarations: [],
})
export class MyModule {
  constructor() {
    console.log("This is a class module!");
  }
}
```

2. **Property Decorators:** e.g. @Input() and @Output()

```typescript
import { Component, Input } from "@angular/core";

@Component({
  selector: "my-component",
  template: "<div>This is a test component!</div>",
})
export class MyComponent {
  @Input() title: string;
}

// The input binding would be sent via a component property binding:
<prop-component [propProperty]="propData"></prop-component>
```

3. **Method Decorators:** e.g. @HostListener()

```typescript
import { Component, HostListener } from "@angular/core";

@Component({
  selector: "my-component",
  template: "<div>This is a test method component!</div>",
})
export class MyComponent {
  @HostListener("click", ["$event"])
  onHostClick(event: Event) {
    console.log("clicked now this event is available!");
  }
}
```

4. **Parameter Decorators:** e.g. @Inject()

```typescript
import { Component, Inject } from "@angular/core";
import { MyService } from "./my-service";

@Component({
  selector: "my-component",
  template: "<div>Parameter decorator</div>",
})
export class MyComponent {
  constructor(@Inject(MyService) myService) {
    console.log(myService); // MyService
  }
}
```

### Q 9. What is Directive?

Directives are used add behaviour to an existing DOM element or an existing component instance.

**Types of directives:**

1. **Component directives:** These are directives with a template.
2. **Structural directives:** These directives change the DOM layout by adding and removing DOM elements. Ex. **`ngIf`, `ngFor`,** and **`ngSwitch`**.
3. **Attribute Directives:** These directives change the appearance or behavior of an element, component, or another directive. Ex. **`ngClass`** and **`ngStyle`**.

### Q 10. Write a custom Directive

```typescript
import { Directive, AfterViewInit, ElementRef } from "@angular/core";

@Directive({
  selector: "[appAutofocus]",
})
export class AutofocusDirective {
  constructor(private el: ElementRef) {}

  ngAfterViewInit() {
    this.el.nativeElement.focus();
  }
}
```

In the HTML page you can use it like a below

```html
<input formControlName="search" appAutofocus type="text" />
```

### Q 11. What is Data Binding

Data binding define communication between a component and template, making it very easy to define interactive applications without worrying about pushing and pulling data.

There are Four types of Data binding

1. **Interpolation / One way data biding {{ value }}:** Adds the value of a property from the component.

```html
<p>Name: {{ title }}</p>
<p>{{ 1 + 1 }}</p>
```

2. **Two-way data binding [(ngModel)] = "value":** Two-way data binding allows to have the data flow both ways. For example, in the below code snippet, both the email DOM input and component email property are in sync

```html
<input type="text" [(ngModel)]="title" />
```

3. **Property binding [property] = "value":** The value is passed from the component to the specified property or simple HTML attribute

```html
<input type="text" [disabled]="isDisabled" />
```

4. **Event binding (event) = "function":** When a specific DOM event happens (eg.: click, change, keyup), call the specified method in the component

```html
<button (click)="onClick()"></button>
```

### Q 12. What are Pipes?

Pipes are simple functions that use template expressions to accept data as input and transform it into a desired output. For example, let us take a pipe to transform a component's text into upper case using uppercase pipe. Ex. `DatePipe`, `UpperCasePipe`, and `CurrencyPipe`

```html
<p>Hello {{ name | uppercase }}</p>
```

### Q 13. Difference between Pure and Impure pipe?

A pure pipe is only called when Angular detects a change in the value or the parameters passed to a pipe. For example, any changes to a primitive input value (String, Number, Boolean, Symbol) or a changed object reference (Date, Array, Function, Object). An impure pipe is called for every change detection cycle no matter whether the value or parameters changes. i.e, An impure pipe is called often, as often as every keystroke or mouse-move.

### Q 14. What is the async pipe?

The AsyncPipe subscribes to an observable or promise and returns the latest value it has emitted. When a new value is emitted, the pipe marks the component to be checked for changes.

Let's take a time observable which continuously updates the view for every 2 seconds with the current time.

```typescript
@Component({
  selector: "async-observable-pipe",
  template: `<div>
    <code>observable|async</code>: Time: {{ time | async }}
  </div>`,
})
export class AsyncObservablePipeComponent {
  time: Observable<string>;
  constructor() {
    this.time = new Observable((observer) => {
      setInterval(() => {
        observer.next(new Date().toString());
      }, 2000);
    });
  }
}
```

### Q 15. What is dependency injection?

Dependency Injection (DI) allows a class to receive dependencies from another class. Most of the time in Angular, dependency injection is done by injecting a service class into a component or module class.

_TestService.ts_

```typescript
import { Injectable } from "@angular/core";

@Injectable()
export class TestService {
  constructor() {}

  login(data) {
    // Call api
  }
}
```

_AppComponent.ts_

```typescript
import { Component } from "@angular/core";
import { TestService } from "./test.service";

@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
  providers: [TestService],
})
export class AppComponent {
  constructor(private testSrv: TestService) {}

  submit() {
    this.testSrv.login(data);
  }
}
```

### Q 16. How do you share data between components?

### Q 17. What are ng-template, ng-container, and ng-content?

- **`ng-template`**
  - It is used to define templates that can be reused or conditionally rendered.
  - ```html
    <ng-template #myTemplate>Your template content here</ng-template>
    ```
- **`ng-container`**
  - It is used to group elements together without adding an extra element to the DOM.
  - ```html
    <ng-container *ngIf="data">Your template content here</ng-container>
    ```
- **`ng-content`**

  - It is used to content projection, allowing the parent component to inject content into a child component.
  - ```html
    <!-- Child component template -->
    <div class="child-component">
      <ng-content></ng-content>
    </div>

    <!-- Parent component template -->
    <app-child>
      <p>Content projected into child component</p>
    </app-child>
    ```

### Q 18. What is view encapsulation?

View encapsulation specifies if the component's template and styles can impact the entire program or vice versa.

**Angular offers three encapsulation methods:**

- **Emulated (Default):** Styles defined within a component's CSS file are scoped to that component only and do not affect the global styles.
- **Native (Shadow DOM):** Shadow DOM provides true encapsulation by creating a separate DOM subtree for each component and encapsulating the styles within that subtree.
- **None:** This is useful when you want to apply global styles or when you need to style elements outside of the component's view encapsulation boundary

Example:

```typescript
@Component({
  templateUrl: 'card.html',
  styles: [`
    .card {
      height: 70px;
      width: 100px;
    }
  `],
  encapsulation: ViewEncapsulation.Native
  // encapsulation: ViewEncapsulation.None
  // encapsulation: ViewEncapsulation.Emulated is default
})
```

### Q 19. How do you define routes?

In Angular, a route refers to navigating between different components or views.

```typescript
const appRoutes: Routes = [
  { path: "todo/:id", component: TodoDetailComponent },
  {
    path: "todos",
    component: TodosListComponent,
    data: { title: "Todos List" },
  },
  { path: "", redirectTo: "/todos", pathMatch: "full" },
  { path: "**", component: PageNotFoundComponent },
];

@NgModule({
  imports: [
    RouterModule.forRoot(
      appRoutes,
      { enableTracing: true } // <-- debugging purposes only
    ),
  ],
})
export class AppModule {}
```

### Q 20. What is the purpose of Wildcard route?

If the URL doesn't match any predefined routes then it causes the router to throw an error and crash the app. In this case, you can use wildcard route. A wildcard route has a path consisting of two asterisks to match every URL.

**Example**

```typescript
  { path: '**', component: PageNotFoundComponent }
```

### Q 21. What is an interceptor?

In Angular, an interceptor is a service that provides a way to intercept HTTP requests or responses before they are sent to the server or received by the application. Interceptors are typically used to modify or augment HTTP requests or responses, add headers, handle errors, or perform other operations that need to be applied globally across multiple HTTP requests.

**_auth.interceptor.ts_**

```typescript
import { Injectable } from "@angular/core";
import {
  HttpInterceptor,
  HttpRequest,
  HttpHandler,
  HttpEvent,
} from "@angular/common/http";
import { Observable } from "rxjs";

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(
    request: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    // Get the authentication token from wherever you store it (e.g., localStorage)
    const authToken = localStorage.getItem("authToken");

    // Clone the request and add the Authorization header if the token exists
    if (authToken) {
      request = request.clone({
        setHeaders: {
          Authorization: `Bearer ${authToken}`,
        },
      });
    }

    // Pass the modified request to the next handler
    return next.handle(request);
  }
}
```

**_app.module.ts_**

```typescript
import { NgModule } from "@angular/core";
import { HttpClientModule, HTTP_INTERCEPTORS } from "@angular/common/http";
import { AuthInterceptor } from "./auth.interceptor";

@NgModule({
  imports: [HttpClientModule],
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: AuthInterceptor,
      multi: true,
    },
  ],
})
export class AppModule {}
```

### Q 22. What is an interface?

In Angular, an interface is a TypeScript feature used to define the structure of objects. It acts as a contract that describes the properties and methods an object must have in order to be considered of that type. Interfaces are commonly used to enforce type-checking and provide better code readability and maintainability

```typescript
// Define the User interface
export interface User {
  id: number;
  username: string;
  email: string;
}

// Example usage of the User interface
const user: User = {
  id: 1,
  username: "john_doe",
  email: "john@example.com",
};

// Function that accepts a User object
function printUserInfo(user: User) {
  console.log(
    `ID: ${user.id}, Username: ${user.username}, Email: ${user.email}`
  );
}

// Call the function with the user object
printUserInfo(user);
```

### Q 23. What is lazy loading?

Lazy loading in Angular refers to a technique where modules are loaded asynchronously when they are needed, rather than being loaded all at once when the application starts up. This technique improves the initial loading time and reduces the initial bundle size of the application, as only the essential modules are loaded initially.

```typescript
import { NgModule } from "@angular/core";
import { Routes, RouterModule } from "@angular/router";

const routes: Routes = [
  { path: "home", component: HomeComponent },
  {
    path: "lazy",
    loadChildren: () => import("./lazy/lazy.module").then((m) => m.LazyModule),
  },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

### Q 24. How to optimize loading large data in angular?

1. **AOT:** The Angular Ahead-of-Time (AOT) compiler converts your Angular HTML and TypeScript code into efficient JavaScript code during the build phase before the browser downloads and runs that code. Compiling your application during the build process provides a faster rendering in the browser.
2. **Tree-shaking:** This is the process of removing unused code resulting in smaller build size. In angular-cli, Tree-Shaking is enabled by default.
3. **Lazy loading:** Lazy loading is the mechanism where instead of loading complete app, we load only the modules which are required at the moment thereby reducing the initial load time.
4. **Ivy Render Engine:** It results in much smaller bundle size than the current engine with improved debugging experience.
5. **RxJS:** RxJS makes the whole library more tree-shakable thereby reducing the final bundle size. However, it has some breaking changes like operators chaining is not possible instead, pipe() function (helps in better tree shaking) is introduced to add operators.
6. **Caching:** Implement client-side caching mechanisms, such as browser caching or in-memory caching using libraries like **`ngrx/store`**, to store frequently accessed data locally. This reduces the number of API requests and improves performance.
7. **Pagination:** Instead of loading all data at once, implement pagination to fetch and display data in smaller, manageable chunks. This reduces the initial load time and enhances the responsiveness of your application.
8. **Infinite Scrolling:** Implement infinite scrolling, where data is loaded dynamically as the user scrolls down the page. This provides a seamless user experience by continuously loading data without requiring the user to navigate through pagination controls.
9. **Progressive Loading:** Load data progressively by initially displaying a placeholder or summary information while fetching the complete dataset in the background. This gives users immediate feedback and improves perceived performance.
10. **Optimize Rendering:** Optimize rendering performance by minimizing DOM manipulations, avoiding unnecessary re-renders, and utilizing Angular features like OnPush change detection strategy and trackBy function for ngFor loops.

### Q 25. What is AOT and JIT?

- **JIT:** Just-in-Time (JIT) is a type of compilation that compiles your app in the browser at runtime, as the application is being loaded. .
- **AOT:** Ahead-of-Time (AOT) is a type of compilation that compiles your app at build time, before the application is deployed to the client's browser.

_AOT compilation offers better performance, smaller bundle sizes, and improved error detection compared to JIT compilation. It is the recommended compilation mode for production deployments of Angular applications. JIT compilation, on the other hand, provides faster development cycles and is suitable for development and testing environments._

> **NOTE:** **JIT** compilation was the default until **Angular 8**, now default is **AOT**

### Q 26. What are Observables and Promises?

### Q 27. What is RXJS and list some operators?

### Q 28. What is the difference between Subject, Behavior subject, and Replay subject?

### Q 29. What is NGRX?

### Q 30. What is a standalone component?

### Q 31. What is Async/await?

### Q 32. What are the advantages of Angular?

### Q 33. What are Template and Reactive forms?

### Q 34. What is angular change detection?

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
