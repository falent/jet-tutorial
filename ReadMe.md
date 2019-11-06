Jet:

-  is a toolkit of solutions for enterprise JS
-  provides a stable architecture 
-  fronted of applications that interact with Cloud services



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



MVVM

**View:**

- behaviors, events and requires knowledge about view model
- minimize logic in views
- describe "what" not "how"
- The View ignores the Model, and uses the View Model to get the information to render and to manage the user interaction.

**ViewModel:**

- Expose properties and commands which view binds
- The View Model knows the Model, and it can use it and expose it 
- abstraction of view 
- javaScript data and logic
- avoid view-related logic (use custom bindings)

**Model:**

- simple JS Object with properties to hold your data
- usually server-side
- In a more generic vision, the Models are all the objects you think about when you have to describe your product; in a web application you get them from the server, maybe in a database.



![1](img\1.PNG)



![2](C:\Project\jet-tutorial\img\2.PNG)



The MVVM design pattern used by Knockout.JSmakes it possible to separate HTML and JS for a better development and mainstance experience

The observer design pattern enables us to easily pass data to and from HTML and JS data objects



## Observer Design Pattern

observables are functions

```javascript
class Vm {

this.word = ko.observable();

}

const myVM = new Vm();

vm.word("New word")
```



## Data Binding

Knockout

specializes in data binding

binds view in HTML, to business logic in JS

two way data binding

**Text:**

```javascript
<span data-bind="text: $context.row.id"></span>
```



**Style:**

```javascript
<tr data-bind = "style: { 'font-weight': myVariable === 'Book' ? 'bold' : normal }">
```



BindingContext tracks all the following information:

- `$parent`: This is the View Model of the parent context; for example, every binding inside a foreach binding will have the foreach view model as `$parent`
- $parents: This refers to an array with all the parents context; empty for the root View Model. You can use an indexer to traverse the hierarchy (for deep-nesting); for instance, $parents[1] will get you the 2nd ancestor and so on
- `$root:` This is the View Model of the highest parent; itself for the root view model.
-  `$rawData`: This is the original View Model, before unwrapping (to understand "unwrapping" better, imagine that you have a property, `x = ko.observable(12)`, and you execute `x()`; you are unwrapping the observable to get the value `12`) 
-  `$data`: This refers to the unwrapped View Model. 

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

ojet build - builds application

oject serve - start server

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

```js
self.chemicals = [

{name: "h2o"},

{name: "co4"}

];
```

Start json 

json-server index.js



To manipulate data:

in view:

```JS
<oj-bind-text value="[[$parent.manipuleData($context.row.name)]]"></oj-bind-text>
```

Modelview:

```JS
self.manipuleData = function (name){ return name+"hahahahaha"; };
```



## Knockout tutorial:

### jednokierunkowy widok:

```javascript
// html
<p>First name: <strong data-bind="text: firstName"></strong></p>
<p>Last name: <strong data-bind="text: lastName"></strong></p>
```



```javascript
//viewmodel

function AppViewModel() {
    this.firstName = "Bert";
    this.lastName = "Bertington";
}

// Activates knockout.js
ko.applyBindings(new AppViewModel());
```

### dwukierunkowy widok:

```javascript
// html
<p>First name: <input data-bind="value: firstName" /></p>
<p>Last name: <input data-bind="value: lastName" /></p>
```

dodajemy funkcje observable

```javascript
//viewmodel

function AppViewModel() {
    this.firstName = ko.observable("Bert");
    this.lastName = ko.observable("Bertington");
}

// Activates knockout.js
ko.applyBindings(new AppViewModel());
```

## Defining computed values

Very often, you'll want to combine or convert multiple observable values to make others. In this example, you might want to define *full name* as being *first name* plus *space* plus *last name*.

To handle this, Knockout has a concept of **computed properties** - these are *observable* (i.e., they notify on change) and they are *computed* based on the values of other observables.

```javascript
// html
<p>First name: <input data-bind="value: firstName" /></p>
<p>Last name: <input data-bind="value: lastName" /></p>
<p>Full name: <strong data-bind="text: fullName"></strong></p>
```

dodajemy funkcje observable

```javascript
//viewmodel
function AppViewModel() {
    this.firstName = ko.observable("Bert");
    this.lastName = ko.observable("Bertington");
    	this.fullName = ko.computed(function() {
    		return this.firstName() + " " + this.lastName();    
		}, this);
}



// Activates knockout.js
ko.applyBindings(new AppViewModel());
```

## Click behavior

 First, add a `capitalizeLastName` function to the viewmodel to implement this behavior: 

```javascript
// html
<p>Full name: <strong data-bind="text: fullName"></strong></p>
<button data-bind="click: capitalizeLastName">Go caps</button>
```

dodajemy funkcje observable

```javascript
function AppViewModel() {
    // ... leave firstName, lastName, and fullName unchanged here ...

    this.capitalizeLastName = function() {
        var currentVal = this.lastName();        // Read the current value
        this.lastName(currentVal.toUpperCase()); // Write back a modified value
    };
}
```

