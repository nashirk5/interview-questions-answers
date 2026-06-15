<!-- Start Angular -->

## **Angular**

<div align="right"><b><a href="../../README.md">↥ Back to home</a></b></div>

### Q 1. What is Angular?

Angular is a popular open-source front-end web framework developed and maintained by Google. It is used to build dynamic, single-page web applications (SPAs). Angular utilizes TypeScript, a superset of JavaScript, and offers a comprehensive set of tools and capabilities like two-way data binding, dependency injection, routing, and component-based architecture.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 2. What are the Angular lifecycle hooks?

**1. ngOnChanges:**

- Called whenever an `@Input()` value changes.
- Used for: Detecting input changes from parent component.

**2. ngOnInit():**

- Called once after the first ngOnChanges.
- Used for: API calls and Initial data loading.

**3. ngDoCheck():**

- Called during every change detection cycle. Lets you implement custom change detection beyond Angular’s default.
- Used for: Custom change detection logic.

**4. ngAfterContentInit():**

- Called once after external content `ng-content` is projected into the component.
- Used for: Accessing projected content.

**5. ngAfterContentChecked():**

- Called after every check of projected content.
- Used for: Responding to projected content updates.

**6. ngAfterViewInit():**

- Called after component view and child views are initialized.
- Used for: DOM access and `@viewChild` operations.

**7. ngAfterViewChecked()**

- Called after every check of the component’s view and its children.
- Used for: Responding after view updates

**8. ngOnDestroy()**

- Called just before the component/directive is destroyed.
- Used for: Cleanup, Unsubscribing Observables and Clearing timers.

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

Components are the main building blocks, which control a part of the UI. A component is defined with a `@Component` decorator. Every component consists of three parts.

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

- When is a Component Destroyed?
  - A component is destroyed when Angular removes it from the component tree, such as during route navigation, when an `*ngIf` condition becomes false, when a parent component is destroyed, or when a dynamically created component is explicitly destroyed. Before removing the component, Angular invokes the ngOnDestroy lifecycle hook, which is used to perform cleanup activities such as unsubscribing from Observables, removing event listeners, clearing timers, and closing WebSocket connections to prevent memory leaks.

- Does Angular destroy services when component is destroyed?
  - It depends how the service are injected. If its root level Not destroyed when component dies.

| Service Scope            | Destroyed with Component?                |
| ------------------------ | ---------------------------------------- |
| `providedIn: 'root'`     | ❌ No                                    |
| App-level provider       | ❌ No                                    |
| Module-level provider    | ❌ Usually No (until module is unloaded) |
| Component-level provider | ✅ Yes                                   |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 5. What is Module?

A module is a place where we can group components, directives, services, and pipes. A module is defined with a `@NgModule` decorator. There are three types of modules.

- **Feature Module:** A module dedicated to a specific feature (user, admin, dashboard)
  ```typescript
  @NgModule({
    declarations: [UserListComponent],
    imports: [CommonModule],
  })
  export class UserModule {}
  ```
- **Shared Module:** A module that contains reusable components, pipes, directives
  ```typescript
  @NgModule({
    declarations: [LoaderComponent, HighlightDirective],
    exports: [LoaderComponent, HighlightDirective],
  })
  export class SharedModule {}
  ```
- **Core Module:** Contains singleton services used globally
  ```typescript
  @NgModule({
    providers: [AuthService, LoggerService],
  })
  export class CoreModule {}
  ```

| Module    | Purpose                        | Example                     |
| --------- | ------------------------------ | --------------------------- |
| AppModule | Root module of the application | App bootstrap, global setup |
| Feature   | Business feature               | User, Admin                 |
| Shared    | Reusable UI                    | Buttons, Pipes              |
| Core      | Global services                | Auth, Logger                |

```typescript
// Common module file
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

Services are objects which get instantiated only once during the lifetime of an application. The main objective of a service is to share data, functions with different components of an Angular application. A service is defined with a `@Injectable` decorator.

```typescript
import { Injectable } from "@angular/core";
@Injectable({
  providedIn: "root",
})
export class TestServiceService {
  constructor() {}
}
```

**Types of Service Instances**

1. **Singleton Service (Most Common):** Every component gets the same instance.

   ```js
   @Injectable({
     providedIn: "root",
   })
   export class UserService {}
   ```

2. **Module-Level Service:** One Instance Per Module Injector. Lazy-loaded modules may get separate instances.

   ```js
   @NgModule({
     providers: [UserService],
   })
   export class UserModule {}
   ```

3. **Component-Level Service:** Every component instance gets its own service.

   ```js
   @Component({
     providers: [UserService],
   })
   export class UserComponent {}
   ```

- What is the difference between `providedIn: 'root'` and `providers: [UserService]`?
  - `providedIn: 'root'` creates a singleton service shared across the application. `providers` at the component level creates a new instance for each component instance.

- When is a service instantiated?
  - Not at application startup. Usually: First Time Requested -> Angular Creates Instance. This is called lazy instantiation.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 7. What is providers in Angular?

Providers are Angular's way of configuring Dependency Injection. A provider tells Angular how to create and supply an instance for a dependency. Providers can be registered at the root, module, or component level, which determines the lifetime and scope of the service instance. Angular uses a hierarchical injector system, so component-level providers can override root-level providers when needed.

**Different Provider Types**

| Provider Type       | Syntax                                                   | Purpose                                 | Creates New Instance? | Common Use Case                                     |
| ------------------- | -------------------------------------------------------- | --------------------------------------- | --------------------- | --------------------------------------------------- |
| **useClass**        | `provide: LoggerService, useClass: FileLoggerService`    | Replace one implementation with another | ✅ Yes                | Environment-specific services, mocking              |
| **useValue**        | `provide: API_URL, useValue: 'https://api.com'`          | Inject a constant/static value          | ❌ No                 | Config values, feature flags, environment settings  |
| **useFactory**      | `provide: UserService, useFactory: factoryFn`            | Create service dynamically using logic  | Depends on factory    | Runtime configuration, conditional service creation |
| **useExisting**     | `provide: LoggerService, useExisting: FileLoggerService` | Create an alias to an existing provider | ❌ No                 | Multiple tokens pointing to same instance           |
| **Direct Provider** | `providers: [UserService]`                               | Shorthand for `useClass`                | ✅ Yes                | Most common service registration                    |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 8. What is Decorators?

Decorators are functions that provide metadata to Angular classes, helping Angular to understand how they should behave.

**Metadata** is used to decorate a class so that it can configure the expected behavior of the class. The metadata is represented by decorators

There are four main types of angular decorators:

1. **Class Decorators:** e.g. `@Component`, `@NgModule` and `@Pipe`

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

2. **Property Decorators:** e.g. `@Input()`, `@Output()`, `@ViewChild` and `@ViewChildren`

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

3. **Method Decorators:** e.g. `@HostListener()`

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

4. **Parameter Decorators:** e.g. `@Inject()`

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

Directives are used to modify the behavior, appearance of DOM elements.

**Types of directives:**

1. **Component directives:** These are directives with a template.
2. **Structural directives:** These directives change the DOM layout by adding and removing DOM elements. Ex. **`ngIf`, `ngFor`,** and **`ngSwitch`**.
3. **Attribute Directives:** These directives change the appearance or behavior of an element, component, or another directive. Ex. **`ngClass`** and **`ngStyle`**.

> _**👉 NOTE:** The `*` is syntactic sugar for Angular’s internal `<ng-template>`._

- Can we use multiple structural directives in a element?
  - No. Angular does not allow multiple structural directives on the same host element.

- Why?
  - Structural directives (`*ngIf`, `*ngFor`, `*ngSwitchCase`, etc.) internally transform the element into an `<ng-template>`.

```html
<div *ngIf="isLoggedIn">Welcome</div>

