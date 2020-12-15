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
Attribute - HTML
Property - (DOM)