## Collections

 Very often, you'll want to generate repeating blocks of UI elements, especially when displaying lists where the user can add and remove elements. Knockout lets you do that easily, using *observable arrays* and the `foreach` binding .`foreach` is part of a family of *control flow bindings* that includes [`foreach`](http://knockoutjs.com/documentation/foreach-binding.html), [`if`](http://knockoutjs.com/documentation/if-binding.html), [`ifnot`](http://knockoutjs.com/documentation/ifnot-binding.html), and [`with`](http://knockoutjs.com/documentation/with-binding.html). These make it possible to construct any kind of iterative, conditional, or nested UI based on your dynamic viewmodel. 

```javascript
// html
<h2>Your seat reservations</h2>

<table>
    <thead><tr>
        <th>Passenger name</th><th>Meal</th><th>Surcharge</th><th></th>
    </tr></thead>
    <!-- Todo: Generate table body -->
<tbody data-bind="foreach: seats">
    <tr>
        <td data-bind="text: name"></td>
        <td data-bind="text: meal().mealName"></td>
        <td data-bind="text: meal().price"></td>
    </tr>    
</tbody>
</table>
```

dodajemy funkcje observable

```javascript
// Class to represent a row in the seat reservations grid
function SeatReservation(name, initialMeal) {
    var self = this;
    self.name = name;
    self.meal = ko.observable(initialMeal);
}

// Overall viewmodel for this screen, along with initial state
function ReservationsViewModel() {
    var self = this;

    // Non-editable catalog data - would come from the server
    self.availableMeals = [
        { mealName: "Standard (sandwich)", price: 0 },
        { mealName: "Premium (lobster)", price: 34.95 },
        { mealName: "Ultimate (whole zebra)", price: 290 }
    ];    

    // Editable data
    self.seats = ko.observableArray([
        new SeatReservation("Steve", self.availableMeals[0]),
        new SeatReservation("Bert", self.availableMeals[0])
    ]);
}

ko.applyBindings(new ReservationsViewModel());
```

## Making the data editable

 You can use bindings within `foreach` blocks just the same as anywhere else, so it's pretty easy to upgrade what we've got into a full data editor. Update your view:  

```javascript
// html
<h2>Your seat reservations</h2>

<table>
    <thead><tr>
        <th>Passenger name</th><th>Meal</th><th>Surcharge</th><th></th>
    </tr></thead>
    <!-- Todo: Generate table body -->
<tbody data-bind="foreach: seats">
    <tr>
        <td><input data-bind="value: name" /></td>
        <td><select data-bind="options: $root.availableMeals, value: meal, optionsText: 'mealName'"></select></td>

        <td data-bind="text: formattedPrice"></td>
    </tr>    
</tbody>
</table>

<button data-bind="click: addSeat">Reserve another seat</button>
```

dodajemy funkcje observable

```javascript
// Class to represent a row in the seat reservations grid
function SeatReservation(name, initialMeal) {
    var self = this;
    self.name = name;
    self.meal = ko.observable(initialMeal);
    
    self.formattedPrice = ko.computed(function() {
        var price = self.meal().price;
        return price ? "$" + price.toFixed(2) : "None";        
    });
}

// Overall viewmodel for this screen, along with initial state
function ReservationsViewModel() {
    var self = this;

    // Non-editable catalog data - would come from the server
    self.availableMeals = [
        { mealName: "Standard (sandwich)", price: 0 },
        { mealName: "Premium (lobster)", price: 34.95 },
        { mealName: "Ultimate (whole zebra)", price: 290 }
    ];    

    // Editable data
    self.seats = ko.observableArray([
        new SeatReservation("Steve", self.availableMeals[0]),
        new SeatReservation("Bert", self.availableMeals[0])
    ]);
    
        // Operations
    self.addSeat = function() {
        self.seats.push(new SeatReservation("", self.availableMeals[0]));
    }
}

ko.applyBindings(new ReservationsViewModel());
```

## Remove seats

Since you can add items, you should be able to remove them too, right? As you'd expect, this is merely a matter of updating the underlying data.

Update your view so that it displays a "remove" link next to each item.

Note that the `$root.` prefix causes Knockout to look for a `removeSeat` handler on your top-level viewmodel instead of on the `SeatReservation` instance being bound --- that's a more convenient place to put `removeSeat` in this example. So, add a corresponding `removeSeat` function to your root viewmodel class, `ReservationsViewModel`: 

```javascript
// html
<h2>Your seat reservations</h2>

<table>
    <thead><tr>
        <th>Passenger name</th><th>Meal</th><th>Surcharge</th><th></th>
    </tr></thead>
    <!-- Todo: Generate table body -->
<tbody data-bind="foreach: seats">
    <tr>
        <td><input data-bind="value: name" /></td>
        <td><select data-bind="options: $root.availableMeals, value: meal, optionsText: 'mealName'"></select></td>
        <td data-bind="text: formattedPrice"></td>
        <td><a href="#" data-bind="click: $root.removeSeat">Remove</a></td>
    </tr>    
</tbody>
</table>

<button data-bind="click: addSeat">Reserve another seat</button>
```

