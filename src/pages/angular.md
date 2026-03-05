<!-- Start Angular -->

## **Angular**

<div align="right"><b><a href="../../README.md">↥ Back to home</a></b></div>

### Q 1. What is Angular?

Angular is a popular open-source front-end web framework developed and maintained by Google. It is used to build dynamic, single-page web applications (SPAs). Angular utilizes TypeScript, a superset of JavaScript, and offers a comprehensive set of tools and capabilities like two-way data binding, dependency injection, routing, and component-based architecture..

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 2. What are the Angular lifecycle hooks?

**1. ngOnChanges(changes: SimpleChanges)**

- Called when Angular sets or updates data-bound input properties (@Input()).
- Receives a SimpleChanges object showing previous and current values.

**2. ngOnInit()**

- Called once after the first ngOnChanges.
- Ideal for initialization logic, e.g., fetching data.

**3. ngDoCheck()**

- Called during every change detection cycle.
- Lets you implement custom change detection beyond Angular’s default.

**4. ngAfterContentInit()**

- Called once after Angular projects external content into the component using - `<ng-content>`.

**5. ngAfterContentChecked()**

- Called after every check of projected content.

**6. ngAfterViewInit()**

- Called once after Angular initializes the component’s view and its child views.

**7. ngAfterViewChecked()**

- Called after every check of the component’s view and its children.

**8. ngOnDestroy()**

- Called just before the component/directive is destroyed.
- Ideal for cleanup, e.g., unsubscribing from Observables, detaching event listeners.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 4. What is Component?

Components are the basic building blocks, which control a part of the UI. A component is defined with a **@Component** decorator. Every component consists of three parts.

- **Template:** which loads the view for the component
- **Stylesheet :** which defines the look and feel for the component
- **Class :** a class contains the business logic for the component

```typescript
import { Component, OnInit } from "@angular/core";
@Component({
  selector: "app-test",
  templateUrl: "./test.component.html",
  styleUrls: ["./test.component.css"],
})
export class TestComponent implements OnInit {
  constructor() {}
  ngOnInit() {}
}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 5. What is Module?

A module is a place where we can group components, directives, services, and pipes. A module is defined with a **@NgModule** decorator. By default, modules are of two types.

- **Root Module:**
- **Feature Module:**

> _**NOTE:** Every application can have only one root module whereas, it can have one or more feature modules._

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 7. What is Metadata?

Metadata is used to decorate a class so that it can configure the expected behavior of the class. The metadata is represented by decorators

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 9. What is Directive?

Directives are used add behaviour to an existing DOM element or an existing component instance.

**Types of directives:**

1. **Component directives:** These are directives with a template.
2. **Structural directives:** These directives change the DOM layout by adding and removing DOM elements. Ex. **`ngIf`, `ngFor`,** and **`ngSwitch`**.
3. **Attribute Directives:** These directives change the appearance or behavior of an element, component, or another directive. Ex. **`ngClass`** and **`ngStyle`**.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 12. What are Pipes?

Pipes are simple functions that use template expressions to accept data as input and transform it into a desired output. For example, let us take a pipe to transform a component's text into upper case using uppercase pipe. Ex. `DatePipe`, `UpperCasePipe`, and `CurrencyPipe`

```html
<p>Hello {{ name | uppercase }}</p>
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 13. Difference between Pure and Impure pipe?

A pure pipe is only called when Angular detects a change in the value or the parameters passed to a pipe. For example, any changes to a primitive input value (String, Number, Boolean, Symbol) or a changed object reference (Date, Array, Function, Object). An impure pipe is called for every change detection cycle no matter whether the value or parameters changes. i.e, An impure pipe is called often, as often as every keystroke or mouse-move.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 15. How to create a custom pipe?

**Example FilterPipe (Search Functionality)**

**🔹 Step 1: Generate Pipe**

```js
ng generate pipe filter
```

**🔹 Step 2: Implement the Pipe**

```js
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter',
  standalone: true
})
export class FilterPipe implements PipeTransform {

  transform(items: any[], searchText: string, field: string): any[] {
    if (!items || !searchText) return items;

    searchText = searchText.toLowerCase();

    return items.filter(item =>
      item[field]?.toLowerCase().includes(searchText)
    );
  }

}
```

**🔹 Step 3: Use in Template**

```html
<input type="text" [(ngModel)]="searchText" placeholder="Search users" />

<li *ngFor="let user of users | filter:searchText:'name'">{{ user.name }}</li>
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 16. What is dependency injection?

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 17. How do you share data between components?

**1. Input/Output Binding:** You can pass data from a parent component to a child component using input bindings (@Input decorator) and receive data back from the child using output bindings (@Output decorator with EventEmitter).

**2. Service:** You can create a service and inject it into the components that need to share data. The service acts as a central place to store and manage the shared data.

**3. RxJS Observables/Subjects:** You can use RxJS Observables or Subjects to create a data stream that multiple components can subscribe to. This allows for more complex scenarios like bi-directional communication and handling asynchronous data.

### Q 18. What are ng-template, ng-container, and ng-content?

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 19. What is view encapsulation?

View encapsulation specifies if the component's template and styles can impact the entire program or vice versa.

**Angular offers three encapsulation methods:**

- **Emulated (Default):** Styles defined within a component's CSS file are scoped to that component only and do not affect the global styles.
- **Native (Shadow DOM):** Shadow DOM provides true encapsulation by creating a separate DOM subtree for each component and encapsulating the styles within that subtree.
- **None:** This is useful when you want to apply global styles or when you need to style elements outside of the component's view encapsulation boundary

_**Example:**_

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 20. How do you define routes?

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
      { enableTracing: true }, // <-- debugging purposes only
    ),
  ],
})
export class AppModule {}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 21. What is the purpose of Wildcard route?

If the URL doesn't match any predefined routes then it causes the router to throw an error and crash the app. In this case, you can use wildcard route. A wildcard route has a path consisting of two asterisks to match every URL.

_**Example:**_

```typescript
  { path: '**', component: PageNotFoundComponent }
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 22. How do you protect a route and its type?

Angular protects routes using Route Guards like CanActivate, CanActivateChild, CanDeactivate, CanLoad, and CanMatch. CanActivate is most common for authentication, while CanDeactivate prevents navigation with unsaved changes. In modern Angular, CanMatch is preferred over CanLoad for lazy-loaded modules.

**✅ Types of Route Guards**
**1️⃣ CanActivate**

- Controls access before entering a route
- Most commonly used for authentication

**2️⃣ CanActivateChild**

