MVC

Model:

- Adding and Retrieving items from DB
- processing data from or to the db
- speaks only with the controller

View:

- this is the only thing the user ever sees
- usually consists of HTML/CSS
- speaks only with the controller (never talks back!!)

Controller:

- processes GET/POST/PUT/DESTROY requests
- All server side logic
- takes info from user
- processes info and talks to the DB if needed
- receives info from DB
- speaks to view to explain presentation to the viewer



Jet:

-  is a toolkit of solutions for enterprise JS
- provides a stable architecture 
- fronted of applications that interact with Cloud services



![1](img\1.PNG)



![2](C:\Project\jet-tutorial\img\2.PNG)

ojet build - builds application

oject serve - start server



Data Binding

Knockout

specializes in data binding

binds view in HTML, to business logic in JS

two way data binding



**Observables**

Knockout.js używa observables (obserwatorów) do śledzenia właściwości  w ViewModel. Według koncepcji działają jak normalne JavaScript’owe  zmienne, ale pozwalają Knockout’owi *obserwować* ich zmiany i automatycznie aktualizować istotne miejsca w widoku.

an "observable" or "observableArray" is a special type of two-way data binding variable used by Knockout

When the value is changed by either the UI or the JS viewModel the other references to the observable are automatically updated as well



## Oracle Jet Components

powerful & clean way of organising UI Code into self-contained reusable chunks

dev pattern beneficial for large applications, simplifying through encapsulation

iprove performance by incremental loading of resources



## Require.js Text Plugin

Extension of require.js

free and open source library included in Oracle JET

enables you to load resources

lets you separate HTML templates from business logic in JS files



## cli 

ojet help create

you can get examples of commands 

## Modules

oracle JET applications are inherently modular

an oracle module has its business logic in JS and its view in JS

{{val}}

- Read-write. (it setts listeners everywhere)
- Two-way data binding

[[val]]

- Read-only. 
- One-way data binding

it converts array into a table  

```javascript
self.dataprovider = new ArrayDataProvider(deptArray, {keyAttributes: 'name', implicitSort: [{attribute: 'name', direction: 'ascending'}]});
```

## REST Services

getJSON

```javascript
self.data = ko.observableArray();
$.getJSON("https://").then
(
function(myData) {
    var tempArray = [];
    $.each(myData, function () ){
           tempArray.push( {
          	name: this.name,
           population: this.population
           });
           });
		self.data(tempArray);
});
self.datasource = new oj.ArrayTableDataSource(
	self.data,
    {idAttribute: 'name'}
)
```

## For Each

```html
<oj-bind-for-each data="[[chemicals]]" as="chemical">
    <template>
    <span class = "oj-panel oj-panel-alt4">
        <oj-bind-text value="[[chemical.data.name]]"></oj-bind-text> 
        </span>
    </template>
```

data in model looks like:

self.chemicals = [

{name: "h2o"},

{name: "co4"}

];

Start json 

json-server index.js

```
<span data-bind="text: $context.row.id"></span>
```