<!-- becomes: -->

<ng-template [ngIf]="isLoggedIn">
  <div>Welcome</div>
</ng-template>

<!-- Now imagine Angular sees: -->
<div *ngIf="isLoggedIn" *ngFor="let user of users"></div>

<!-- It doesn't know which <ng-template> should wrap the element first. -->
ngIf? -> ngFor? OR ngFor? -> ngIf?
```

Use ng-container

```html
<ng-container *ngIf="isLoggedIn">
  <div *ngFor="let user of users">{{ user.name }}</div>
</ng-container>
```

Angular 17+ New Control Flow

```js
@if (isLoggedIn) {
  @for (user of users; track user.id) {
    <div>{{ user.name }}</div>
  }
}
```

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

Data Binding is a technique used to synchronize data between the Angular component and the HTML template.

There are Four types of Data binding

1. **Interpolation / One way data biding `{{ }}`:** Used to display data from component to template.

```html
<p>Name: {{ title }}</p>
<p>{{ 1 + 1 }}</p>
```

2. **Two-way data binding `[(ngModel)]` = "value":** Two-way data binding allows to have the data flow both ways. For example, in the below code snippet, both the title DOM input and component title property are in sync.

```html
<input type="text" [(ngModel)]="title" />
```

3. **Property binding `[]` = "value":** Used to bind component data to HTML element properties.

```html
<input type="text" [disabled]="isDisabled" />
```

4. **Event binding (event) = "function":** Used to handle user events from template to component.

```html
<button (click)="onClick()"></button>
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 12. What are Pipes?

Pipes are used to transform or format data in Angular templates without changing the original value. They take input data, process it, and return a transformed output. They are written using the `|` symbol.

```html
<p>Hello {{ name | uppercase }}</p>
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 13. Difference between Pure and Impure pipe?

A pure pipe runs only when Angular detects a change in the input value or its reference. This includes changes in primitive values like `String`, `Number`, `Boolean`, and `Symbol`, or when the reference of objects such as `Array`, `Object`, `Date`, or `Function` changes.

An impure pipe runs during every change detection cycle, even if the value has not changed. Because of this, it can execute very frequently, such as on every keystroke or mouse movement.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 14. What is the async pipe?

The async pipe automatically subscribes to Observables or Promises and unsubscribes when the component is destroyed.

```typescript
// Example with Observable
users$ = this.userService.getUsers();

<div *ngFor="let user of users$ | async">
  {{ user.name }}
</div>

// Example with Promise
message = Promise.resolve('Hello Angular');

<p>{{ message | async }}</p>
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

Dependency Injection is a design pattern where Angular automatically provides required dependencies (services or objects) to a class instead of the class creating them manually.

```typescript
@Injectable({
  providedIn: "root",
})
export class UserService {
  getUsers() {
    return ["John", "Alex"];
  }
}
```

```typescript
constructor(private userService: UserService) {
  console.log(this.userService.getUsers());
}
```

**How Angular DI Works**

- Service is registered in Angular Injector
- Component requests dependency
- Injector creates/provides service instance
- Angular injects it into constructor

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 17. How do you share data between components?

**1. Input/Output Binding:** You can pass data from a parent component to a child component using input bindings `@Input` decorator and receive data back from the child using output bindings `@Output` with EventEmitter.

**2. Service:** You can create a service and inject it into the components that need to share data. The service acts as a central place to store and manage the shared data.

**3. RxJS Observables/Subjects:** You can use RxJS Observables or Subjects to create a data stream that multiple components can subscribe to. This allows for more complex scenarios like bi-directional communication and handling asynchronous data.

### Q 18. What are ng-template, ng-container, and ng-content?

- **`ng-template`**
  - It is used to define templates that can be reused or conditionally rendered.
  - ```html
    <div *ngIf="isLoggedIn; else loginTemplate">Dashboard</div>

    <ng-template #loginTemplate> Please Login </ng-template>
    ```

- **`ng-container`**
  - It is used to group elements together without adding an extra element to the DOM.
  - ```html
    <ng-container *ngIf="isVisible">
      <h1>Hello</h1>
      <p>Angular</p>
    </ng-container>
    ```
- **`ng-content`**
  - It allows a parent component to pass HTML/content into a child component.
  - ```html
    <!-- Child component template -->
    <div class="child-component">
      <ng-content></ng-content>
    </div>

    <!-- Parent component template -->
    <app-child>
      <p>Content projected into child component</p>
    </app-child>

    <!-- Output -->
    <div class="child-component">
      <p>Content projected into child component</p>
    </div>
    ```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 19. What is view encapsulation?

View Encapsulation controls how component styles are applied in Angular.

**Types of View Encapsulation:**

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

**How It Works**

- Component sends HTTP request
- Interceptor catches request
- Request can be modified
- Request goes to server
- Response comes back through interceptor