- Protects child routes
- Runs before any child route loads

**3️⃣ CanDeactivate**

- Prevents leaving a route
- Useful for unsaved form changes
- Example use case:
- “Are you sure you want to leave without saving?”

**4️⃣ CanLoad (Legacy Lazy Loading Guard)**

- Prevents lazy-loaded module from loading
- Runs before module is downloaded
- Not recommended in newer Angular versions

**5️⃣ CanMatch (Modern Replacement for CanLoad)**

- Controls whether a route should match
- Used with lazy loading
- Preferred in Angular 15+

| Guard Type       | Purpose                             |
| ---------------- | ----------------------------------- |
| CanActivate      | Protect route before entering       |
| CanActivateChild | Protect child routes                |
| CanDeactivate    | Prevent leaving route               |
| CanLoad          | Prevent lazy module loading (older) |
| CanMatch         | Conditional route matching (modern) |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 23. What is router-outlet and how to create multiple router-outlets?

`router-outlet` is a directive that acts as a placeholder where Angular loads routed components dynamically. By default, there is one primary outlet, but we can create multiple named outlets using the `name` attribute. Named outlets allow rendering multiple routed components simultaneously in different layout sections.

**How to Create Multiple Router-Outlets**

Angular supports multiple outlets using named outlets.

**1️⃣ Default (Primary) Outlet**

```html
<router-outlet></router-outlet>
```

This is called the primary outlet.

**2️⃣ Named Router-Outlets**

You can define additional outlets using the name attribute.

```html
<router-outlet></router-outlet>

<router-outlet name="sidebar"></router-outlet>
```

**3️⃣ Configure Routes for Named Outlets**

```js
{
  path: 'dashboard',
  component: DashboardComponent
},
{
  path: 'help',
  component: HelpComponent,
  outlet: 'sidebar'
}
```

**4️⃣ Navigate to Multiple Outlets**

```js
this.router.navigate([
  {
    outlets: {
      primary: ["dashboard"],
      sidebar: ["help"],
    },
  },
]);
```

Now:

DashboardComponent loads in the primary outlet

HelpComponent loads in the sidebar outlet

**Real-World Use Cases**

- Layout with persistent sidebar
- Chat window + main content

> Node: We can create Only one primary outlet and Multiple named outlets.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 24. What routerLink and active router links?

`routerLink` is a directive used for declarative navigation in Angular without reloading the page. `routerLinkActive` adds CSS classes when the associated route is active. We can use `routerLinkActiveOptions` with `exact: true` to control exact route matching.

**Example:**

```html
<a routerLink="/dashboard">Dashboard</a>

<!-- With parameters: -->
<a [routerLink]="['/user', userId]">View User</a>

<!-- With query params: -->
<a [routerLink]="['/products']" [queryParams]="{ category: 'electronics' }">
  Products
</a>

<!-- routerLinkActive -->
<a routerLink="/dashboard" routerLinkActive="active"> Dashboard </a>
```

**Exact Matching (Important Interview Point)**

By default, Angular does partial matching.

**Example:** `/dashboard/settings` will also activate /dashboard`

To avoid this:

```html
<a
  routerLink="/dashboard"
  routerLinkActive="active"
  [routerLinkActiveOptions]="{ exact: true }"
>
  Dashboard
</a>
```

Now it activates only when exact path matches.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 25. What is an interceptor?

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
    next: HttpHandler,
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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 26. What is an interface?

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
    `ID: ${user.id}, Username: ${user.username}, Email: ${user.email}`,
  );
}

// Call the function with the user object
printUserInfo(user);
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 27. What is lazy loading?

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 28. How to optimize loading large data in angular?

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 29. What is AOT and JIT?

- **JIT:** Just-in-Time (JIT) is a type of compilation that compiles your app in the browser at runtime, as the application is being loaded. .
- **AOT:** Ahead-of-Time (AOT) is a type of compilation that compiles your app at build time, before the application is deployed to the client's browser.

_AOT compilation offers better performance, smaller bundle sizes, and improved error detection compared to JIT compilation. It is the recommended compilation mode for production deployments of Angular applications. JIT compilation, on the other hand, provides faster development cycles and is suitable for development and testing environments._

> _**NOTE: JIT** compilation was the default until **Angular 8**, now default is **AOT**_

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 30. What are Observables and Promises?

**Observable:** In Angular, Observables are a data streaming abstraction provided by the RxJS library. It is used to handle sequence of asynchronous operation or events over time.

```typescript
import { Observable, Observer } from "rxjs";

// Creating an Observable
const observable = new Observable<number>((observer: Observer<number>) => {
  // Emitting values asynchronously
  setTimeout(() => {
    observer.next(1); // Emit first value
  }, 1000);

  setTimeout(() => {
    observer.next(2); // Emit second value
  }, 2000);

  setTimeout(() => {
    observer.next(3); // Emit third value
    observer.complete(); // Complete the observable
  }, 3000);
});

// Subscribing to the Observable
observable.subscribe(
  (value: number) => console.log("Next:", value), // Handle emitted values
  (error: any) => console.error("Error:", error), // Handle errors
  () => console.log("Completed"), // Handle completion
);
```

**Promise:** Promises are used to handle asynchronous operations in javascript

```typescript
let myPromise = new Promise(function (resolve, reject) {
  // "Producing Code" (May take some time)

  resolve(); // when successful
  reject(); // when error
});

// "Consuming Code" (Must wait for a fulfilled Promise)
myPromise.then();
myPromise.catch();
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 31. What are the difference between Promises and Observables?

| Promise                                               | Observable                                                      |
| ----------------------------------------------------- | --------------------------------------------------------------- |
| Emits a single value                                  | Emits multiple values over a period of time                     |
| Eager, meaning they execute immediately upon creation | Lazy, meaning they do not execute until there is a subscription |
| cannot be canceled once they are created              | can be unsubscribed                                             |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 32. What are RXJS and list some operators?

RxJS stands for Reactive Extensions for JavaScript. It’s a library for handling asynchronous data streams using Observables. Instead of working with single values (like a promise), RxJS allows you to work with streams of values over time. Think of it as a way to listen and react to data as it arrives, whether that data comes from user input, HTTP requests, WebSockets, or other sources.

At its core, RxJS provides a way to work with asynchronous data streams (like HTTP requests, events, or user inputs) as collections. You can subscribe to these streams and then use operators (like .map(), .filter(), .merge(), etc.) to manipulate and process the data in a declarative manner.

**Key Concepts in RxJS:**

