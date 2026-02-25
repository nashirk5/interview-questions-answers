<!-- Start Angular -->

## **Angular**

<div align="right"><b><a href="../../README.md">↥ Back to home</a></b></div>

### Q 1. What is Angular?

Angular is a popular open-source front-end web framework developed and maintained by Google. It is used to build dynamic, single-page web applications (SPAs). Angular utilizes TypeScript, a superset of JavaScript, and offers a comprehensive set of tools and capabilities like two-way data binding, dependency injection, routing, and component-based architecture..

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 2. What are the Angular lifecycle hooks?

1. **ngOnChanges():** This hook is called whenever one or more input properties of the component change. This method/hook receives a SimpleChanges object that contains the previous and current values of the property.
2. **ngOnInit():** It initializes the component and sets the input properties of the component.
3. **ngDoCheck():** This is for the detection and to act on changes that Angular can't detect.
4. **ngAfterContentInit():** This is called in response after Angular projects external content into the component's view.
5. **ngAfterContentChecked():** This is called in response after Angular checks the content projected into the component.
6. **ngAfterViewInit():** This is called in response after Angular initializes the component's views and child views.
7. **ngAfterViewChecked():** This is called in response after Angular checks the component's views and child views.
8. **ngOnDestroy():** This is the cleanup phase just before Angular destroys the directive/component.

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 16. How do you share data between components?

**1. Input/Output Binding:** You can pass data from a parent component to a child component using input bindings (@Input decorator) and receive data back from the child using output bindings (@Output decorator with EventEmitter).

**2. Service:** You can create a service and inject it into the components that need to share data. The service acts as a central place to store and manage the shared data.

**3. RxJS Observables/Subjects:** You can use RxJS Observables or Subjects to create a data stream that multiple components can subscribe to. This allows for more complex scenarios like bi-directional communication and handling asynchronous data.

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 18. What is view encapsulation?

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
      { enableTracing: true }, // <-- debugging purposes only
    ),
  ],
})
export class AppModule {}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 20. What is the purpose of Wildcard route?

If the URL doesn't match any predefined routes then it causes the router to throw an error and crash the app. In this case, you can use wildcard route. A wildcard route has a path consisting of two asterisks to match every URL.

_**Example:**_

```typescript
  { path: '**', component: PageNotFoundComponent }
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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
    `ID: ${user.id}, Username: ${user.username}, Email: ${user.email}`,
  );
}

// Call the function with the user object
printUserInfo(user);
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 25. What is AOT and JIT?

- **JIT:** Just-in-Time (JIT) is a type of compilation that compiles your app in the browser at runtime, as the application is being loaded. .
- **AOT:** Ahead-of-Time (AOT) is a type of compilation that compiles your app at build time, before the application is deployed to the client's browser.

_AOT compilation offers better performance, smaller bundle sizes, and improved error detection compared to JIT compilation. It is the recommended compilation mode for production deployments of Angular applications. JIT compilation, on the other hand, provides faster development cycles and is suitable for development and testing environments._

> _**NOTE: JIT** compilation was the default until **Angular 8**, now default is **AOT**_

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 26. What are Observables and Promises?

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

### Q 27. What are the difference between Promises and Observables?

| Promise                                               | Observable                                                      |
| ----------------------------------------------------- | --------------------------------------------------------------- |
| Emits a single value                                  | Emits multiple values over a period of time                     |
| Eager, meaning they execute immediately upon creation | Lazy, meaning they do not execute until there is a subscription |
| cannot be canceled once they are created              | can be unsubscribed                                             |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 28. What are RXJS and list some operators?

RxJS (Reactive Extensions for JavaScript) is a library for handling asynchronous programming using observables. It makes it easier to compose asynchronous or event-based programs by using operators to transform, filter, and combine streams of data.

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

**_Example:_**

```js
import { of } from "rxjs";
import { map } from "rxjs/operators";

// Create an observable that emits numbers
const observable = of(1, 2, 3, 4);

// Subscribe to the observable and use operators to transform the emitted values
observable
  .pipe(
    map((value) => value * 2), // Double each value
  )
  .subscribe((result) => console.log(result));

// Output: 2, 4, 6, 8
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 28. What are the difference between Subject, Behavior subject, and Replay subject?

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

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 29. What is NGRX?

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

### Q 30. What is a standalone component?

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

### Q 31. What is Async/await?

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

### Q 32. What are Template and Reactive forms?

### Q 33. What is NgZone?

Angular provides a service called NgZone which creates a zone named angular to automatically trigger change detection when the following conditions are satisfied.

- When a sync or async function is executed.
- When there is no microTask scheduled.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 34. What is angular change detection?

Angular change detection is a built-in framework feature that ensures the automatic synchronization between the data of a component and its HTML template view.

Change detection works by detecting common browser events like mouse clicks, HTTP requests, and other types of events, and deciding if the view of each component needs to be updated or not.

There are two types of change detection:

- **Default change detection:** Angular decides if the view needs to be updated by comparing all the template expression values before and after the occurrence of an event, for all components of the component tree
- **OnPush change detection:** this works by detecting if some new data has been explicitly pushed into the component, either via a component input or an Observable subscribed to using the async pipe

ApplicationRef.tick(): Invoke this method to explicitly process change detection and its side-effects. It check the full component tree.
NgZone.run(callback): It evaluate the callback function inside the Angular zone.
ChangeDetectorRef.detectChanges(): It detects only the components and it's children.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 35. What are switchMap, mergeMap()?

<!-- Your content -->
<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 36. What are forkJoin, combineLatest, zip and diff?

<!-- Your content -->
<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

<!-- ### Q 32. What are Template and Reactive forms?

Your content
<div align="right"><b><a href="#angular">↥ Back to top</a></b></div> -->

##