> _**👉 NOTE:** Why do we use req.clone() in interceptor? Because Angular HTTP requests are immutable._

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 26. What is an interface?

In Angular, an interface is a TypeScript feature used to define the structure of objects.

It acts as a contract that describes the properties and methods an object must have in order to be considered of that type. Interfaces are commonly used to enforce type-checking and provide better code readability and maintainability

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

Lazy Loading is a technique where feature modules are loaded asynchronously only when they are needed instead of loading the entire application at startup.

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

1. Use Server-Side Pagination instead of loading all records at once.
2. Implement Virtual Scrolling (Angular CDK) to render only visible rows.
3. Use Infinite Scrolling for large lists and feeds.
4. Enable Lazy Loading for feature modules.
5. Use OnPush Change Detection to reduce unnecessary checks.
6. Implement `trackBy` with `*ngFor` to avoid recreating DOM elements.
7. Cache API responses using `shareReplay()`.
8. Use Debounce and `distinctUntilChanged()` for search inputs.
9. Prefer Async Pipe over manual subscriptions.
10. Avoid fetching unnecessary fields from APIs.
11. Use Skeleton Loaders instead of blocking spinners for better UX.
12. Implement SSR/Hydration for faster initial page load.
13. Use Tree Shaking and Code Splitting to reduce bundle size.
14. Load images lazily using `loading="lazy"`.
15. Profile performance using Lighthouse, Angular DevTools, and Chrome Performance Tab.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 29. What is AOT and JIT?

- **JIT:** Just-in-Time (JIT) is a type of compilation that compiles your app in the browser at runtime, as the application is being loaded. .
- **AOT:** Ahead-of-Time (AOT) is a type of compilation that compiles your app at build time, before the application is deployed to the client's browser.

_AOT compilation offers better performance, smaller bundle sizes, and improved error detection compared to JIT compilation. It is the recommended compilation mode for production deployments of Angular applications. JIT compilation, on the other hand, provides faster development cycles and is suitable for development and testing environments._

> _**NOTE: JIT** compilation was the default until **Angular 8**, now default is **AOT**_

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 30. What are Observables and Promises?

**Observable:** Observables are RxJS objects used to handle asynchronous data streams and can emit multiple values over time.

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

### Q 32. What is RXJS?

RxJS (Reactive Extensions for JavaScript) is a library used for reactive programming with Observables. It handle asynchronous data streams like HTTP requests, Events (click, input, scroll), WebSockets and Timers. In Angular, RxJS is used heavily with HttpClient, forms, and state management.

**Reactive programming** is a programming style where you react to changes in data over time instead of actively pulling or checking for updates.

In simple terms: You don’t ask for data repeatedly. You just “listen” and react when data changes

**Key Concepts in RxJS:**

**1. Observable:** An Observable is a stream of data that emits values over time and only runs when someone subscribes to it. It can emit multiple values, an error, or a completion signal depending on the execution flow.

**2. Observer:** An Observer is the consumer that receives data from an Observable. It defines how to handle incoming values, errors, and completion using next, error, and complete.

**3. Subscription:** The process of linking an observer to an observable. When you subscribe, you start receiving the data from the observable.

**4. Operators:** Operators are functions used inside `.pipe()` to transform, filter, or control data flowing through an Observable. They help in shaping the data before it reaches the subscriber.

**5. Subject:** A Subject is both an Observable and an Observer, meaning it can emit and receive values. It is used when you want to multicast data to multiple subscribers.

**Common Operators:** RxJS operators are used inside `.pipe()` to transform, filter, and control data streams.

**1. Pipe Operator:** Used to combine multiple operators.

```js
fromEvent(searchInput, "input")
  .pipe(
    debounceTime(300),
    map((event) => event.target.value),
    distinctUntilChanged(),
    switchMap((query) => this.http.get(`/api/search?q=${query}`)),
  )
  .subscribe((results) => (this.searchResults = results));
```

**2. Map Operator:** `map()` operator helps to transforms each emitted value into a new value. It is used when you want to modify data coming from a stream.

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

**3. Filter Operator:** If the condition returns true, filter will emit value. Filters values based on a condition. If the condition returns true, filter will emit value.

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

**4. Tap Operator:** The `tap()` lets you perform side effects like logging or debugging on Observable values without changing them.

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

**5. switchMap():** Cancels the previous inner Observable and switches to the latest one. Commonly used in search or API calls.

```js
this.searchControl.valueChanges
  .pipe(
    debounceTime(300),
    distinctUntilChanged(),
    switchMap((searchTerm) =>
      this.http.get(`/api/products?search=${searchTerm}`),
    ),
  )
  .subscribe((results) => {
    this.products = results;
  });
```

**6. mergeMap():** Executes Observables one after another in sequence. Each request waits for the previous one to finish.

```js
from([1, 2, 3])
  .pipe(mergeMap((id) => this.http.get(`/api/users/${id}`)))
  .subscribe((user) => {
    console.log(user);
  });
```

**7. ConcatMap Operator:** Creates an output Observable which sequentially emits all values from given Observable and then moves on to the next.

```js
from([1, 2, 3])
  .pipe(concatMap((id) => this.http.post("/api/save", { id })))
  .subscribe((res) => {
    console.log("Saved:", res);
  });
```

| Area           | Operators                                                     |
| -------------- | ------------------------------------------------------------- |
| Creation       | from,fromEvent, of                                            |
| Combination    | combineLatest, concat, merge, startWith , withLatestFrom, zip |
| Filtering      | debounceTime, distinctUntilChanged, filter, take, takeUntil   |
| Transformation | bufferTime, concatMap, map, mergeMap, scan, switchMap         |
| Utility        | tap                                                           |
| Multicasting   | share                                                         |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 33. What is switchMap and mergeMap, and its difference?

**SwitchMap:** `switchMap()` cancels the previous inner Observable and only keeps the latest one active. If a new value comes before the previous request completes, the old one is discarded.

**Real use case:**
Search box. If user types “a → ap → app”, only the last request (“app”) is considered. Previous API calls are cancelled to avoid unnecessary responses.

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

**MergeMap** `mergeMap()` does NOT cancel previous requests. It runs all inner Observables in parallel and returns results as they arrive.

**Real use case:**
Loading multiple user details or uploading multiple files where each request should complete independently.

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