**1. Observable:** Represents a stream of data or events. You can think of it as a producer that emits values over time.

**2. Observer:** The consumer of the observable stream. An observer subscribes to an observable to receive its values.

**3. Subscription:** The process of linking an observer to an observable. When you subscribe, you start receiving the data from the observable.

**4. Operators:** Functions that enable transformation, combination, or manipulation of data from observables. Some examples include:

- **map:** Transforms the data.
- **filter:** Filters out certain items based on a condition.
- **merge:** Combines multiple observables into one.
- **debounceTime:** Introduces a delay between events.

**5. Subject:** A special type of observable that can also act as an observer. It allows multicasting to multiple subscribers.

**6. Scheduler:** Manages the timing of when certain operations (like emitting values) should occur.

| Area           | Operators                                                     |
| -------------- | ------------------------------------------------------------- |
| Creation       | from,fromEvent, of                                            |
| Combination    | combineLatest, concat, merge, startWith , withLatestFrom, zip |
| Filtering      | debounceTime, distinctUntilChanged, filter, take, takeUntil   |
| Transformation | bufferTime, concatMap, map, mergeMap, scan, switchMap         |
| Utility        | tap                                                           |
| Multicasting   | share                                                         |

**Common Operators:**

**1. Pipe Operator:** The pipe() operator is a method to compose multiple operators together in a readable, functional way. It’s commonly used in Angular for HTTP responses, user input handling, and reactive forms.

**Use Cases:**
Transforming data: e.g., converting API responses before using them.
Filtering values: e.g., only pass certain items from a list.
Combining streams: e.g., merge multiple Observables.
Error handling: e.g., catchError within the pipeline.
Debouncing user input for search fields or auto-complete.

```js
// Example 1:
this.http.get<User[]>('/api/users')
  .pipe(
    map(users => users.filter(u => u.active)), // only active users
    map(users => users.map(u => u.name)) // extract names
  )
  .subscribe(names => this.userNames = names);

// Example 2:
fromEvent(searchInput, 'input')
  .pipe(
    debounceTime(300),
    map(event => event.target.value),
    distinctUntilChanged(),
    switchMap(query => this.http.get(`/api/search?q=${query}`))
  )
  .subscribe(results => this.searchResults = results);
```

**2. Map Operator:** The map() operator, basically, helps us to transform data using an observer. It takes each value emitted by an Observable and transforms it into something else, then passes it along to the next step in the pipeline.

**Use Cases**

- Transform API responses into a usable format.
- Extract specific properties from objects.
- Convert values (e.g., numbers to strings, timestamps to readable dates).

```js
// Example 1:
import { of } from "rxjs";
import { map } from "rxjs/operators";

of(1, 2, 3)
  .pipe(map((x) => x * 10))
  .subscribe(console.log);

// Output:
10;
20;
30;

// Example 2:
this.http.get<User[]>('/api/users')
  .pipe(
    map(users => users.map(u => u.name)) // transform array of users to array of names
  )
  .subscribe(names => console.log(names));
```

**3. Filter Operator:** The filter() allows an Observable to emit only values that meet a specified condition, discarding the rest. If the condition returns true, filter will emit value.

```js
// Example 1:
from([5, 12, 8, 20, 3])
  .pipe(
    filter(num => num > 10) // only allow numbers > 10
  )
  .subscribe(result => console.log(result)); // outputs: 12, 20


// Example 2:
this.http.get<User[]>('/api/users')
  .pipe(
    map(users => users.filter(u => u.active)) // only active users
  )
  .subscribe(activeUsers => console.log(activeUsers));
```

**4. ConcatMap Operator:** Creates an output Observable which sequentially emits all values from given Observable and then moves on to the next.

```js
import { of } from 'rxjs';
import { concatMap, delay } from 'rxjs/operators';

of(1, 2, 3)
  .pipe(
    concatMap(val => of(`Result ${val}`).pipe(delay(1000)))
  )
  .subscribe(console.log);

// Output:
Result 1
Result 2
Result 3
```

**5. Tap Operator:** The tap() lets you perform side effects like logging or debugging on Observable values without changing them.

**Use Cases**

- Logging values for debugging streams.
- Updating loading indicators or counters in UI.
- Triggering side effects like saving to local storage or analytics events.
- Performing actions without breaking the pipeline before passing values to map or filter.

```js
// Example 1: Logging API responses
this.http.get<User[]>('/api/users')
  .pipe(
    tap(users => console.log('Fetched users:', users)), // side effect
    map(users => users.filter(u => u.active))
  )
  .subscribe(activeUsers => console.log('Active users:', activeUsers));


// Example 2: Showing and hiding a loading spinner
this.http.get('/api/data')
  .pipe(
    tap(() => this.loading = true), // before request
    finalize(() => this.loading = false) // after complete
  )
  .subscribe(data => this.data = data);
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 33. What is switchMap and mergeMap, its difference?

**🔹 switchMap:** `switchMap` maps each value from a source Observable to an inner Observable and switches to the latest one, cancelling any previous emissions that haven’t completed.
It’s used in Angular for autocomplete, live search, or reactive form validation, where only the latest input matters.
Common pitfalls include unintended cancellation of previous streams and forgetting proper error handling.

> switchMap cancels previous streams and keeps only the latest, ideal for live search or reactive forms.

**Use Cases**

- Live search / autocomplete: cancel previous HTTP requests if the user types a new character.
- Dependent API calls where only the latest input matters.
- Reactive forms where the latest value triggers async validation.

```js
// Example 1: Autocomplete search
fromEvent(searchInput, "input")
  .pipe(
    map((event) => event.target.value),
    debounceTime(300),
    distinctUntilChanged(),
    switchMap((query) => this.http.get(`/api/search?q=${query}`)),
  )
  .subscribe((results) => (this.searchResults = results));

// Example 2: Reactive form validation
this.form
  .get("email")
  .valueChanges.pipe(
    debounceTime(300),
    switchMap((email) => this.http.get(`/api/check-email?email=${email}`)),
  )
  .subscribe((isAvailable) => (this.emailAvailable = isAvailable));
```

**🔹 mergeMap** mergeMap maps each source value to an inner Observable and subscribes to all of them concurrently.
It does not cancel previous Observables, allowing multiple operations to run in parallel.
Ideal for independent tasks like multiple file uploads or batch API calls.
Common pitfalls include overloading with too many concurrent operations and loss of order in emitted results.

**Use Cases**

- Multiple HTTP requests that can run concurrently.
- Parallel processing of user actions, like batch uploads.
- Combining streams where every emission should trigger a new async task.
- Handling multiple API calls from a list without waiting for each to finish sequentially.

```js
// Example 1: Parallel API calls for a list of IDs
from([1, 2, 3])
  .pipe(
    mergeMap((id) => this.http.get(`/api/item/${id}`)), // runs all requests concurrently
  )
  .subscribe((result) => console.log(result));

