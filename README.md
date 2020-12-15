#### Component
Component Selector have 3 ways format.
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
### Property Binding
Used for dynamic values or changing values it works with strings, numbers, booleans(true/false), and changing values unlike intepolation "{{}}" only works with string values.
Attribute - HTML
Property - (DOM)
```
@Component({
selector: 'app-test',
template: `
    <div>
        <h1>{{ title_name }}</h1>
        <input [id]="myId" type='text' /> <!-- Property binding, it works with numbers, booleans(true/false), changing values -->
        <input id="{{ myId }}" type='text' /> <!-- Interpolation, only works with string values and it's not changing if already have a value -->
        <input [disabled]="myStatus" type='text' /> <!-- Property binding using [] on the attribute "disabled" -->
        <input bind-disabled="myStatus" type='text' /> <!-- Property binding using "bind-" on the attribute "disabled"-->
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
