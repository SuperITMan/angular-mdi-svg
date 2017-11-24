# angular-mdi-svg
Material Design Icons mdi.svg file for Angular(JS) Material.
Based on [MaterialDesign](https://github.com/Templarian/MaterialDesign) project, there is a CRON behind this project to pull the last version of the **mdi.svg** file from [https://materialdesignicons.com](https://materialdesignicons.com).

Add the following plugin configuration in webpack config:
```javascript
new CopyWebpackPlugin([
  { from: 'node_modules/angular-mdi-svg/mdi.svg',
    to: 'assets/mdi.svg'
  }
]);
```


## Usage
This bundle is usable with Angular(JS) Material and to facilitate his usage, it's recommended to use [copy-webpack-plugin](https://github.com/webpack-contrib/copy-webpack-plugin). 
### Angular 2.x/4.x/5.x
```typescript App module
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { NgModule } from '@angular/core';
import { MatIconRegistry, MatIconModule } from '@angular/material';
import { DomSanitizer } from '@angular/platform-browser';
import { HttpModule } from '@angular/http';
/*
From the latest master, HttpClientModule is required instead
import { HttpClientModule } from '@angular/common/http';
*/

...
@NgModule({
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    HttpModule,
    // From the latest master, HttpClientModule is required instead
    // Your other modules
    // Take note that you have to import MatIconModule into your app
    MatIconModule
  ]
})
export class AppModule {
  constructor(matIconRegistry: MatIconRegistry, domSanitizer: DomSanitizer){
    matIconRegistry.addSvgIconSet(domSanitizer.bypassSecurityTrustResourceUrl('./assets/mdi.svg')); // Or whatever path you placed mdi.svg at
  }
}
```

If you're using Angular CLI, make sure to include `assets` folder under `.angular-cli.json` in `assets` array (Although by default, the angular CLI will autofill it in):

```json Angular CLI file
{
   "apps": [
     {
       "assets": [
         "assets"
       ]
     }
   ]
}
```
Usage:

```html Example Usage
<!-- Icon by itself -->
<mat-icon svgIcon="android"></mat-icon>
<!-- Icon button -->
<button mat-icon-button>
  <mat-icon svgIcon="android"></mat-icon>
</button>
<!-- You can also combine an icon and text together -->
<button mat-button>
  <mat-icon svgIcon="code-tags"></mat-icon>
  View source
</button>
```

Please also add the following class to your styles (`styles.css`) to solve the problem where an icon isn't aligned properly when used in a menu item:

```css styles.css
button.mat-menu-item {
  line-height: 24px !important;
}
a.mat-menu-item > mat-icon {
  margin-bottom: 14px;
}
.mat-icon svg {
  height: 24px;
  width: 24px;
}
```

[Demo](https://stackblitz.com/edit/mdi-material-example)

For more information on icons, refer to the [icon docs](https://material.angular.io/components/icon/overview).

### Angular JS Material
```javascript Configuration
var app = angular.module('myApp', ['ngMaterial']);
app.config(function($mdIconProvider) {
  $mdIconProvider
    .defaultIconSet('assets/mdi.svg')
});
```

Usage:

```html Example Usage
<md-icon md-svg-icon="android"></md-icon>
<md-button aria-label="Android" class="md-icon-button">
  <md-icon md-svg-icon="android"></md-icon>
</md-button>
```