// Example 2: Multiple user actions triggering independent HTTP calls
from(userClicks)
  .pipe(mergeMap((click) => this.http.post("/api/action", click)))
  .subscribe((response) => console.log("Action processed:", response));
```

| Feature              | **switchMap**                                                         | **mergeMap**                                                          |
| -------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| **Behavior**         | Switches to the latest inner Observable, **cancelling previous ones** | Merges all inner Observables **concurrently**, no cancellations       |
| **Concurrency**      | 1 active at a time (previous cancelled)                               | Multiple active at a time (all run concurrently)                      |
| **Order of Results** | Only latest emission matters                                          | Order not guaranteed, results arrive as completed                     |
| **Use Case**         | Autocomplete search, live search, reactive forms (latest input only)  | Parallel API calls, batch processing, independent async tasks         |
| **Pitfalls**         | Previous requests may be cancelled unintentionally                    | Too many concurrent requests can overload server; order not preserved |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 34. What are forkJoin, combineLatest, zip and diff?

**🔹 forkJoin** forkJoin executes multiple Observables in parallel and emits a single combined result when all of them complete.
If any Observable fails, the entire stream errors out.
It is best suited for multiple HTTP calls that must finish before rendering a page.
Common pitfalls include waiting forever if an Observable never completes, and failure if any Observable errors.

**Use Cases**

- Multiple HTTP requests where you need all responses before continuing.
- Loading multiple resources in parallel and combining the results.
- Performing initial app setup where several independent async calls must finish first.

```js
// Example 1: Parallel API requests and combining results
forkJoin({
  users: this.http.get<User[]>('/api/users'),
  posts: this.http.get<Post[]>('/api/posts'),
  comments: this.http.get<Comment[]>('/api/comments')
}).subscribe(({ users, posts, comments }) => {
  console.log('All data loaded:', users, posts, comments);
});

// Example 2: Waiting for multiple independent async calls
forkJoin([
  this.http.get('/api/settings'),
  this.http.get('/api/profile'),
  this.http.get('/api/notifications')
]).subscribe(([settings, profile, notifications]) => {
  console.log('App initialized:', settings, profile, notifications);
});
```

**🔹 combineLatest** combineLatest combines multiple Observables and emits the latest values from each whenever any Observable emits.
It waits until all Observables emit at least once before producing output.
Common pitfalls include no emission until all sources emit, memory leaks, or too frequent updates.

**Use Cases**

- Reactive forms: combine multiple form controls to calculate a derived value.
- UI components: updating a display when multiple Observables change.
- Live filtering/search: combine filter selections and search input.
- Real-time dashboards: aggregate multiple data streams.

```js
// Example 1: Combine form inputs for validation
combineLatest([
  this.form.get("price").valueChanges,
  this.form.get("quantity").valueChanges,
])
  .pipe(map(([price, quantity]) => price * quantity))
  .subscribe((total) => (this.total = total));

// Example 2:Combine multiple API streams
combineLatest([
  this.http.get("/api/users"),
  this.http.get("/api/roles"),
]).subscribe(([users, roles]) => {
  this.usersWithRoles = users.map((u) => ({
    ...u,
    role: roles.find((r) => r.id === u.roleId),
  }));
});
```

**🔹 zip** zip combines multiple Observables by pairing their emissions based on index order.
It waits for corresponding values from each Observable before emitting a combined result.
Useful when data streams must be synchronized sequentially.
Common pitfalls include stopping early if a source completes and slower emission if sources emit at different rates.

**Use Cases**

- Combining related data streams where order matters.
- Coordinating multiple async operations that produce results sequentially.
- Synchronizing UI events like multiple sliders or inputs that must update together.
- Batch processing where each batch requires a value from each Observable.

```js
// Example 1: Pairing IDs and user names
const ids$ = of(1, 2, 3);
const names$ = of("Alice", "Bob", "Charlie");

zip(ids$, names$).subscribe(([id, name]) => {
  console.log(`User ${id}: ${name}`);
});
// Output: User 1: Alice, User 2: Bob, User 3: Charlie

// Example 2: Combining slider values
zip(slider1.valueChanges, slider2.valueChanges).subscribe(([val1, val2]) => {
  this.combinedValue = val1 + val2;
});
```

| Feature            | **combineLatest**                                                                               | **forkJoin**                                                                 | **zip**                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| **Emission**       | Emits **every time any source Observable emits**, but only after all have emitted at least once | Emits **once**, after **all source Observables complete**                    | Emits **once per combination**, pairing values **one-to-one** in order |
| **Values emitted** | Latest value from each Observable at the moment of emission                                     | Only the **last value** of each Observable                                   | Pairs values from each Observable in order (like zip in arrays)        |
| **Completion**     | Completes when **all sources complete**                                                         | Completes after **all sources complete**                                     | Completes when **any source completes**                                |
| **Use Case**       | Reactive UI updates where you care about **latest values**                                      | Multiple parallel API calls where you need **all results before proceeding** | Coordinating streams where values are **paired sequentially**          |
| **Pitfalls**       | Won’t emit until all sources have emitted at least once                                         | Won’t emit if a source never completes                                       | Stops when the shortest Observable completes, may lose extra values    |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 35. What is signal and its types?

Signals in Angular are part of Angular’s reactive system, introduced to provide a simpler and more predictable way to manage reactive state.
A Signal is essentially a reactive value container that notifies all subscribers automatically whenever its value changes — similar to how BehaviorSubject works, but with simpler syntax and better performance.

Think of a Signal like a reactive variable: you read it directly, and Angular automatically tracks dependencies to update the UI when it changes.

**Types of Signals**

**1. Writable Signal**

- Can store a value and be updated with set or by modifying its state.
- Example: countSignal.set(newValue)

**2. Readonly Signal**

- Cannot be updated directly — only allows reading.
- Useful for exposing state safely from a service or component.

**3. Computed Signal**

- Derives its value from other signals automatically.
- Updates automatically when the dependent signals change.

**4. Effect (Reactive Effect)**

- Runs a side-effect function whenever a signal it depends on changes.
- Example: updating the DOM, logging, or triggering other actions.

Real-World Examples

Writable Signal

```js
import { signal } from "@angular/core";

