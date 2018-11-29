## Different version used
<pre>
     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/


Angular CLI: 7.0.2
Node: 8.11.1
OS: darwin x64
Angular:
...

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.10.2
@angular-devkit/core         7.0.2
@angular-devkit/schematics   7.0.2
@schematics/angular          7.0.2
@schematics/update           0.10.2
rxjs                         6.3.3
typescript                   3.1.3
</pre>

## Generate new project

```bash
# check first
ng new SvBaseApp --routing --prefix sv --style scss --dry-run

#once happy run it
ng new SvBaseApp --routing --prefix sv --style scss
```

## Go to the new App directory

```bash
cd SvBaseApp/
```

## Add Material design

```bash
ng add @angular/material
```

It will ask for options, I have used the following

```text
ng add @angular/material
Installing packages for tooling via npm.
npm WARN @angular/material@7.1.0 requires a peer of @angular/cdk@7.1.0 but none is installed. You must install peer dependencies yourself.

+ @angular/material@7.1.0
added 1 package in 16.927s
Installed packages for tooling via npm.
? Choose a prebuilt theme name, or "custom" for a custom theme: Purple/Green       [ Preview: https://material.angular.io?theme=purple-green ]
? Set up HammerJS for gesture recognition? Yes
? Set up browser animations for Angular Material? Yes
```

### Add material nav

```bash
# test it first
ng generate @angular/material:nav MainNav --dry-run

# then run it 
ng generate @angular/material:nav MainNav
```

Put router outlet into main nav content area

```html
<mat-sidenav-container class="sidenav-container">
  <mat-sidenav #drawer class="sidenav" fixedInViewport="true"
      [attr.role]="(isHandset$ | async) ? 'dialog' : 'navigation'"
      [mode]="(isHandset$ | async) ? 'over' : 'side'"
      [opened]="!(isHandset$ | async)">
    <mat-toolbar>Menu</mat-toolbar>
    <mat-nav-list>
      <a mat-list-item href="#">Link 1</a>
      <a mat-list-item href="#">Link 2</a>
      <a mat-list-item href="#">Link 3</a>
    </mat-nav-list>
  </mat-sidenav>
  <mat-sidenav-content>
    <mat-toolbar color="primary">
      <button
        type="button"
        aria-label="Toggle sidenav"
        mat-icon-button
        (click)="drawer.toggle()"
        *ngIf="isHandset$ | async">
        <mat-icon aria-label="Side nav toggle icon">menu</mat-icon>
      </button>
      <span>SvBaseApp</span>
    </mat-toolbar>
    <router-outlet></router-outlet>
  </mat-sidenav-content>
</mat-sidenav-container>

```

and replace everything in `app.component.html` with Main Nav component, like so

```html
<sv-main-nav></sv-main-nav>
```

### Create a dashboard 

generate dashboard component

```bash
# test first
ng generate @angular/material:dashboard Home --dry-run

# then run it 
ng generate @angular/material:dashboard Home
```

add dashboard to the route (`app-routing.module.ts`)

```typescript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { HomeComponent } from './home/home.component';

const routes: Routes = [{
  path: '',
  component: HomeComponent
}];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

```