| Feature              | switchMap                     | mergeMap                         | concatMap                      | exhaustMap                                           |
| -------------------- | ----------------------------- | -------------------------------- | ------------------------------ | ---------------------------------------------------- |
| **Execution**        | Switches to latest Observable | Runs all Observables in parallel | Runs one after another (queue) | Ignores new Observables while current one is running |
| **Previous request** | ❌ Cancelled                  | ❌ Not cancelled                 | ❌ Waits until completion      | ✅ Current request continues, new requests ignored   |
| **Order maintained** | ❌ No                         | ❌ No                            | ✅ Yes                         | ✅ Yes (only first request processed)                |
| **Concurrency**      | Only latest active            | Multiple at same time            | One at a time                  | One at a time (ignores new emissions)                |
| **Best use case**    | Search, autocomplete          | Parallel API calls, file uploads | Sequential tasks, step forms   | Login, Submit button, Payment processing             |
| **Risk**             | Can miss previous results     | Can overload server              | Slower execution               | Can ignore valid user actions                        |
| **Behavior style**   | Latest wins                   | All execute                      | FIFO (queue system)            | First wins, rest ignored until completion            |

**Easy Interview Memory Line**

- `switchMap` → Latest wins (cancel previous)
- `mergeMap` → Everyone wins (run all in parallel)
- `concatMap` → Wait in line (queue, one by one)
- `exhaustMap` → First wins (ignore new until complete)

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 34. What are forkJoin, combineLatest, zip and diff?

**forkJoin** forkJoin executes multiple Observables in parallel and emits a single combined result when all of them complete.
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

**combineLatest** combineLatest combines multiple Observables and emits the latest values from each whenever any Observable emits.
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

| Feature             | forkJoin                  | combineLatest                     | zip                  |
| ------------------- | ------------------------- | --------------------------------- | -------------------- |
| Emits               | Once (after all complete) | Every time any Observable changes | Paired values only   |
| Requires completion | Yes                       | No                                | No                   |
| Behavior            | Final result only         | Live updates                      | Synchronized pairing |
| Order dependency    | No                        | No                                | Yes                  |
| Best use case       | API calls, dashboard load | Real-time UI updates              | Matching streams     |

**Easy Memory Trick**

- forkJoin → Wait all, emit once (final result)
- combineLatest → Anytime change, latest values
- zip → Pair by index (like zipper)

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 35. What is signal and its types?

A Signal is a reactive primitive introduced in Angular to manage state in a simple and efficient way. It holds a value and automatically notifies the UI whenever that value changes, without needing RxJS or manual subscriptions.

```js
// Component
import { signal } from '@angular/core';

count = signal(0);

increment() {
  this.count.set(this.count() + 1);
}

// HTML
<p>{{ count() }}</p>
```

**Types of Signals**

**1. Writable Signal:** A signal whose value can be changed manually using set() or update(). Used for state management (like counter, form state, UI state). Real use case: Counter, toggle button, form inputs, UI state updates.

```js
import { signal } from "@angular/core";

const count = signal(0); // writable signal
count.set(5); // update value
console.log(count()); // read value -> 5
```

**2. Computed Signal:** A signal that is derived from other signals and automatically updates when dependencies change. Real use case: Cart total price, filtered lists, derived UI values.

```js
import { computed } from "@angular/core";

const a = signal(2);
const b = signal(3);

const sum = computed(() => a() + b());
console.log(sum()); // 5

a.set(5);
console.log(sum()); // 8 (auto-updated)
```

**3. Effect Signal:** Used to perform side effects whenever a signal changes (like logging, API calls, or syncing data). Real use case: Logging, saving to localStorage, triggering API calls.

```js
import { effect } from "@angular/core";

effect(() => {
  console.log(`The sum is ${sum()}`);
});
// Automatically logs whenever `sum` changes
```

| Type            | Purpose                  | Writable | Example Use          |
| --------------- | ------------------------ | -------- | -------------------- |
| Writable Signal | Store and update value   | ✅ Yes   | Counter, form state  |
| Computed Signal | Derived/calculated value | ❌ No    | Total price, filters |
| Effect Signal   | Side effects on change   | ❌ No    | Logging, API sync    |

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

- A special type of Observable that is also an observer — it can emit values manually using next().
- Hot by default, meaning multiple subscribers share the same execution.
- Useful for multicasting values to multiple subscribers.
- Commonly used for event buses, shared state, or bridging imperative code with Observables.

```js
const subject = new Subject<number>();
subject.subscribe(val => console.log('Subscriber 1:', val));
subject.subscribe(val => console.log('Subscriber 2:', val));
subject.next(Math.random());
// Both subscribers receive the **same value**
```

**Cold vs Hot Observables**

- Cold Observable
  - Starts execution for each subscriber
  - Example: HTTP request
- Hot Observable
  - Shared execution
  - Example: Subject, WebSocket

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 37. What are the difference between Subject, Behavior subject, Replay subject, and AsyncSubject?

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

**4. AsyncSubject:**

- An AsyncSubject is a special type of Subject that only emits the last value when the stream completes.
- If the stream never completes, it will not emit anything.
- Give me only the final result, and only when everything is done.

```js
const asyncSubject = new AsyncSubject<number>();

asyncSubject.subscribe(v => console.log('A:', v));

asyncSubject.next(1);
asyncSubject.next(2);
asyncSubject.next(3);

asyncSubject.complete();

// Output
A: 3
```

| Feature                        | Subject               | BehaviorSubject             | ReplaySubject               | AsyncSubject               |
| ------------------------------ | --------------------- | --------------------------- | --------------------------- | -------------------------- |
| Stores values                  | ❌ No                 | ✅ Latest value             | ✅ Multiple values (buffer) | ✅ Only last value         |
| New subscriber gets old values | ❌ No                 | ✅ Latest value immediately | ✅ Past buffered values     | ❌ Only after completion   |
| Emits immediately              | ❌ Only future values | ✅ Yes (latest)             | ✅ Yes (replay history)     | ❌ No                      |
| Requires initial value         | ❌ No                 | ✅ Yes                      | ❌ No                       | ❌ No                      |
| Emits when complete() called   | ❌ No                 | ❌ No                       | ❌ No                       | ✅ Yes (only last value)   |
| Common use case                | Events, clicks        | App state, login user       | Chat, history, cache        | Final result (HTTP/report) |

