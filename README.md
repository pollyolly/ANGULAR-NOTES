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
style: `
    h1 {
        color:red
    }
`
})
```
#### Component