const count = signal(0); // writable signal
count.set(5); // update value
console.log(count()); // read value -> 5
```

Computed Signal

```js
import { computed } from "@angular/core";

const a = signal(2);
const b = signal(3);

const sum = computed(() => a() + b());
console.log(sum()); // 5

a.set(5);
console.log(sum()); // 8 (auto-updated)
```

Effect

```js
import { effect } from "@angular/core";

effect(() => {
  console.log(`The sum is ${sum()}`);
});
// Automatically logs whenever `sum` changes
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 36. What is difference between Subject and Observable?

**Observable:**

- A data producer that emits values over time.
- Cold by default, meaning it only starts emitting when someone subscribes.
- Each subscription is independent — each subscriber gets its own execution.
- Cannot emit values manually from outside; it’s defined by its creator.

```js
const obs$ = new Observable((observer) => {
  observer.next(Math.random());
});
obs$.subscribe((val) => console.log("Subscriber 1:", val));
obs$.subscribe((val) => console.log("Subscriber 2:", val));
// Each subscriber gets a **different random number**
```

**Subject:**

-A special type of Observable that is also an observer — it can emit values manually using next().
-Hot by default, meaning multiple subscribers share the same execution.
-Useful for multicasting values to multiple subscribers.
-Commonly used for event buses, shared state, or bridging imperative code with Observables.

```js
const subject = new Subject<number>();
subject.subscribe(val => console.log('Subscriber 1:', val));
subject.subscribe(val => console.log('Subscriber 2:', val));
subject.next(Math.random());
// Both subscribers receive the **same value**
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 37. What are the difference between Subject, Behavior subject, and Replay subject?

**1. Subject:**

- A basic observable that emits values to its subscribers.
- Does not store the previous value, and new subscribers only receive values emitted after they subscribe.

```typescript
const subject = new Subject<number>();

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`),
});

subject.next(1);
subject.next("A");

// Logs:
// observerA: 1
// observerA: A
```

**2. BehaviorSubject:**

- Extends Subject and stores the latest value emitted.
- New subscribers receive the last emitted value immediately upon subscription.
- Useful for scenarios where you need to access the most recent value or provide an initial value.

```typescript
import { BehaviorSubject } from "rxjs";
const subject = new BehaviorSubject(0); // 0 is the initial value

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`),
});

subject.next(1);
subject.next(2);

// Logs
// observerA: 0
// observerA: 1
// observerA: 2
```

**3. ReplaySubject:**

- Extends Subject and stores a buffer of previous emissions.
- New subscribers can receive a specified number of previous emissions (buffer) upon subscription.
- Useful for scenarios where you need to replay previous emissions to late subscribers or for caching purposes.

```typescript
import { ReplaySubject } from "rxjs";
const subject = new ReplaySubject(3); // buffer 3 values for new subscribers

subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`),
});

subject.next(1);
subject.next(2);
subject.next(3);

// Logs:
// observerA: 1
// observerA: 2
// observerA: 3
```

| **Type**          | **Initial Value** | **Emits Last Value** | **Replay Previous Values** | **Use Case**                                                                      |
| ----------------- | ----------------- | -------------------- | -------------------------- | --------------------------------------------------------------------------------- |
| `Subject`         | No                | No                   | No                         | Multicasting to multiple observers; no memory of past values                      |
| `BehaviorSubject` | Yes               | Yes (last value)     | No                         | Store and emit the **current state** to new subscribers                           |
| `ReplaySubject`   | Optional          | Yes (all buffered)   | Yes (buffered n values)    | Emit **past n values** to new subscribers; useful for caching or replaying events |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 38. What is NGRX?

**NGRX** is a state management library for Angular applications, inspired by Redux. It provides a centralized store to manage the state of an application and facilitates predictable state management by enforcing unidirectional data flow.

Here's a brief overview of NGRX concepts with an example:

**1. Store:** The central repository for application state. It holds the entire state of the application as a single immutable object.

**2. Actions:** Plain JavaScript objects that represent events or user interactions that can change the state of the application. They are dispatched to the store.

**3. Reducers:** Pure functions that specify how the application's state changes in response to actions. They take the current state and an action as input, and return the new state.

**4. Effects:** Asynchronous operations triggered by actions, such as HTTP requests or accessing browser storage. They listen for dispatched actions, perform side effects, and dispatch new actions in response.

**5. Selectors:** Functions used to derive or select specific pieces of state from the store. They help in composing and optimizing state access.

_**Here's a simple example of how NGRX can be used in an Angular application:**_

**1. Define Actions:**

```typescript
import { createAction, props } from "@ngrx/store";
import { PostInterface } from "src/app/_interface/post.interface";

const prefix = "[POST]";

export const getPost = createAction(`${prefix} Get Post`);

export const getPostSuccess = createAction(
  `${getPost.type}, Success`,
  props<{ post: PostInterface[] }>(),
);

export const createPost = createAction(
  `${prefix} Create Post`,
  props<{ post: PostInterface }>(),
);

export const createPostSuccess = createAction(
  `${createPost.type} Success`,
  props<{ post: PostInterface }>(),
);
```

**2. Define Reducers:**

```typescript
import { createReducer, on } from "@ngrx/store";
import { PostState } from "./post.model";
import * as fromPost from "./index";
import { Actions } from "@ngrx/store-devtools/src/reducer";

export const initialPostState: PostState = {
    isLoading: false,
    post: []
}

export const reducer = createReducer<PostState>(
    initialPostState,
    on(fromPost.getPost, (state) => {
        return {
            ...state,
            isLoading: true
        }
    }),
    on(fromPost.getPostSuccess, (state, { post }) => {
        return {
            ...state,
            isLoading: false,
            post
        }
    }),
    on(fromPost.createPost, (state) => {
        return {
            ...state,
            isLoading: true
        }
    }),
    on(fromPost.createPostSuccess, (state, { post }) => {
        return {
            ...state,
            isLoading: false,
            post: [...state.post, post]
        }
    })
  }
```

**3. Define Effects (Optional):**