- Subject → No memory
- BehaviorSubject → Last value memory
- ReplaySubject → Full history memory
- AsyncSubject → Final value only

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

```html
<h2>Template-driven Form</h2>

<form #regForm="ngForm" (ngSubmit)="onSubmit(regForm)">
  <!-- Name -->
  <div>
    <label>Name</label>
    <input
      type="text"
      name="name"
      ngModel
      required
      minlength="3"
      #name="ngModel"
    />
    <div *ngIf="name.invalid && name.touched">
      Name is required (min 3 characters)
    </div>
  </div>

  <!-- Email -->
  <div>
    <label>Email</label>
    <input type="email" name="email" ngModel required email #email="ngModel" />
    <div *ngIf="email.invalid && email.touched">Enter a valid email</div>
  </div>

  <!-- Password -->
  <div>
    <label>Password</label>
    <input
      type="password"
      name="password"
      ngModel
      required
      minlength="6"
      #password="ngModel"
    />
    <div *ngIf="password.invalid && password.touched">
      Password must be at least 6 characters
    </div>
  </div>

  <button type="submit" [disabled]="regForm.invalid">Register</button>
</form>
```

**Reactive forms:** Reactive Forms define the form model in TypeScript using FormControl and FormGroup, giving better scalability, validation control, and testability. They follow a model-driven approach.

| Feature       | Template Forms      | Reactive Forms      |
| ------------- | ------------------- | ------------------- |
| Setup         | HTML                | TypeScript          |
| Data flow     | Two-way binding     | Reactive streams    |
| Validation    | Template directives | Validators in TS    |
| Testing       | Harder              | Easier              |
| Scalability   | Small forms         | Large/complex forms |
| Dynamic forms | Difficult           | Easy                |

### Q 42. Write a code to submit a form by using the Reactive form?

```js
import { Component } from '@angular/core';
import { FormBuilder, Validators, FormArray } from '@angular/forms';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {

  constructor(private fb: FormBuilder) {}

  // Main Form
  employeeForm = this.fb.group({
    name: ['', [Validators.required, Validators.minLength(3)]],
    email: ['', [Validators.required, Validators.email]],
    department: ['', Validators.required],

    // Dynamic skills list
    skills: this.fb.array([])
  });

  // Getter for skills FormArray
  get skills(): FormArray {
    return this.employeeForm.get('skills') as FormArray;
  }

  // Add new skill
  addSkill() {
    this.skills.push(
      this.fb.control('', Validators.required)
    );
  }

  // Remove skill
  removeSkill(index: number) {
    this.skills.removeAt(index);
  }

  // Submit form
  onSubmit() {
    console.log('Employee Data:', this.employeeForm.value);

    if (this.employeeForm.valid) {
      // Here you would call API
      alert('Employee Registered Successfully!');
    } else {
      alert('Form is invalid');
    }
  }
}
```

```html
<h2>Employee Registration Form</h2>

<form [formGroup]="employeeForm" (ngSubmit)="onSubmit()">
  <!-- Name -->
  <div>
    <label>Name</label>
    <input type="text" formControlName="name" />
    <div
      *ngIf="employeeForm.get('name')?.invalid && employeeForm.get('name')?.touched"
    >
      Name is required (min 3 characters)
    </div>
  </div>

  <!-- Email -->
  <div>
    <label>Email</label>
    <input type="email" formControlName="email" />
    <div
      *ngIf="employeeForm.get('email')?.invalid && employeeForm.get('email')?.touched"
    >
      Enter valid email
    </div>
  </div>

  <!-- Department -->
  <div>
    <label>Department</label>
    <select formControlName="department">
      <option value="">Select</option>
      <option value="IT">IT</option>
      <option value="HR">HR</option>
      <option value="Finance">Finance</option>
    </select>
  </div>

  <!-- Skills (Dynamic FormArray) -->
  <div>
    <h4>Skills</h4>

    <button type="button" (click)="addSkill()">+ Add Skill</button>

    <div formArrayName="skills">
      <div *ngFor="let skill of skills.controls; let i = index">
        <input [formControlName]="i" placeholder="Enter skill" />

        <button type="button" (click)="removeSkill(i)">Remove</button>
      </div>
    </div>
  </div>

  <!-- Submit -->
  <button type="submit" [disabled]="employeeForm.invalid">Submit</button>
</form>
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 43. What is NgZone?

`NgZone` is a service in Angular that helps manage change detection automatically or manually when async operations happen (like setTimeout, API calls, WebSocket, etc.). In simple terms: `NgZone` tells Angular when to update the UI after async work.

- When a sync or async function is executed.
- When there is no microTask scheduled.

```js
// Running code inside Angular zone (default behavior)
constructor(private ngZone: NgZone) {}

ngOnInit() {
  setTimeout(() => {
    this.data = 'Updated inside Angular zone';
  }, 1000);
}

// Running code outside Angular zone
constructor(private ngZone: NgZone) {}

ngOnInit() {
  this.ngZone.runOutsideAngular(() => {
    setTimeout(() => {
      this.data = 'Updated outside Angular zone';

      // Manually trigger UI update
      this.ngZone.run(() => {
        console.log('UI updated manually');
      });

    }, 1000);
  });
}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 44. What is angular change detection?

Change Detection is Angular's mechanism for synchronizing component data with the DOM. By default, Angular checks the entire component tree using Zone.js-triggered cycles, while OnPush reduces checks by reacting only to input reference changes, events, and observable emissions. In Angular 16+, Signals provide fine-grained reactivity and further improve performance by updating only affected UI parts.

There are two types of change detection:

- **Default change detection:** Angular decides if the view needs to be updated by comparing all the template expression values before and after the occurrence of an event, for all components of the component tree
- **OnPush change detection:** this works by detecting if some new data has been explicitly pushed into the component, either via a component input or an Observable subscribed to using the async pipe

ApplicationRef.tick(): Invoke this method to explicitly process change detection and its side-effects. It check the full component tree.
NgZone.run(callback): It evaluate the callback function inside the Angular zone.
ChangeDetectorRef.detectChanges(): It detects only the components and it's children.

**Follow-Up Questions**

1. How does Angular internally know when to run Change Detection?
   - Angular uses Zone.js to patch async APIs such as: setTimeout, Promise, HTTP requests,DOM events. When an async operation completes, Zone.js notifies Angular, which triggers a Change Detection cycle.