dodajemy funkcje observable

```javascript
// Class to represent a row in the seat reservations grid
function SeatReservation(name, initialMeal) {
    var self = this;
    self.name = name;
    self.meal = ko.observable(initialMeal);
    
    self.formattedPrice = ko.computed(function() {
        var price = self.meal().price;
        return price ? "$" + price.toFixed(2) : "None";        
    });
}

// Overall viewmodel for this screen, along with initial state
function ReservationsViewModel() {
    var self = this;

    // Non-editable catalog data - would come from the server
    self.availableMeals = [
        { mealName: "Standard (sandwich)", price: 0 },
        { mealName: "Premium (lobster)", price: 34.95 },
        { mealName: "Ultimate (whole zebra)", price: 290 }
    ];    

    // Editable data
    self.seats = ko.observableArray([
        new SeatReservation("Steve", self.availableMeals[0]),
        new SeatReservation("Bert", self.availableMeals[0])
    ]);
    
        // Operations
    self.addSeat = function() {
        self.seats.push(new SeatReservation("", self.availableMeals[0]));
    }
}

ko.applyBindings(new ReservationsViewModel());
```

### Displaying a total value

Add the following `ko.computed` property inside `ReservationsViewModel`:

```javascript
// html

<h3 data-bind="visible: totalSurcharge() > 0">
    Total surcharge: $<span data-bind="text: totalSurcharge().toFixed(2)"></span>
</h3>
```

dodajemy funkcje observable

```javascript
// Class to represent a row in the seat reservations grid
function SeatReservation(name, initialMeal) {
    var self = this;
    self.name = name;
    self.meal = ko.observable(initialMeal);
    
    self.formattedPrice = ko.computed(function() {
        var price = self.meal().price;
        return price ? "$" + price.toFixed(2) : "None";        
    });
}

// Overall viewmodel for this screen, along with initial state
function ReservationsViewModel() {
    var self = this;

    // Non-editable catalog data - would come from the server
    self.availableMeals = [
        { mealName: "Standard (sandwich)", price: 0 },
        { mealName: "Premium (lobster)", price: 34.95 },
        { mealName: "Ultimate (whole zebra)", price: 290 }
    ];    

    // Editable data
    self.seats = ko.observableArray([
        new SeatReservation("Steve", self.availableMeals[0]),
        new SeatReservation("Bert", self.availableMeals[0])
    ]);
    
        // Operations
    self.addSeat = function() {
        self.seats.push(new SeatReservation("", self.availableMeals[0]));
    }
    // This example code!!
    self.totalSurcharge = ko.computed(function() {
   		var total = 0;
   		for (var i = 0; i < self.seats().length; i++)
       		total += self.seats()[i].meal().price;
   		return total;
	});
}

ko.applyBindings(new ReservationsViewModel());
```



#### Hash-based/pushState navigation 

For **hash-based** navigation, the visitor's position in a virtual navigation space is stored in the *URL hash*, which is the part of the URL after a 'hash' symbol (e.g., `/my/app/#category=shoes&page=4`). Whenever the URL hash changes, the browser *doesn't* issue an HTTP request to fetch a new page; instead it merely adds the new URL to its back/forward history list and exposes the updated URL hash to scripts running in the page. The script notices the new URL hash and dynamically updates the UI to display the corresponding item (e.g., page 4 of the "shoes" category).

This makes it possible to support back/forward button navigation in a single page application (e.g., pressing 'back' moves to the previous URL hash), and effectively makes virtual locations bookmarkable and shareable.

**pushState** is an HTML5 API that offers a different way to change the current URL, and thereby insert new back/forward history entries, without triggering a page load. This differs from hash-based navigation in that you're not limited to updating the hash fragment — you can update the entire URL.

Mamy foldery:

```javascript
// html
<!-- Folders -->
<ul class="folders" data-bind="foreach: folders">
    <li data-bind="text: $data, 
                   css: { selected: $data == $root.chosenFolderId() },
                   click: $root.goToFolder"></li>
</ul>
```

????

```javascript
function WebmailViewModel() {
    // Data
    var self = this;
    self.folders = ['Inbox', 'Archive', 'Sent', 'Spam'];
    self.chosenFolderId = ko.observable();

    // Behaviours    
    self.goToFolder = function(folder) { self.chosenFolderId(folder); };    
};

ko.applyBindings(new WebmailViewModel());
```







CSS3 introduced a new layout mode (an alternative to floats and positioning) called flexbox, which is an easy and responsive method of arranging elements on a page. To use flexbox, you simply have to specify the CSS attribute display: flex on the container elements, and any elements within the container (also called flex items) will automatically align into separate columns.



ECMA zajmuje sie standaryzacja technologii. ECMAScript JS to implementacja tego standartu

document.getElementById("nazwaElementu").innerHTML = ....



<br>
    <oj-bind-text value="[[$parent.manipuleData($context.row.name)]]"></oj-bind-text>



            self.manipuleData = function (name) {
                return name + "hahahahaha";
            };