```typescript
import { Injectable } from "@angular/core";
import { Actions, createEffect, ofType } from "@ngrx/effects";
import * as fromPost from "./index";
import { map, switchMap } from "rxjs";
import { PostService } from "src/app/_services/post.service";
import { PostInterface } from "src/app/_interface/post.interface";

@Injectable()
export class PostEffects {
  constructor(
    private readonly actions$: Actions,
    private readonly postSrv: PostService,
  ) {}

  getPost$ = createEffect(() =>
    this.actions$.pipe(
      ofType(fromPost.getPost.type),
      switchMap(() => this.postSrv.getPost()),
      map((post: PostInterface[]) => fromPost.getPostSuccess({ post })),
    ),
  );

  createPost$ = createEffect(() =>
    this.actions$.pipe(
      ofType(fromPost.createPost.type),
      switchMap(({ post }) => this.postSrv.createPost(post)),
      map((post: PostInterface) => fromPost.createPostSuccess({ post })),
    ),
  );
}
```

**4. Define Selectors (Optional):**

```typescript
import { createFeatureSelector, createSelector } from "@ngrx/store";
import { PostState } from "./post.model";

export const selectPostState = createFeatureSelector<PostState>("post");
export const selectPostList = createSelector(
  selectPostState,
  (state) => state.post,
);
export const selectPostIsLoading = createSelector(
  selectPostState,
  (state) => state.isLoading,
);
```

**5. Define App State:**

```typescript
export interface PostInterface {
  id: number;
  title: string;
}

import { PostInterface } from "src/app/_interface/post.interface";

export interface PostState {
  isLoading: boolean;
  showAddEditPost: boolean;
  post: PostInterface[];
}
```

**6. Post Store Module Setup:**

```typescript
import { NgModule } from "@angular/core";
import { StoreModule } from "@ngrx/store";
import { postReducer } from "./post.reducers";
import { EffectsModule } from "@ngrx/effects";
import { PostEffects } from "./post.effects";

@NgModule({
  imports: [
    StoreModule.forFeature("post", postReducer),
    EffectsModule.forFeature([PostEffects]),
  ],
})
export class PostStoreModule {}
```

**7. Use in Component:**

```typescript
import { Component, OnInit } from "@angular/core";
import { Observable } from "rxjs";
import { PostInterface } from "../_interface/post.interface";
import { Store, select } from "@ngrx/store";
import * as fromPost from "../_store/post";

@Component({
  selector: "app-post",
  templateUrl: "./post.component.html",
  styleUrls: ["./post.component.scss"],
})
export class PostComponent implements OnInit {
  post$!: Observable<PostInterface[]>;
  isLoading$!: Observable<boolean>;

  constructor(private store: Store) {}

  ngOnInit(): void {
    this.initDispatch();
    this.initSubscriptions();
  }

  private initDispatch(): void {
    this.store.dispatch(fromPost.getPost());
  }

  private initSubscriptions(): void {
    this.post$ = this.store.pipe(select(fromPost.selectPostList));
    this.isLoading$ = this.store.pipe(select(fromPost.selectPostIsLoading));
  }
}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 39. What is a standalone component?

Standalone components are a new feature in Angular that allows you to create reusable components that can be used without the need for an NgModule. This can make your code more modular, efficient, and easier to share. Angular 14+ Standalone Components. If playback doesn't begin shortly, try restarting your device.

```typescript
@Component({
  standalone: true,
  selector: "photo-gallery",
  imports: [ImageGridComponent],
  template: ` ... <image-grid [images]="imageList"></image-grid> `,
})
export class PhotoGalleryComponent {
  // component logic
}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 40. What is Async/await?

Async/await is a feature in JavaScript that allows you to write asynchronous code in a synchronous-looking manner. It provides a more readable and understandable way to work with asynchronous operations, such as fetching data from a server, reading files, or making network requests.

_Here's a brief overview of how async/await works:_

**Async Functions:** An async function is a function that operates asynchronously via the event loop, and it always returns a promise. You declare an async function using the async keyword before the function declaration.

**Await Operator:** Inside an async function, you can use the await keyword before an expression that returns a promise. The await keyword pauses the execution of the async function until the promise is resolved, and then it returns the resolved value.

_**Example:**_