2. Why is OnPush faster than Default Change Detection?
   Default strategy checks the entire component tree whenever Change Detection runs. OnPush limits checks to: Input reference changes, Events, Observable emissions, Manual triggers. This reduces unnecessary component evaluations and improves performance.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 45. What is Ivy?

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

### Q 46. What is difference between observable, subject and signal?

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

### Q 49. What are Web Vitals?

Core Web Vitals are user-centric performance metrics defined by Google to measure page loading, responsiveness, and visual stability.

The three key metrics are LCP (Largest Contentful Paint) for loading performance, INP (Interaction to Next Paint) for responsiveness, and CLS (Cumulative Layout Shift) for visual stability.

**Largest Contentful Paint(LCP):** Measures how long it takes for the largest visible content element to appear.

**Interaction to Next Paint(INP):** Measures how quickly the UI responds after a user interaction. **Good Score ≤ 200ms**

**Cumulative Layout Shift(CLS):** Measures unexpected movement of page elements. **Good Score ≤ 0.1**

| Metric | Measures            | Good Score |
| ------ | ------------------- | ---------- |
| LCP    | Loading Performance | ≤ 2.5s     |
| INP    | Interactivity       | ≤ 200ms    |
| CLS    | Visual Stability    | ≤ 0.1      |

In Angular applications, these can be improved through lazy loading, code splitting, OnPush change detection, virtual scrolling, image optimization, caching, and SSR.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 50. How would you architect a large Angular application?

I would organize the application into Core, Shared, and Feature modules. Core contains singleton services, interceptors, and guards. Shared contains reusable components, directives, and pipes. Business domains are separated into feature modules with lazy loading to improve performance. I would keep business logic in services, use smart and dumb component patterns, implement centralized error handling through interceptors, and choose state management based on complexity, using services for smaller applications and NgRx for larger ones. For enterprise-scale systems, I would also consider micro frontends, reusable component libraries, and modern Angular features like standalone components and signals to improve maintainability and scalability.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 51. How do you optimize a 100k-row grid?

For a 100k-row grid, I would never render all rows at once because the DOM becomes too large and impacts memory, rendering, and change detection performance. Instead, I would use virtual scrolling to render only the visible rows, implement pagination or server-side paging if appropriate, use OnPush change detection, trackBy in ngFor, optimize API calls, and avoid expensive calculations inside templates.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 52. What causes memory leaks?

Memory leaks occur when objects remain referenced and cannot be garbage collected. In Angular, the most common causes are unsubscribed Observables, event listeners, timers, and retained object references. I prevent them using AsyncPipe, takeUntil/takeUntilDestroyed, proper cleanup in ngOnDestroy, and regular memory profiling with browser DevTools.

**Common Causes:**

- Unsubscribed Observables (`Subject`, `BehaviorSubject`, `interval`, `valueChanges`)
- Event listeners not removed
- `setInterval` or long-running timers not cleared
- Closures holding references to large objects
- Detached DOM elements still referenced
- Global variables
- Misuse of `shareReplay()` or cached data

**Prevention:**

- Use `AsyncPipe`
- Use `takeUntil()` or `takeUntilDestroyed()`
- Remove event listeners in `ngOnDestroy`
- Clear intervals/timeouts
- Avoid unnecessary global references

- How Would You Detect a Memory Leak?
  - Using browser DevTools: Chrome DevTools -> Memory Tab -> Heap Snapshot

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 53. What is circular dependencies and how do you avoid ?

Circular dependency occurs when two or more modules, services, or components depend on each other directly or indirectly. It can lead to runtime errors, unexpected behavior, and make the code difficult to maintain. I avoid it by maintaining clear separation of responsibilities, using interfaces/abstractions, introducing mediator services, and following a layered architecture.

Circular dependencies are avoided by enforcing one-way dependency flow, extracting shared logic, and using a mediator service or state management instead of direct service-to-service coupling.

How to Detect Circular Dependencies?

```js
npm install madge -g
madge --circular src
```

Angular build warnings and dependency graph tools can also help identify them.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 54. How would you reduce initial bundle size?

To reduce the initial bundle size, I focus on loading only the code required for the first screen. I use lazy loading for feature modules, remove unused dependencies, optimize third-party libraries, enable tree shaking, use standalone components where appropriate, and optimize images and assets. The goal is to improve load time and Core Web Vitals such as LCP.

**Key Techniques:**

- **Lazy Loading:** Load feature modules only when users navigate to them.
- **Code Splitting:** Split large bundles into smaller chunks.
- **Tree Shaking:** Remove unused code during production builds.
- **Optimize Third-Party Libraries:** Import only required modules/functions.
- **Standalone Components:** Reduce module overhead and improve route-level loading.
- **Image Optimization:** Compress and lazy-load images.
- **Avoid Large Dependencies:** Replace heavy libraries with lighter alternatives when possible.
- **Production Build Optimizations:** AOT compilation, minification, compression (Gzip/Brotli).

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 55. What is template lazy loading?

Yes, Angular supports template-level lazy loading. In Angular 17+, I can use `@defer` blocks to lazy load components based on conditions such as viewport visibility, user interaction, or idle time. This reduces the initial bundle size and improves page load performance because heavy components are downloaded only when required. Additionally, for images I use the browser's native `loading="lazy"` attribute.

**Load on Viewport:** Downloads when the component scrolls into view.

```js
@defer (on viewport) {
  <app-heavy-chart />
}
```

**Load on Interaction:** Downloads when the user interacts.

