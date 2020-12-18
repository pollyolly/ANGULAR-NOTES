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
        <h1 [style.color]="myStatus ? 'green' : 'red'">This is Blue</h1>                <!-- Conditional style binding -->
        <h1 [style.color]="myColor">This is Blue</h1>                                   <!-- String value of variable myColor="blue" -->
        <h1 [style.color]="orange">This is Blue</h1>                                    <!-- string value directly -->
        <h1 [ngStyle]="titleStyle">This text is with multiple style</h1>                <!-- Multiple style in a Style binding -->
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
#### Event Binding
$event - give information about the DOM event that was occured.
```
@Component({
selector: 'app-test',
template: `
    <div>
        <input type="button" (click)="getClick($event)" />         <!-- $event gives information about the DOM event -->
        <input type="button" (click)="iSay='This is my world!'" /> <!-- Directly initialize in HTML the value in a variable -->
        {{ iSay }}
    </div>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
     public title_name = "App Test";
     public iSay = "";
     
     constructor(){}
     getClick(event){
        console.log(event);
        this.iSay = "Hello world";
     }
}
```
#### Template reference variable
#myInput is a template reference variable used to get the HTML and DOM property.
```
@Component({
selector: 'app-test',
template: `
    <div>
        <input #myInput type="text" />                           <!-- #myInput will access DOM and HTML -->
        <input type="button" (click)="setValue(myInput.value)">  <!-- myInput.value to get the value from #myInput -->
        <input type="button" (click)="setValue(myInput)">        <!-- if .value is not added this will return the HTML "<input #myInput type="text" />" instead-->
        {{ theValue }}
    </div>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
     public title_name = "App Test";
     public theValue = "";
     
     constructor(){}
     setValue(event){
        this.theValue = "Im the value!";
     }
}
```
#### Two Way Binding
Allow to update and display the value of the property.
Needs to import Form module in angular to work.
```
@Component({
selector: 'app-test',
template: `
    <div>
        <input [(ngModel)]="theValue" type="text" />     <!-- This will update the template -->
        {{ theValue }}                                   
    </div>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
     public theValue = "";
     constructor(){}
}
```
#### ngIf Directive
ngIf is used to conditionally render the HTML.
ng-template is used as container for the HTML.
```
@Component({
selector: 'app-test',
template: `
    <h2 *ngIf="myStatus; then variableThen; else variableElse">
        This is the default value.
    </h2>
    <ng-template #variableThen> 
        <p>
            This will be showed when true!
        </p>
    </ng-template>
    
    <ng-template #variableElse>
        <p>
            This will be showed when false!
        </p>
    </ng-template>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
     public myStatus = true;
     constructor(){}
}
```
#### ngSwitch Directive 
```
@Component({
selector: 'app-test',
template: `
    <div [ngSwitch]="color">
        <div *ngSwitchCase="'blue'">Picked blue color</div>
        <div *ngSwitchCase="'red'">Picked red color</div>
        <div *ngSwitchCase="'green'">Picked green color</div>
        <div *ngSwitchDefault> Think another color! </div>
    </div>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
     public color = "blue";
     constructor(){}
}
```
#### ngFor Directive
```
@Component({
selector: 'app-test',
template: `
    <div [ngFor]="let color of theColors">
           {{color}}
    </div>
    <div [ngFor]="let color of theColors;index as i">
           {{i}}  {{color}}
    </div>
    <div [ngFor]="let color of theColors;first as i">
           {{i}}  {{color}} <!-- This will be true if the first index and false if not -->
    </div>
    <div [ngFor]="let color of theColors;last as i">
           {{i}}  {{color}} <!-- This will be true if the last index and false if not -->
    </div>
    <div [ngFor]="let color of theColors;even as i">
           {{i}}  {{color}} <!-- This will be true if even index and false if not -->
    </div>
    <div [ngFor]="let color of theColors;odd as i">
           {{i}}  {{color}}  <!-- This will be true if odd index and false if not -->
    </div>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
     public theColors = ["blue","red","green"];
     constructor(){}
}
```
#### Component 
Communicate from Parent To Child Component
Parent to Child Component to Child Component is not possible.
```
//Parent Component
@Component({
selector: 'app-test',
template: `
    {{ myMessage }}
    <app-test-two (childEvent)="myMessage=$event" [parentData]="name"></app-test-two>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
    public name = "Who I am?";
    public myMessage = "";
     constructor(){}
}

//Child Component
@Component({
selector: 'app-test-two',
template: `
    <h2>{{ parentData }}</h2>
    <h2>{{ parentDataTwo }}</h2>
    <button (click)="fireEvent()">Send Message</button>
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
    @Input() public parentData;                         //receiving the parentData from Parent Component [parentData]="name"
    @Input('parentData') public parentDataTwo;          //aliasing the parentData
    @Output() public childEvent = new EventEmitter();   //only way to send data from Child Component to Parent Component using event
     constructor(){}
     
     fireEvent(){
        this.childEvent.emit('Hello Parent I'm here from child component!!'):
     }
}
```
#### Pipe
```
@Component({
selector: 'app-test',
template: `
    <p>{{ name | uppercase }}</p>
    <p>{{ nametwo | lowercase }}</p>
    <p>{{ name | titlecase }}</p>
    <p>{{ name | slice:3:5 }}</p>                   <!-- starting from 0 cut from position 3 to 4 the result is "an" -->
    <p>{{ myJson | json }}</p>                      <!-- {"firstname": "Dianna","lastname": "Zubiri"} -->
    
    <p>{{ number | number:'1.2-3' }}</p>            <!-- 5.679 --> <!-- 1 integer value dot minimum 2 decimal and maximum 3 decimal value -->
    <p>{{ number | number:'3.4-5' }}</p>            <!-- 005.67900  -->
    <p>{{ number | number:'3.1-2' }}</p>            <!-- 5.67 -->
    
    <p>{{ 0.25 | percent }}</p>                     <!-- 25% -->
    
    <p>{{ 0.25 | currencey }}</p>                   <!-- default $ dollar -->
    <p>{{ 0.25 | currencey:'PHP' }}</p>             <!-- P0.25 -->
    <p>{{ 0.25 | currencey:'EUR':'code' }}</p>      <!-- EUR0.25 -->
    
    <p>{{ date }}</p> <!--  -->
    <p>{{ date | date:'short' }}</p>                <!-- 12/3/17 9:49 PM -->
    <p>{{ date | date:'shortDate' }}</p>            <!-- 12/3/17 -->
    <p>{{ date | date:'shortTime' }}</p>            <!-- 9:49 PM -->
`,
styles: [`

  `]
});
export class NameComponent implements OnInit {
     public name = "lhana roades";
     public nametwo = "LHANA ROADES";
     public myJson = {
        "firstname": "Dianna",
        "lastname": "Zubiri"
     };
     public number = 5.67900000;
     constructor(){}
}
```
#### Service
```
```