```javascript
// Example asynchronous function
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data fetched successfully");
    }, 2000);
  });
}

// Async function using async/await
async function getData() {
  try {
    console.log("--- Start ---");
    const result = await fetchData();
    console.log(result);
    console.log("--- End ---");
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}

// Calling the async function
getData();
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 41. What are Template and Reactive forms?

**Template forms:** Template-Driven Forms define form logic in the HTML template using directives like ngModel, making them simple and suitable for small forms.

**Reactive forms:** Reactive Forms define the form model in TypeScript using FormControl and FormGroup, giving better scalability, validation control, and testability. They follow a model-driven approach.

| Feature       | Template Forms      | Reactive Forms      |
| ------------- | ------------------- | ------------------- |
| Setup         | HTML                | TypeScript          |
| Data flow     | Two-way binding     | Reactive streams    |
| Validation    | Template directives | Validators in TS    |
| Testing       | Harder              | Easier              |
| Scalability   | Small forms         | Large/complex forms |
| Dynamic forms | Difficult           | Easy                |

### Q 42. What is NgZone?

Angular provides a service called NgZone which creates a zone named angular to automatically trigger change detection when the following conditions are satisfied.

- When a sync or async function is executed.
- When there is no microTask scheduled.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 43. What is angular change detection?

Angular change detection is a built-in framework feature that ensures the automatic synchronization between the data of a component and its HTML template view.

Change detection works by detecting common browser events like mouse clicks, HTTP requests, and other types of events, and deciding if the view of each component needs to be updated or not.

There are two types of change detection:

- **Default change detection:** Angular decides if the view needs to be updated by comparing all the template expression values before and after the occurrence of an event, for all components of the component tree
- **OnPush change detection:** this works by detecting if some new data has been explicitly pushed into the component, either via a component input or an Observable subscribed to using the async pipe

ApplicationRef.tick(): Invoke this method to explicitly process change detection and its side-effects. It check the full component tree.
NgZone.run(callback): It evaluate the callback function inside the Angular zone.
ChangeDetectorRef.detectChanges(): It detects only the components and it's children.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 44. What is Ivy?

Ivy is Angular’s next-generation compilation and rendering engine, introduced in Angular 9.
It improves bundle size, build speed, tree shaking, debugging, and incremental compilation.
It replaced the older View Engine with a more optimized and efficient architecture.

**Why Ivy Was Introduced**

- Before Ivy (View Engine):
- Large bundle sizes
- Slower builds
- Harder debugging
- Poor tree shaking

**Ivy solved these problems by:**

- Generating less and more optimized code
- Making Angular more modular
- Improving incremental builds

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 45. What is difference between observable, subject and signal?

**Real-World Analogy**

- Observable → A newspaper subscription: each subscriber gets their own copy independently.
- Subject → A live TV broadcast: everyone watching sees the same program at the same time.
- Signal → A thermostat reading: any component depending on it automatically updates when the temperature changes.

**Interview-Ready Answer**

Observable is a cold, lazy stream where each subscriber executes independently.
Subject is a hot stream that can emit values manually to multiple subscribers simultaneously.
Signal is a reactive value container with auto-tracked dependencies and computed derivations, ideal for state management.

| Feature                | **Observable**                             | **Subject**                                        | **Signal**                                                          |
| ---------------------- | ------------------------------------------ | -------------------------------------------------- | ------------------------------------------------------------------- |
| **Nature**             | Lazy stream of values (cold by default)    | Hot stream, can emit values manually               | Reactive value container                                            |
| **Emissions**          | Controlled by producer                     | Controlled manually via `.next()`                  | Controlled by `set()` or derived automatically                      |
| **Subscribers**        | Each subscriber gets independent execution | Subscribers share same stream (multicast)          | Subscribers read value directly, auto-tracked dependencies          |
| **Reactivity**         | Requires `.subscribe()` to get values      | Multicast to multiple subscribers                  | Automatically notifies dependents when value changes                |
| **Derived / Computed** | Use operators like `map`, `combineLatest`  | Can use operators on the Subject stream            | Use `computed()` to derive reactive values automatically            |
| **Side-effects**       | Can use `tap()` inside pipeline            | Can use `tap()` or emit manually                   | Use `effect()` for side-effects                                     |
| **Use Case**           | Async streams like HTTP requests, timers   | Event buses, shared state, component communication | State management, reactive UI, derived values                       |
| **Memory Management**  | Need to unsubscribe or use `async` pipe    | Need to unsubscribe if long-lived                  | Tracks dependencies automatically, no manual subscriptions required |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 46. Compact Angular RxJS cheat sheet covering the most common operators!

**Quick Analogies for Interviews**

- Observable → Newspaper subscription → each subscriber gets full copy independently.
- Subject → Live TV broadcast → subscribers see only what’s currently airing.
- Signal → Thermostat → all UI components always reflect the latest value automatically.
- switchMap → Changing TV channels → previous stops, latest plays.
- mergeMap → Multiple delivery trucks → all run concurrently.
- concatMap → Coffee line → one at a time, in order.
- forkJoin → All friends arrive → start together once everyone is ready.
- combineLatest → Dashboard → updates whenever any widget changes.
- zip → Pairing socks → first with first, second with second, etc.

| Operator / Concept | What It Does                                                  | Key Points                                         | Use Case                                     |
| ------------------ | ------------------------------------------------------------- | -------------------------------------------------- | -------------------------------------------- |
| **map**            | Transforms each emitted value                                 | Always emits same number of values                 | Multiply numbers, format API data            |
| **filter**         | Emits only values meeting a condition                         | Doesn’t modify values                              | Only active users, valid inputs              |
| **tap**            | Performs side effects without changing values                 | For logging, loaders, analytics                    | Debugging, UI updates                        |
| **switchMap**      | Maps to inner Observable, **cancels previous**                | Only latest value matters                          | Autocomplete, live search, reactive forms    |
| **mergeMap**       | Maps to inner Observables **concurrently**                    | All emissions run independently                    | Parallel API calls, batch processing         |
| **concatMap**      | Maps to inner Observables **sequentially**                    | Preserves order                                    | Sequential API calls, dependent operations   |
| **forkJoin**       | Waits for **all Observables to complete**, emits last values  | Emits once, fails if any error                     | Multiple HTTP requests, app initialization   |
| **combineLatest**  | Emits on **any source emission** using latest values from all | Emits after all have emitted at least once         | Reactive forms, dashboards, UI state         |
| **zip**            | Combines values **one-to-one in order**                       | Stops when shortest Observable completes           | Pairing inputs, batch coordination           |
| **Observable**     | Cold, lazy stream                                             | Independent for each subscriber                    | HTTP calls, timers                           |
| **Subject**        | Hot, can emit manually                                        | Multicasts to all subscribers                      | Event bus, shared state                      |
| **Signal**         | Reactive value container                                      | Auto-updates dependents, supports computed/effects | State management, derived values, UI updates |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 47. What is Resolvers?

Resolvers in Angular are router services that fetch data before a route is activated, ensuring components have all required data at load.

**Conceptual Explanation**

- A Resolver is essentially a service that implements the Resolve interface.
- It runs before navigation to a route is completed.
- The route waits for the resolver to complete, and the data returned is injected into the component via ActivatedRoute.

**Use Case / Why We Need It**

- Prevents the component from rendering without the necessary data.
- Useful when loading data from APIs before showing the page.
- Keeps routing logic and data fetching separate from the component, improving maintainability.

**Common Pitfalls**

- Resolver must return an Observable or Promise, otherwise routing fails.
- Long-running HTTP calls can delay navigation, so use caching if necessary.

**Example:** Imagine a User Profile page where you need the user data before showing the UI.

**Resolver Service**

```js
import { Injectable } from '@angular/core';
import { Resolve } from '@angular/router';
import { Observable } from 'rxjs';
import { UserService } from './user.service';

@Injectable({ providedIn: 'root' })
export class UserResolver implements Resolve<any> {
  constructor(private userService: UserService) {}

  resolve(): Observable<any> {
    return this.userService.getUserProfile(); // fetches user data
  }
}
```

**Routing Module**

```js
const routes = [
  {
    path: "profile",
    component: ProfileComponent,
    resolve: { user: UserResolver }, // key: 'user' will hold the resolved data
  },
];
```

**Component Usage**

```js
import { ActivatedRoute } from '@angular/router';

export class ProfileComponent {
  user: any;

  constructor(private route: ActivatedRoute) {
    this.user = this.route.snapshot.data['user']; // access resolver data
  }
}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 48. what is Tree Shaking?

Tree Shaking is a build-time optimization that removes unused code from the final Angular bundle, reducing size and improving performance. Angular CLI automatically applies it during production builds using ES Modules.

**Conceptual Explanation**

- During build, Angular (via Webpack and the CLI) analyzes which functions, classes, modules, and imports are actually used.
- Anything not referenced anywhere is eliminated from the final JavaScript bundle.
- This helps reduce bundle size, improve loading time, and enhance performance.

**Why Angular Uses Tree Shaking**

- Smaller bundle size → faster downloads.
- Faster execution → fewer unused functions in memory.
- Optimized production builds → Angular CLI automatically applies it during ng build --prod.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 49. Angular Release History (Quick Interview Recap).

