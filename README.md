#### References
```
https://www.youtube.com/watch?v=Y6OP-lPJxgs&list=PLC3y8-rFHvwhBRAgFinJR8KHIrCdTkZcZ&index=7
https://stackblitz.com/angular/kkaakmpqgjm?file=src%2Fapp%2Fhero.service.ts
https://angular.io/guide/example-apps-list
```
#### Component
Component Selector have 3 way format.
```
@Component({
selector: 'app-test',
templateUrl: './app.component.html',
styleUrls: './app.component.css'
})

selector: '[app-test]'
<div app-test>
</div>

selector: '.app-test'
<div class=".app-test">
</div>

selector: 'app-test'
<app-test></app-test>
```
Component styling and templating have also different way to add.
```
@Component({
selector: 'app-test',
template: `
    <div>
        <h1>Testing title</h1>
    </div>
`,
styles: [`
    h1 {
        color:red
    }
`]
})

Use backticks (`) to allow multiple lines in style and template.
```
#### Interpolation
Interpolation is the "{{  }}" (double curly brace) that evaluate the value in it and display the value in the browser.
*Note it will only work in string values.
```
@Component({
selector: 'app-test',
template: `
    <div>
        <h1>{{ title_name }}</h1>
    </div>
`,
styles: [`
    h1 {
        color:red
    }
`]
});
export class NameComponent implements OnInit {
     public title_name = "App Test";
     constructor(){}
}
```
#### Property Binding
Used for dynamic values or changing values it works with strings, numbers, booleans(true/false), and changing values unlike interpolation "{{}}" only works with string values.

Attribute - HTML

Property - (DOM)
```
@Component({
selector: 'app-test',
template: `
    <div>
        <h1>{{ title_name }}</h1>
        <input [id]="myId" type='text' />                   <!-- Property binding, it works with numbers, booleans(true/false), changing values -->
        <input id="{{ myId }}" type='text' />               <!-- Interpolation, only works with string values and it's not changing if already have a value -->
        <input disabled="{{ myStatus }}" type='text' />     <!-- Interpolation, This will work one time, but the value will not change forever -->
        <input [disabled]="myStatus" type='text' />         <!-- Property binding using [] on the attribute "disabled" -->
        <input bind-disabled="myStatus" type='text' />      <!-- Property binding using "bind-" on the attribute "disabled"-->
    </div>
`,
styles: [`h1 { color:red }`]
});
export class NameComponent implements OnInit {
     public title_name = "App Test";
     public myId = "testId";
     public myStatus = false;
     constructor(){}
}
```
#### Class Binding
```
@Component({
selector: 'app-test',
template: `
    <div>
        <h1 class="text-red" [class]="footerClass" class="text-red">This is Blue</h1>   <!-- This is blue because ordinary class are overwrite by Class binding -->
        <h1 [class]="footerClass">This is Blue</h1>                                     <!-- Class binding -->
        <h1 [class.text-blue]="myStatus">This is Blue</h1>                              <!-- alternative formatting of Class binding -->
        <h1 [ngClass]="myClasses">This text is with multiple classes</h1>               <!-- Multiple classes in a Class binding -->
    </div>
`,
styles: [`
    .text-red {color:red;}
    .text-blue {color:blue;}
    .text-uppercase {text-transform: uppercase;}
    .text-italic {font-style: italic;}
  `]
});
export class NameComponent implements OnInit {
     public title_name = "App Test";
     public footerClass = "text-blue";
     public myStatus = true;
     public myClasses = {
        "text-blue": this.myStatus,
        "text-uppercase": !this.myStatus, //no effect since false
        "text-italic": this.myStatus
     }
     constructor(){}
}
```
#### Style Binding
```
@Component({
selector: 'app-test',
template: `
    <div>
        <h1 [style.color]="myColor">This is Blue</h1>                                   <!-- String value of variable myColor="blue" -->
        <h1 [style.color]="orange">This is Blue</h1>                                     <!-- string value directly -->
        <h1 [ngStyle]="titleStyle">This text is with multiple classes</h1>               <!-- Multiple style in a Style binding -->
    </div>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
     public title_name = "App Test";
     public myColor = "blue";
     public myStatus = true;
     public titleStyle = {
        fontStyle: "italic",
        color: "blue"
     }
     constructor(){}
}
```
