# TODO-App, never forget!

### User Introduce

TODO-App is a small, light and fast todolist application.
The use is simple:

1- Type your TODO
2- Save it with "enter"

And There you go ! Your new TODO is added to your list of other TODOs!

Several possibilities are then available to you:
- By checking a TODO, it is considered completed (it is scratched and remains in the list).
- By clicking on the arrow, you can check all the boxes at once!
- You can sort the TODOs according to their completions or not.
- Delete all completed TODOs via the "clear completed" button
- You can obviously delete all the elements independently (this is your list after all 😉).

Don't worry, your list items will remain saved in your browser. 
So you can close the page, turn off your computer, walk your dog, do the dishes, and then come back. They will always be there.

## Technical documentation

This app run with JavaScript (Vannilla, ES5). 
She's build with a module paradigm.

Chrome, edge, safari and FireFox compatibility.


### Table of Contents

-   [Todo][1]
    -   [Parameters][2]
    -   [storage][3]
-   [Controller][4]
    -   [Parameters][5]
    -   [setView][6]
        -   [Parameters][7]
    -   [showAll][8]
    -   [showActive][9]
    -   [showCompleted][10]
    -   [addItem][11]
        -   [Parameters][12]
    -   [removeItem][13]
        -   [Parameters][14]
    -   [removeCompletedItems][15]
    -   [toggleComplete][16]
        -   [Parameters][17]
    -   [toggleAll][18]
        -   [Parameters][19]
    -   [\_updateCount][20]
    -   [\_filter][21]
        -   [Parameters][22]
    -   [\_updateFilterState][23]
        -   [Parameters][24]
-   [Model][25]
    -   [Parameters][26]
    -   [create][27]
        -   [Parameters][28]
    -   [read][29]
        -   [Parameters][30]
        -   [Examples][31]
    -   [update][32]
        -   [Parameters][33]
    -   [remove][34]
        -   [Parameters][35]
    -   [removeAll][36]
        -   [Parameters][37]
    -   [getCount][38]
        -   [Parameters][39]
-   [Store][40]
    -   [Parameters][41]
    -   [find][42]
        -   [Parameters][43]
        -   [Examples][44]
    -   [findAll][45]
        -   [Parameters][46]
    -   [save][47]
        -   [Parameters][48]
    -   [remove][49]
        -   [Parameters][50]
    -   [drop][51]
        -   [Parameters][52]
-   [escapeHtmlChar][53]
    -   [Parameters][54]
-   [Template][55]
    -   [defaultTemplate][56]
        -   [Parameters][57]
    -   [show][58]
        -   [Parameters][59]
        -   [Examples][60]
    -   [itemCounter][61]
        -   [Parameters][62]
    -   [clearCompletedButton][63]
        -   [Parameters][64]
-   [window][65]
    -   [app][66]
-   [View][67]
    -   [Parameters][68]
    -   [template][69]
        -   [Parameters][70]
    -   [\_removeItem][71]
        -   [Parameters][72]
    -   [\_clearCompletedButton][73]
        -   [Parameters][74]
    -   [\_setFilter][75]
        -   [Parameters][76]
    -   [\_elementComplete][77]
        -   [Parameters][78]
    -   [\_editItem][79]
        -   [Parameters][80]
    -   [\_editItemDone][81]
        -   [Parameters][82]
    -   [render][83]
        -   [Parameters][84]
    -   [bind][85]
        -   [Parameters][86]
-   [checked][87]
-   [self][88]
-   [blur][89]

## Todo

Sets up a brand new Todo list.

### Parameters

-   `name` **[string][90]** The name of your new to do list.

### storage

## Controller

Takes a model and view and acts as the controller between them

### Parameters

-   `model` **[Object][91]** The model instance
-   `view` **[Object][91]** The view instance

### setView

Loads and initialises the view

#### Parameters

-   `locationHash` **[string][90]** '' | 'active' | 'completed'

### showAll

An event to fire on load. Will get all items and display them in the
todo-list

### showActive

Renders all active tasks

### showCompleted

Renders all completed tasks

### addItem

An event to fire whenever you want to add an item. Simply pass in the event
object and it'll handle the DOM insertion and saving of the new item.

#### Parameters

-   `title`

### removeItem

By giving it an ID it'll find the DOM element matching that ID,
remove it from the DOM and also remove it from storage.

#### Parameters

-   `id` **[number][92]** The ID of the item to remove from the DOM and
    storage

### removeCompletedItems

Will remove all completed items from the DOM and storage.

### toggleComplete

Give it an ID of a model and a checkbox and it will update the item
in storage based on the checkbox's state.

#### Parameters

-   `id` **[number][92]** The ID of the element to complete or uncomplete
-   `completed` **[Object][91]** => reference to the checkbox. The checkbox to check the state of complete
                             or not
-   `silent` **([boolean][93] \| [undefined][94])** Prevent re-filtering the todo items

