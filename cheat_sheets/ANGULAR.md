# ANGULAR

[home page](https://angular.io/)
[material Angular](https://material.angular.io/)

## WHAT IS IT

## ANGULAR CLI

[home page](https://cli.angular.io/)

### what is it
Angular CLI is a very powerful CLI which nicely complements (or even sustain) the Angular landscape. it is the key tool which you will be living by as soon as you start creating app, component, directive,.... anything in Angular.
better to get familiarized with it.

https://medium.com/codingthesmartway-com-blog/creating-angular-projects-with-angular-cli-e32b2cb486da

## SETUP

## HELLO WORLD

## BASICS OF COMPONENTS AND DIRECTIVES

## ONE LEVEL DEEPER

### ANGULAR Forms
https://blog.ng-book.com/the-ultimate-guide-to-forms-in-angular-2/ 


#### Reactive Forms

#### how to deactivate forms based on entry of another field
see [here](https://www.technouz.com/4725/disable-angular-reactiveform-input-based-selection/)
example of situation is profile editor which we want to be editable on demand
https://www.technouz.com/4725/disable-angular-reactiveform-input-based-selection/

## MORE DETAILS


### ANGULAR MATERIAL
[home page](https://material.angular.io/)
#### THEMING YOUR APP
example [here](https://www.positronx.io/create-angular-material-8-custom-theme/)

### NGX-Permissions
Ngx permission is an angular package which allows to enable RBAC on the front end. Stay aware though it is not changing the strategy in place on your back-end.

### PROGRESSIV WEBAPP

### REALTIME app
https://www.djamware.com/post/5e50b735525fc968b04a707f/mean-stack-angular-9-build-realtime-crud-web-app-quickly#express-router 

### SERVICE WORKERS / WEBWORKERS

### Authentication with Firebase
[here](https://www.youtube.com/watch?v=O_jxEC0hWcA&t=225s)

### UI LIBRARY


- [PrimeNG](https://primefaces.org/primeng/showcase/#/setup): offers more than 70 UI component ready to use in angular webapp
- [GoldenLayout](https://github.com/EmbeddedEnterprises/ng6-golden-layout): has a docking windows mechanism
  
### Theming your app

dynamic themes
- change the stylesheet: http://www.carbonrider.com/2019/03/27/angular-change-theme-at-runtime/
- with observable and class on component: https://blog.wb.gy/build-dynamic-themes-for-angular-material/
- https://nerdhut.de/2020/01/13/dynamic-angular-material-themes/
  
Theme can be applied either on the entirety of the app or to a subpart of it.
They can be changed dynamically.
Let's see how the inner panel only of our app can be themed with a dynamic change.

Note: many references over the internet indicates to use either ``--style=sass`` or ``--style=scss`` option for the creation of the app with ``angular CLI``, it seems that ``scss`` is the only really working.

#### creation of the theme
There are plenty of tutorial for the creation of the theme itself. Let's not dig into this here.
Good practice is to avoid modifying the ``styles.scss`` which is found into ``src`` folder. This one is not meant to host theme and this would create confusion in the code structure.
Instead, one should consider the ``theme`` as an asset of the application and describe into the ``assets\themes`` folder which one will create.
In this folder, have a ``xxx-theme.scss`` file created and simply import it into your ``src\styles.scss``.
````scss
@import "./assets/styles/xxx-theme";
````

In your ``xxx-theme.Scss`` file have the proper styles created or referenced
````scss
@import "~@angular/material/theming";

@include mat-core();

$primary: mat-palette($mat-indigo);
$accent: mat-palette($mat-pink, A200, A100, A400);
$warn: mat-palette($mat-red);
$theme: mat-light-theme($primary, $accent, $warn);

@include angular-material-theme($theme);

// Our dark theme
.dark-theme {
  color: $light-primary-text;
  $dark-primary: mat-palette($mat-yellow);
  $dark-accent: mat-palette($mat-amber, A400, A100, A700);
  $dark-warn: mat-palette($mat-red);
  $dark-theme: mat-dark-theme($dark-primary, $dark-accent, $dark-warn);

  @include angular-material-theme($dark-theme);
}
````

Now that the files are created, let's consider how to use them into the application.

#### applying a theme
the angular Material document refers to an ``OverlayKit`` or something. this is to be furter explored especially when using custom component it seems.

the most efficient approach for dynamically changing the style of a component is to use ``class binding``.
So in the component which is to be theme, add the following piece of code:
````html
    <div [ngClass]="{'dark-theme': isThemeDark | async}">
      <div class="mat-app-background">
        
      </div>
    </div>
````
the class binding allows then to dynamically change the class (note the usage of observable here with the ``async`` pipe).

In the Typescript component code, one shall add the reference to the theme itself,
````ts
... //add the observable for class binding
isThemeDark: Observable<boolean>;
...
````
This observable is initialized during OnInit to connect to the a service in which the theme is modified.
This service is ``ThemeService``. It will be described later on.
in your component,
- inject the ThemeService
- initialize isThemeDark to the said reference in ThemeService
  
````ts
constructor(private breakpointObserver: BreakpointObserver,
            ...
            private theme: ThemeService
            ) {}

ngOnInit(){
  this.auth.logout();
  this.isThemeDark = this.theme.isThemeDark;
}
````
Last but not least, one must add in the UI a way to select the theme itself.
Let's put it, for now, as a simple toggle button which triggers a function in the component.
````html
    <mat-slide-toggle
      [checked]="isThemeDark | async"
      (change)="onChangeTheme($event.checked)"
      >Dark theme</mat-slide-toggle
    >
````
add this function in the component code
````ts
  onChangeTheme(checked: boolean){
    this.theme.setTheme(checked);
  }
````

#### capturing the change event and propagating
last but not least, let's create our service for Theme management.
So far, not firm recommendation as per where to put this service, so I put it into shared (as it is likely to be shared...).

````ts
import { Injectable } from '@angular/core';
import { Subject } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ThemeService {
private themeDark: Subject<boolean> = new Subject<boolean>();
isThemeDark = this.themeDark.asObservable();
  constructor() { }

  setTheme(theme: boolean){
    this.themeDark.next(theme);
  }
}
````
Code is pretty simple it offers the possibility to change the theme with the ``setTheme`` which only swithes the subject ``boolean``.
Then a public Observable is shared on the Subject... this is the observable that we will connect to.

### ROUTING AND NAVIGATION 

Let's presume I got this router config
```` typescript
export const EmployeeRoutes = [
   { path: 'sales', component: SalesComponent },
   { path: 'contacts', component: ContactsComponent }
];
````
and have navigated to the SalesComponent via this URL

/department/7/employees/45/sales
Now I'd like to go to contacts, but as I don't have all the parameters for an absolute route (e.g. the department ID, 7 in the above example) I'd prefer to get there using a relative link, e.g.
```` typescript
[routerLink]="['../contacts']" ````
or
```` typescript
this.router.navigate('../contacts')
````
which unfortunately doesn't work. There may be an obvious solution but I'm not seeing it. Can anyone help out here please?


The RouterLink directive always treats the provided link as a delta to the current URL:
```` typescript
[routerLink]="['/absolute']"
[routerLink]="['../../parent']"
[routerLink]="['../sibling']"
[routerLink]="['./child']"     // or
[routerLink]="['child']" 

// with route param     ../sibling;abc=xyz
[routerLink]="['../sibling', {abc: 'xyz'}]"
// with query param and fragment   ../sibling?p1=value1&p2=v2#frag
[routerLink]="['../sibling']" [queryParams]="{p1: 'value', p2: 'v2'}" fragment="frag"
````
The navigate() method requires a starting point (i.e., the relativeTo parameter). If none is provided, the navigation is absolute:
```` typescript
constructor(private router: Router, private route: ActivatedRoute) {}

this.router.navigate(["/absolute/path"]);
this.router.navigate(["../../parent"], {relativeTo: this.route});
this.router.navigate(["../sibling"],   {relativeTo: this.route});
this.router.navigate(["./child"],      {relativeTo: this.route}); // or
this.router.navigate(["child"],        {relativeTo: this.route});

// with route param     ../sibling;abc=xyz
this.router.navigate(["../sibling", {abc: 'xyz'}], {relativeTo: this.route});
// with query param and fragment   ../sibling?p1=value1&p2=v2#frag
this.router.navigate(["../sibling"], {relativeTo: this.route, 
    queryParams: {p1: 'value', p2: 'v2'}, fragment: 'frag'});

// RC.5+: navigate without updating the URL 
this.router.navigate(["../sibling"], {relativeTo: this.route, skipLocationChange: true});  
````

If you are using the new router (3.0.0-beta2), you can use the ActivatedRoute to navigate to relative path as follow:
```` typescript
constructor(private router: Router, private r:ActivatedRoute) {} 

///
// DOES NOT WORK SEE UPDATE
goToContact() {
  this.router.navigate(["../contacts"], { relativeTo: this.r });
}
````
Update 08/02/2019 Angular 7.1.0
current route: /department/7/employees/45/sales

the old version will do: /department/7/employees/45/sales/contacts

As per @KCarnaille's comment the above does not work with the latest Router. The new way is to add .parent to this.r so
```` typescript
    // Working(08/02/2019) 
    goToContact() {
       this.router.navigate(["../contacts"], { relativeTo: this.r.parent });
    }
````
the update will do: /department/7/employees/45/contacts

#### authentication
https://auth0.com/blog/complete-guide-to-angular-user-authentication/


### is loading service
https://gitlab.com/service-work/is-loading


### Connect to Git Hub
standard http request sent from a serice
https://scotch.io/courses/build-your-first-angular-website/creating-a-user-service-to-connect-to-github 

````typescript
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class GithubService {

  gitHubURL = 'https://api.github.com';
  constructor(private http: HttpClient) { }

  getUsers(){
    // in parameter give the API to be used.
    return this.http.get(`${this.gitHubURL}/users/nuscracker25/repos`);
  }

  getFile(){
    return this.http.get(`${this.gitHubURL}/repos/nuscracker25/stapleMD/contents/ANGULAR.md`);
  }


}
````

clean code on http request
````typescript
 getIssues(url?: string): Observable<any> {
    if (url) {
      return this.http.get(url, { observe: 'response' })
        .pipe(
          catchError(this.handleError('getIssues', []))
        );
    } else {
      return this.http.get('https://api.github.com/repos/angular/angular.js/issues?per_page=10', { observe: 'response' })
        .pipe(
          catchError(this.handleError('getIssues', []))
        );
    }
  }

  /**
  * Get a single issue by issue number.
  *
  * @param num: number - number of the issue to fetch
  */
  getIssue(num: number): Observable<any> {
    const url = `https://api.github.com/repos/angular/angular.js/issues/${num}`;
    return this.http.get(url).pipe(
      catchError(this.handleError('getIssue', []))
    );
  }

  /**
 * Get comments by issue number.
 *
 * @param num: number - number of the issue to fetch comments for
 */
  getComments(num: number): Observable<any> {
    const url = `https://api.github.com/repos/angular/angular.js/issues/${num}/comments`;
    return this.http.get(url).pipe(
      catchError(this.handleError('getComments', []))
    );
  }

  /**
   * Handle Http operation that failed.
   * Let the app continue.
   * @param operation - name of the operation that failed
   * @param result - optional value to return as the observable result
   */
  private handleError<T>(operation = 'operation', result?: T) {
    return (error: any): Observable<T> => {

    console.error(`${operation} failed: ${error.message}`);

      // Let the app keep running by returning an empty result.
      return of(result as T);
    };
  }
````

https://github.com/tabvn/angular2.github.api/tree/master/src/app/services

## ANGULAR app backed by firebase
### firebase
is a google Storage as a Service that offers an interesting free tier
mostly nosql database
it also offers a service for real time data base
and option to host a webapp

any google account can access it

### the project
a webapp for ship vocabulary references with books and author
front end is angular based. 
source code stored on git
content file (extended stored on github)
details files are markdown
one is expecting to trace evolution of modification brought to the database.

#### set up your database
navifate to the firebase console: https://flatlogic.com/blog/low-code-no-code-development-platforms/
where you will be asked to accept the terms and condition.
The Firebase console is where you can see all your projects (you can have an infinite number of those)
![firebase console](img/Firebase%20console.png)

Follow the steps for creating a project.

Then add a database to your project:
select a Cloud Firestore database 
![firestore console](img/Cloud%20Firestore -%20Console%20Firebase.png)

select the "Start in test mode" which allows for any developper to modify the database
![firestore:test mode](img/Cloud%20Firestore -%20creation_test%20mode.png)

you will then be transported to the collection manager where you will have to start populating your database with a first collection and an initial element in it
follow the wizard to get your first element created
![firestore:first_element](img/Cloud Firestore -%20First%20Collection.png)

at this point you have laid out the foundation of your database. you'll need to get the required information to access:
- navigate the settings of your project
- in the section project parameters, scroll down to the bottom where you can add an application to your firebase database. this will share the details to be used in any API call. this information are obviously to be kept secret.
- selecting the web application </> will show the details
- 
### Angular application creation 
standard set of command
````shell
ng new <application></application> --routing --style=scss
cd <application>
ng add @angular/material
npm install --save ngx-logger
npm install --save firebase @angular/fire
cd src
cd app
ng g m core
ng g m shared
ng g m feature --routing
ng add @angular/pwa --project sol-XVIII
cd feature

````
in sequence
1. creation of angular project with router and scss style
2. cd into application
3. install ngx-logger (very good logging tool)
4. install firebase component in app
5. navigate to src of app
6. structure app with core, shared
7. add a feature module with routing
8. add PWA support into project
9. navigate to feature

then creation of main navigation using material schematic
````shell
ng generate @angular/material:navigation home
````
### configuration of the app to firebase

in your environments/environment.js file add the firebaseConfig which you can get from the admin panel of your app in firebase console

````typescript
export const environment = {
  production: false,
  firebaseConfig : {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_STORAGE_BUCKET",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
  }
};
````
the above information being confidential, it is recommended not to publish them anywhere (especially not on yout github account)

Then the Firebase module are added into you ``src/app/app.module.ts

````typescript
import { AngularFireModule } from '@angular/fire';
import { AngularFireDatabaseModule } from '@angular/fire/database';
import { environment } from '../environments/environment';

@NgModule({
        // [...]
    imports: [
        // [...]
        AngularFireModule.initializeApp(environment.firebaseConfig),
        AngularFireDatabaseModule
    ],
````
if you work with an active server screening your modification (``ng serve``) you will see an error message once these modification are done. Simply stop ``CTRL + C`` in you shell then restard ``ng s``.

### creation of the angular model
always good to have your angular models to structure your code and secure

````shell
ng g class <name> --type=model
````
These models belong to the business model part of the application. Let's have them defined and stored into the ``core`` module of the application.

### Angular Service to cope with this new model
creation of the service for coping with people definition
``ng g service people``

In the newly created people.service.ts,
add the appropriate import and inject the dependencies

````typescript
import { Injectable } from '@angular/core';
import { AngularFirestore } from '@angular/fire/firestore';

@Injectable({
  providedIn: 'root'
})
export class PeopleService {
 constructor(
    private firestore: AngularFirestore,
    private logger: NGXLogger
  ) { }

  /**
   * offers access to the people list
   */
  getPeoples(){
    return this.firestore.collection('people').snapshotChanges().pipe(
      map(actions => {

        return actions.map(a => {
          const data = a.payload.doc.data() as People;
          const id = a.payload.doc.id;
         // data.uid = id;
          return {id, ...data };
        });
      })
    );
  }

  /**
   * creates a new people in the database
  */
 createPeople(people: People){
   return this.firestore.collection('people').add(people);
 }

 updatePeople(people: People){
   delete people.id; // delete the id of said people
   this.firestore.doc('people/'+people.id).update(people);
 }

 deletePeople(peopleId: string){
   this.firestore.doc('people/'+peopleId).delete();
 }
}
````
Four more methods are added to respectively cover the standard CRUD operation

To render the list of people in the propert component, one adds the required service, and during ``OnInit`` register to the ``getPeople()`` the pipe is then manipulated

````typescript
    ngOnInit(){
      this.peopleService.getPeoples().subscribe(data =>{

        data => {
          this.peoples = data.map(e=> {
            return {
              id: e.payload.doc.id,
              ...e.payload.doc.data()
            } as People;
          })
        }
       });
     };
````