```js
@defer (on interaction) {
  <app-user-details />
}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 56. What is Web Security and how do you handle it?

1. **XSS (Cross-Site Scripting):** XSS occurs when malicious scripts are injected into a webpage and executed in a user's browser. Angular helps prevent XSS through built-in sanitization, but developers should avoid unsafe DOM manipulation and validate user input.

   **Prevention:**
   - Angular automatically sanitizes HTML.
   - Avoid direct DOM manipulation.
   - Use Angular bindings instead of innerHTML.
   - Use Content Security Policy (CSP).

2. **CORS:** CORS is a browser security mechanism that restricts cross-origin requests unless explicitly allowed by the server.
   - Why does the API work in Postman but fail in the browser?
     - Because browsers enforce CORS.

     ```js
     Frontend: app.company.com;

     Backend: api.company.com;

     // Backend must allow:
     Access - Control - Allow - Origin;
     ```

3. **CSRF (Cross-Site Request Forgery):** CSRF attacks force authenticated users to perform unintended actions. Common protections include CSRF tokens and SameSite cookie settings.

4. **Authentication vs Authorization:** Authentication verifies identity, while authorization determines what resources a user can access.

5. **JWT Security:** Access Token and Refresh Token. Access Token and Refresh Token. Store in: Secure HttpOnly Cookies

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 57. What design patterns do you follow?

In Angular, the most common design patterns I use are Singleton for services, Observer through RxJS, Factory via dependency injection, Facade for NgRx state management, Strategy for dynamic business rules, and Decorator through Angular decorators like `@Component` and `@Injectable`. These patterns help build scalable, maintainable, and loosely coupled enterprise applications.

1. **Singleton Pattern:** Only one instance of a class exists throughout the application.

   Angular services provided at the root level are examples of the Singleton pattern because only one instance is shared across the application.

2. **Observer Pattern:** One object notifies multiple subscribers when data changes.

   Angular heavily uses the Observer pattern through RxJS Observables and Subjects, where multiple subscribers react to emitted values.

3. **Factory Pattern:** Create objects without exposing creation logic.

   Angular's dependency injection system internally follows the Factory pattern to create and provide service instances.

4. **Facade Pattern:** I frequently use the Facade pattern with NgRx to hide state management complexity and provide a simple API for components.

5. **Strategy Pattern:** Switch behavior dynamically without changing the client code.
   The Strategy pattern allows different algorithms or behaviors to be selected at runtime without modifying the calling code.

6. **Decorator Pattern:** Angular extensively uses the Decorator pattern through decorators such as `@Component`, `@Injectable`, and `@Directive`.

| Pattern   | Angular Example         |
| --------- | ----------------------- |
| Singleton | Services                |
| Observer  | RxJS Observables        |
| Factory   | Dependency Injection    |
| Facade    | NgRx Facade Services    |
| Strategy  | Dynamic Business Logic  |
| Adapter   | API Response Mapping    |
| Decorator | @Component, @Injectable |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 58 What is loosely and tight coupled in angular?

Tight Coupling: Components or services directly depend on concrete implementations, making code difficult to modify, test, and maintain.

Loose Coupling: Components or services interact through Angular Dependency Injection, interfaces, inputs/outputs, and observables, reducing dependencies and making the application more flexible, testable, and maintainable.

Angular is designed to encourage loose coupling through its Dependency Injection framework.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 59. What is Hydration?

Hydration allows Angular to reuse server-rendered HTML and make it interactive without re-rendering the entire page.

It works with SSR to improve performance, reduce rendering work, improve Core Web Vitals such as LCP, and provide a better user experience.

- When Is Hydration Used?
  - Typically with: Angular Universal (SSR) + Hydration. SSR renders the page on the server. Hydration activates it on the client.

```html
<!-- Without Hydration -->
Server ↓ HTML Sent to Browser ↓ Browser Displays HTML ↓ Angular Bootstraps ↓
Destroys Existing DOM ↓ Recreates DOM

<!-- This causes extra work and slower page rendering. -->

---

<!-- With Hydration -->
Server ↓ HTML Sent to Browser ↓ Browser Displays HTML ↓ Angular Bootstraps ↓
Reuses Existing DOM ↓ Attaches Events

<!-- No unnecessary DOM recreation. -->
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 60. What is New Control Flow (`@if`,` @for`, `@switch`),

Angular 17 introduced built-in control flow syntax such as `@if`, `@for`, and `@switch` to replace structural directives like `*ngIf` and `*ngFor`. The new syntax is more readable, easier to maintain, and provides better performance, especially with `@for`, which includes an improved diffing mechanism and built-in tracking support.

**`@if`**

```html
<!-- Before -->
<div *ngIf="isLoggedIn">Welcome User</div>

<!-- After -->
@if (isLoggedIn) {
<div>Welcome User</div>
}

<!-- Else Block -->

<!-- Before -->
<div *ngIf="isLoggedIn; else login">Welcome User</div>

<ng-template #login> Please Login </ng-template>

<!-- After -->
@if (isLoggedIn) {
<div>Welcome User</div>
} @else {
<div>Please Login</div>
}
```

**`@for`**