### toggleAll

Will toggle ALL checkboxes' on/off state and completeness of models.
Just pass in the event object.

#### Parameters

-   `completed`

### \_updateCount

Updates the pieces of the page which change depending on the remaining
number of todos.

### \_filter

Re-filters the todo items, based on the active route.

#### Parameters

-   `force` **([boolean][93] \| [undefined][94])** forces a re-painting of todo items.

### \_updateFilterState

Simply updates the filter nav's selected states

#### Parameters

-   `currentPage`

## Model

Creates a new Model instance and hooks up the storage.

### Parameters

-   `storage` **[Object][91]** A reference to the client side storage class

### create

Creates a new todo model

#### Parameters

-   `title` **[string][90]?** The title of the task
-   `callback` **[function][95]?** The callback to fire after the model is created

### read

Finds and returns a model in storage. If no query is given it'll simply
return everything. If you pass in a string or number it'll look that up as
the ID of the model to find. Lastly, you can pass it an object to match
against.

#### Parameters

-   `query` **([string][90] \| [number][92] \| [object][91])?** A query to match models against
-   `callback` **[function][95]?** The callback to fire after the model is found

#### Examples

```javascript
model.read(1, func); // Will find the model with an ID of 1
model.read('1'); // Same as above
//Below will find a model with foo equalling bar and hello equalling world.
model.read({ foo: 'bar', hello: 'world' });
```

### update

Updates a model by giving it an ID, data to update, and a callback to fire when
the update is complete.

#### Parameters

-   `id` **[number][92]** The id of the model to update
-   `data` **[Object][91]** The properties to update and their new value
-   `callback` **[function][95]** The callback to fire when the update is complete.

### remove

Removes a model from storage

#### Parameters

-   `id` **[number][92]** The ID of the model to remove
-   `callback` **[function][95]** The callback to fire when the removal is complete.

### removeAll

WARNING: Will remove ALL data from storage.

#### Parameters

-   `callback` **[function][95]** The callback to fire when the storage is wiped.

### getCount

Returns a count of all todos

#### Parameters

-   `callback`

## Store

Creates a new client side storage object and will create an empty
collection if no collection already exists.

### Parameters

-   `name` **[string][90]** The name of our DB we want to use
-   `callback` **[function][95]** Our fake DB uses callbacks because in
    real life you probably would be making AJAX calls

### find

Finds items based on a query given as a JS object

#### Parameters

-   `query` **[Object][91]** The query to match against (i.e. {foo: 'bar'})
-   `callback` **[function][95]** The callback to fire when the query has
    completed running

#### Examples

```javascript
db.find({foo: 'bar', hello: 'world'}, function (data) {
 // data will return any items that have foo: bar and
 // hello: world in their properties
});
```

### findAll

Will retrieve all data from the collection

#### Parameters

-   `callback` **[function][95]** The callback to fire upon retrieving data

### save

Will save the given data to the DB. If no item exists it will create a new
item, otherwise it'll simply update an existing item's properties

#### Parameters

-   `updateData` **[Object][91]** The data to save back into the DB
-   `callback` **[function][95]** The callback to fire after saving
-   `id` **[number][92]** An optional param to enter an ID of an item to update

### remove

Will remove an item from the Store based on its ID

#### Parameters

-   `id` **[number][92]** The ID of the item you want to remove
-   `callback` **[function][95]** The callback to fire after saving

### drop

Will drop all storage and start fresh

#### Parameters

-   `callback` **[function][95]** The callback to fire after dropping the data

## escapeHtmlChar

### Parameters

-   `chr` **[Array][96]** get the escape Html character

## Template

Sets up defaults for all the Template methods such as a default template

### defaultTemplate

#### Parameters

-   `defaultTemplate` **[string][90]** push a default template of a TODO on the DOM

### show

Creates an <li> HTML string and returns it for placement in your app.

NOTE: In real life you should be using a templating engine such as Mustache
or Handlebars, however, this is a vanilla JS example.

#### Parameters

-   `data` **[Object][91]** The object containing keys you want to find in the
                         template to replace.

#### Examples

```javascript
view.show({
id: 1,
title: "Hello World",
completed: 0,
});
```

Returns **[string][90]** HTML String of an <li> element

### itemCounter

Displays a counter of how many to dos are left to complete

#### Parameters

-   `activeTodos` **[number][92]** The number of active todos.

Returns **[string][90]** String containing the count

### clearCompletedButton

Updates the text within the "Clear completed" button

#### Parameters

-   `completedTodos` **\[type]** The number of completed todos.

Returns **[string][90]** String containing the count

## window

global qs, qsa, $on, $parent, $delegate

### app

Export to window

## View

**Extends Template**

View that abstracts away the browser's DOM completely.
It has two simple entry points:

-   bind(eventName, handler)
    Takes a todo application event and registers the handler