| Version           | Year | Major Updates                                                                           |
| ----------------- | ---- | --------------------------------------------------------------------------------------- |
| **AngularJS 1.x** | 2010 | First Angular framework, MVC architecture, two-way data binding, dependency injection   |
| **Angular 2**     | 2016 | Complete rewrite of AngularJS, introduced **TypeScript**, component-based architecture  |
| Angular 4         | 2017 | Smaller bundle size, improved **AOT compilation**, faster rendering                     |
| Angular 5         | 2017 | Build optimizer, **HttpClient module**, improved compiler                               |
| Angular 6         | 2018 | **Angular CLI improvements**, Angular Elements, RxJS 6 support                          |
| Angular 7         | 2018 | **Virtual scrolling**, CLI prompts, performance improvements                            |
| Angular 8         | 2019 | **Differential loading**, dynamic imports, web workers                                  |
| Angular 9         | 2020 | **Ivy rendering engine** enabled by default                                             |
| Angular 10        | 2020 | Better TypeScript integration, stricter project configuration                           |
| Angular 11        | 2020 | Faster builds, improved **Hot Module Replacement (HMR)**                                |
| Angular 12        | 2021 | Ivy everywhere, improved build system, strict typing                                    |
| Angular 13        | 2021 | **View Engine removed**, Ivy fully adopted                                              |
| Angular 14        | 2022 | **Typed Reactive Forms**, standalone component preview                                  |
| Angular 15        | 2022 | **Standalone components stable**, simplified module usage                               |
| Angular 16        | 2023 | **Signals introduced**, improved hydration, better performance                          |
| Angular 17        | 2023 | **New control flow (`@if`, `@for`)**, deferrable views                                  |
| Angular 18        | 2024 | **Signals improvements**, zoneless experiments, performance upgrades                    |
| Angular 19        | 2024 | Improved server rendering, better hydration and performance                             |
| Angular 20        | 2025 | Continued **signals-first architecture**, improved build tools and developer experience |

### Here is the Major release for quick interview recap.

| Version       | Year | Key Updates (2–3 lines)                                                                                                                               |
| ------------- | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Angular 2** | 2016 | Complete rewrite of AngularJS. Introduced **component-based architecture, TypeScript, RxJS, and dependency injection**. Foundation of modern Angular. |
| Angular 9     | 2020 | Introduced **Ivy rendering engine** as default. Reduced bundle size, improved build speed, better debugging and tree-shaking.                         |
| Angular 14    | 2022 | Introduced **Typed Reactive Forms** for better TypeScript safety and autocomplete. Also improved standalone APIs preview.                             |
| Angular 15    | 2022 | **Standalone Components became stable**, allowing apps without NgModules. Simplified architecture and improved lazy loading.                          |
| Angular 16    | 2023 | Introduced **Signals**, a new reactive state management model. Also improved hydration and performance optimizations.                                 |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 50. Angular Interview Quick Revision Sheet.

**1️⃣ Angular Core Concepts**

| Concept              | Quick Explanation                                                     |
| -------------------- | --------------------------------------------------------------------- |
| Component            | Basic building block of Angular UI (template + class + metadata).     |
| Module (NgModule)    | Organizes components, directives, pipes, and services.                |
| Standalone Component | Component that works **without NgModule** (introduced in Angular 15). |
| Directive            | Adds behavior to DOM elements (`ngIf`, `ngFor`).                      |
| Pipe                 | Transforms data in templates (`date`, `uppercase`).                   |
| Service              | Business logic shared across components.                              |
| Dependency Injection | Angular automatically provides service instances.                     |

**2️⃣ Angular Lifecycle Hooks**

| Hook            | Purpose                                 |
| --------------- | --------------------------------------- |
| ngOnInit        | Runs after component initialization     |
| ngOnChanges     | Runs when input properties change       |
| ngDoCheck       | Custom change detection                 |
| ngAfterViewInit | Runs after view initialization          |
| ngOnDestroy     | Cleanup (unsubscribe, remove listeners) |

**3️⃣ Change Detection**

| Strategy | Description                                                         |
| -------- | ------------------------------------------------------------------- |
| Default  | Angular checks every component in each change detection cycle       |
| OnPush   | Angular checks component only when inputs/events/observables change |

**Triggered by:**

- events
- HTTP responses
- timers
- promises

**4️⃣ RxJS Essentials**

| Concept       | Explanation                                      |
| ------------- | ------------------------------------------------ |
| Observable    | Stream of asynchronous data                      |
| Subject       | Multicast observable that can emit values        |
| switchMap     | Cancels previous request and switches to new one |
| mergeMap      | Executes multiple observables concurrently       |
| concatMap     | Executes observables sequentially                |
| forkJoin      | Waits for all observables to complete            |
| combineLatest | Emits when any observable emits                  |

**5️⃣ Forms**

| Type           | Description                                            |
| -------------- | ------------------------------------------------------ |
| Template Forms | Defined mainly in HTML using `ngModel`                 |
| Reactive Forms | Defined in TypeScript using `FormGroup`, `FormControl` |
| Typed Forms    | Introduced in Angular 14 for strong TypeScript typing  |

```js
FormControl → single input
FormGroup → group of controls
FormArray → dynamic controls
```

**6️⃣ Angular Architecture**

```js
Component
   ↓
Template
   ↓
Service (business logic)
   ↓
API / Backend
```

**Angular uses:**

- Component-based architecture
- Dependency Injection
- RxJS for async operations

7️⃣ Important Angular Features by Version

| Version    | Feature                |
| ---------- | ---------------------- |
| Angular 2  | Component architecture |
| Angular 9  | Ivy rendering engine   |
| Angular 14 | Typed Forms            |
| Angular 15 | Standalone Components  |
| Angular 16 | Signals                |

**8️⃣ Signals (Modern Reactivity)**

```js
count = signal(0);

count.set(5);
```

Benefits:

- fine-grained reactivity
- less change detection
- better performance

**9️⃣ Angular Project Structure**

```js
src/
 ├── app/
 │   ├── components
 │   ├── services
 │   ├── models
 │   └── app.module.ts
 ├── assets
 ├── environments
 └── main.ts
```

main.ts bootstraps the application.

**🔟 Angular Performance Best Practices**

- Use OnPush change detection
- Use trackBy in ngFor
- Use lazy loading
- Avoid unnecessary subscriptions
- Use async pipe
- Use signals where appropriate

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q . Error Handling

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

##