```html
<!-- Before -->
<div *ngFor="let user of users">{{ user.name }}</div>

<!-- After -->
@for (user of users; track user.id) {
<div>{{ user.name }}</div>
}

<!-- Empty State -->

<!-- Before -->
<div *ngIf="users.length === 0">No Users Found</div>

<!-- After -->
@for (user of users; track user.id) {
<div>{{ user.name }}</div>
} @empty {
<div>No Users Found</div>
}
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 61. What is HostBinding vs HostListener, viewChild vs viewChildren, and ViewChild vs ContentChild?

**`@HostBinding`** is used to bind properties, classes, styles, or attributes to the host element.

**`@HostListener`** is used to listen to events emitted by the host element such as click, mouseenter, or keydown.

**`ViewChild`** is used to access a single child element or component from the view.

**`ViewChildren`** is used when multiple matching elements or components need to be accessed.

`ViewChild` accesses elements and components that belong to the component's own view.

`ContentChild` accesses content projected into the component through `ng-content`. `ViewChild` works with the component template, whereas `ContentChild` works with projected content.

`@HostBinding` binds properties or styles to the host element, while `@HostListener` listens to host element events. `ViewChild` retrieves a single element or component from the component's own template, `ViewChildren` retrieves multiple matching elements as a `QueryList`, and `ContentChild` is used to access content projected through `ng-content`. `ViewChild/ViewChildren` work with the view, whereas `ContentChild` works with projected content.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 62. Coding Standards & Code Quality Tools?

- **Angular Style Guide:** Follow Angular's recommended folder structure, naming conventions, component architecture, and best practices to maintain consistency across the application.

- **ESLint:** Enforces coding standards, catches code smells, and prevents common development mistakes.

- **Prettier:** Automatically formats code to ensure a consistent coding style across the team.

- **SonarQube:** Identifies code smells, security vulnerabilities, duplicate code, technical debt, and test coverage issues.

- **Jest / Karma:** Helps maintain code quality through automated unit and integration tests.

- **GitHub Actions / Azure DevOps / Jenkins:** Automates linting, testing, security scans, and deployment through CI/CD pipelines.

- **GitHub Copilot:** AI coding assistant that suggests code, test cases, and implementation patterns.

- **Cursor AI:** AI-powered IDE that assists with code reviews, refactoring, debugging, and code explanations.

- **CodeRabbit:** AI code reviewer that analyzes pull requests and provides suggestions for improvements and bug fixes.

- **Husky:** Runs automated checks such as linting and tests before allowing commits.

- **lint-staged:** Executes linting and formatting only on changed files to speed up pre-commit validation.

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

### Q 63. How do you deploy the build?

**CI/CD Deployment Flow**

- Developer raises a Pull Request (PR)
  - Code is reviewed by team members before merging.
- CI Pipeline Triggered
  - Runs ESLint and Prettier checks.
  - Executes unit test cases (Jasmine/Jest).
  - Runs SonarQube analysis for code quality, security vulnerabilities, and code coverage.
- Build Generation
  - Angular production build is created using:
  - `ng build --configuration production`
  - Build artifacts are generated and versioned.
- Artifact Storage
  - The generated artifact is stored in the CI/CD platform (Azure DevOps Artifacts, Nexus, Artifactory, etc.).
  - Each artifact has a unique version/build number.
- Secrets Management
  - Secrets are stored in HashiCorp Vault.
  - CI/CD pipeline retrieves secrets securely during deployment.
  - Secrets are never stored in source code or Git repositories.
- Deployment
  - CD pipeline picks the approved artifact.
  - Deploys to Dev → QA/UAT → Production environments.
  - Environment-specific configurations are injected during deployment.
- Post-Deployment Validation
  - Smoke tests.
  - Health checks.
  - Application monitoring and log verification.
- Rollback Strategy
  - If an issue is detected, no new build is created.
  - Redeploy the previous stable artifact version.
  - Since artifacts are immutable and already tested, rollback is fast and low risk.

**Rollback:** For our Angular application, we don't maintain separate rollback code. Every release generates a versioned artifact that is stored in the artifact repository. If a deployment fails, we redeploy the previous stable artifact through the release pipeline.

```yml
trigger:
  branches:
    include:
      - main

pool:
  vmImage: "ubuntu-latest"

steps:
  # Install Node.js
  - task: NodeTool@0
    inputs:
      versionSpec: "20.x"

  # Install dependencies
  - script: |
      npm install
    displayName: "Install Dependencies"

  # Run Lint
  - script: |
      npm run lint
    displayName: "Run ESLint"

  # Run Unit Tests
  - script: |
      npm run test -- --watch=false --browsers=ChromeHeadless
    displayName: "Run Unit Tests"

  # SonarQube Analysis
  - task: SonarQubePrepare@5
    inputs:
      SonarQube: "SonarQube-Service"
      scannerMode: "CLI"

  - task: SonarQubeAnalyze@5

  - task: SonarQubePublish@5
    inputs:
      pollingTimeoutSec: "300"

  # Angular Production Build
  - script: |
      npm run build -- --configuration production
    displayName: "Build Angular App"

  # Publish Artifact
  - task: PublishBuildArtifacts@1
    inputs:
      PathtoPublish: "dist"
      ArtifactName: "angular-app"
```

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

<!-- ### Q . Error

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div> -->

### Q . Angular Release History (Quick Interview Recap).

| Version           | Year     | Major Updates                                                                                                                           |
| ----------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| **AngularJS 1.x** | 2010     | First Angular framework, MVC architecture, two-way data binding, dependency injection                                                   |
| **Angular 2**     | 2016     | Complete rewrite of AngularJS, introduced **TypeScript**, component-based architecture                                                  |
| Angular 4         | 2017     | Smaller bundle size, improved **AOT compilation**, faster rendering                                                                     |
| Angular 5         | 2017     | Build optimizer, **HttpClient module**, improved compiler                                                                               |
| Angular 6         | 2018     | **Angular CLI improvements**, Angular Elements, RxJS 6 support                                                                          |
| Angular 7         | 2018     | **Virtual scrolling**, CLI prompts, performance improvements                                                                            |
| Angular 8         | 2019     | **Differential loading**, dynamic imports, web workers                                                                                  |
| Angular 9         | 2020     | **Ivy rendering engine** enabled by default                                                                                             |
| Angular 10        | 2020     | Better TypeScript integration, stricter project configuration                                                                           |
| Angular 11        | 2020     | Faster builds, improved **Hot Module Replacement (HMR)**                                                                                |
| Angular 12        | 2021     | Ivy everywhere, improved build system, strict typing                                                                                    |
| Angular 13        | 2021     | **View Engine removed**, Ivy fully adopted                                                                                              |
| Angular 14        | 2022     | **Typed Reactive Forms**, standalone component preview                                                                                  |
| Angular 15        | 2022     | **Standalone components stable**, simplified module usage                                                                               |
| Angular 16        | 2023     | **Signals introduced**, improved hydration, better performance                                                                          |
| Angular 17        | 2023     | **New control flow (`@if`, `@for`)**, deferrable views                                                                                  |
| Angular 18        | 2024     | **Signals improvements**, zoneless experiments, performance upgrades                                                                    |
| Angular 19        | 2024     | Improved server rendering, better hydration and performance                                                                             |
| Angular 20        | 2025     | Continued **signals-first architecture**, improved build tools and developer experience                                                 |
| Angular 20        | May 2025 | Modern build pipeline, SSR improvements                                                                                                 |
| Angular 21        | Nov 2025 | Zoneless change detection, Signal Forms improvements                                                                                    |
| Angular 22        | Jun 2026 | Signal Forms stable, Zoneless default for new projects, OnPush default for new components, template and API enhancements ([Angular][1]) |

[1]: https://angular.dev/reference/releases?utm_source=chatgpt.com "Versioning and releases • Angular"

The biggest Angular milestones were Ivy in Angular 9, Standalone Components in Angular 14/15, Signals in Angular 16, the new control flow and deferred loading in Angular 17, and the continued move toward zoneless change detection and SSR improvements in Angular 18-20. These changes focus on better performance, simpler APIs, and improved developer experience. |

<div align="right"><b><a href="#angular">↥ Back to top</a></b></div>

##