-   render(command, parameterObject)
    Renders the given command with the options

### Parameters

-   `template` **[Object][91]** herited of Template.defaultTemplate
     => "       <li data-id="{{id}}" class="{{completed}}">             <div class="view">
                                <input class="toggle" type="checkbox" {{checked}}>
                                <label>{{title}}</label>
                                <button class="destroy"></button>
                        </div>
                </li>"

### template

#### Parameters

-   `ENTER_KEY` **[number][92]** keyboard for validate new TODO
-   `ESCAPE_KEY` **[number][92]** keyboard for escape
-   `$todoList` **[Array][96]** select all the items with the "todo-list" class
-   `$todoList` **[Array][96]** select all the items with the "todo-list" class
-   `$todoList` **[Array][96]** select all the items with the "todo-list" class
-   `$todoItemCounter` **[Array][96]** select all the items with the "todo-count" class
-   `$clearCompleted` **[Array][96]** select all the items with the "clear-completed" class
-   `$main` **[Array][96]** select all the items with the "main" class
-   `$footer` **[Array][96]** select all the items with the "footer" class
-   `$toggleAll` **[Array][96]** select all the items with the "toggle-all" class
-   `$newTodo` **[Array][96]** select all the items with the "new-todo" class

### \_removeItem

select a TODO with his id and remove it from the DOM

#### Parameters

-   `id` **[string][90]** id off the element targeted withe this remove event

### \_clearCompletedButton

#### Parameters

-   `completedCount` **[number][92]** number of items how are completed
-   `visible` **[boolean][93]** apply display style "visible" or "block"

### \_setFilter

#### Parameters

-   `currentPage` **[string][90]** 'all' | 'active' | 'completed'

### \_elementComplete

#### Parameters

-   `id` **[string][90]** the id of TODO item targeted
-   `completed` **[boolean][93]**

### \_editItem

Can change a value of a todo in the list

#### Parameters

-   `id` **[string][90]**
-   `title` **[string][90]** text in the TODO

### \_editItemDone

Validate the itm modify with View.prototype.\_editItem

#### Parameters

-   `id` **[string][90]**
-   `title` **[string][90]** text in the TODO

### render

centralise all the method of the View class

#### Parameters

-   `viewCmd` **[Function][95]** parameter for apply the select method
-   `parameter`

### bind

manage the context (bind() methode)

#### Parameters

-   `event`
-   `handler`

## checked

In case it was toggled from an event and not by clicking the checkbox

## self

## blur

Remove the cursor from the input when you hit enter just like if it
were a real form

[1]: #todo

[2]: #parameters

[3]: #storage

[4]: #controller

[5]: #parameters-1

[6]: #setview

[7]: #parameters-2

[8]: #showall

[9]: #showactive

[10]: #showcompleted

[11]: #additem

[12]: #parameters-3

[13]: #removeitem

[14]: #parameters-4

[15]: #removecompleteditems

[16]: #togglecomplete

[17]: #parameters-5

[18]: #toggleall

[19]: #parameters-6

[20]: #_updatecount

[21]: #_filter

[22]: #parameters-7

[23]: #_updatefilterstate

[24]: #parameters-8

[25]: #model

[26]: #parameters-9

[27]: #create

[28]: #parameters-10

[29]: #read

[30]: #parameters-11

[31]: #examples

[32]: #update

[33]: #parameters-12

[34]: #remove

[35]: #parameters-13

[36]: #removeall

[37]: #parameters-14

[38]: #getcount

[39]: #parameters-15

[40]: #store

[41]: #parameters-16

[42]: #find

[43]: #parameters-17

[44]: #examples-1

[45]: #findall

[46]: #parameters-18

[47]: #save

[48]: #parameters-19

[49]: #remove-1

[50]: #parameters-20

[51]: #drop

[52]: #parameters-21

[53]: #escapehtmlchar

[54]: #parameters-22

[55]: #template

[56]: #defaulttemplate

[57]: #parameters-23

[58]: #show

[59]: #parameters-24

[60]: #examples-2

[61]: #itemcounter

[62]: #parameters-25

[63]: #clearcompletedbutton

[64]: #parameters-26

[65]: #window

[66]: #app

[67]: #view

[68]: #parameters-27

[69]: #template-1

[70]: #parameters-28

[71]: #_removeitem

[72]: #parameters-29

[73]: #_clearcompletedbutton

[74]: #parameters-30

[75]: #_setfilter

[76]: #parameters-31

[77]: #_elementcomplete

[78]: #parameters-32

[79]: #_edititem

[80]: #parameters-33

[81]: #_edititemdone

[82]: #parameters-34

[83]: #render

[84]: #parameters-35

[85]: #bind

[86]: #parameters-36

[87]: #checked

[88]: #self

[89]: #blur

[90]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[91]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[92]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number

[93]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[94]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/undefined

[95]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function

[96]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array