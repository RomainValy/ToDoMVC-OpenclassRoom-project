### Table of Contents

-   [Todo][1]
    -   [Parameters][2]
-   [Controller][3]
    -   [Parameters][4]
    -   [setView][5]
        -   [Parameters][6]
    -   [showAll][7]
    -   [showActive][8]
    -   [showCompleted][9]
    -   [addItem][10]
        -   [Parameters][11]
    -   [removeItem][12]
        -   [Parameters][13]
    -   [removeCompletedItems][14]
    -   [toggleComplete][15]
        -   [Parameters][16]
    -   [toggleAll][17]
        -   [Parameters][18]
    -   [\_updateCount][19]
    -   [\_filter][20]
        -   [Parameters][21]
    -   [\_updateFilterState][22]
        -   [Parameters][23]
-   [Model][24]
    -   [Parameters][25]
    -   [create][26]
        -   [Parameters][27]
    -   [read][28]
        -   [Parameters][29]
        -   [Examples][30]
    -   [update][31]
        -   [Parameters][32]
    -   [remove][33]
        -   [Parameters][34]
    -   [removeAll][35]
        -   [Parameters][36]
    -   [getCount][37]
        -   [Parameters][38]
-   [Store][39]
    -   [Parameters][40]
    -   [find][41]
        -   [Parameters][42]
        -   [Examples][43]
    -   [findAll][44]
        -   [Parameters][45]
    -   [save][46]
        -   [Parameters][47]
    -   [remove][48]
        -   [Parameters][49]
    -   [drop][50]
        -   [Parameters][51]
-   [Template][52]
    -   [show][53]
        -   [Parameters][54]
        -   [Examples][55]
    -   [itemCounter][56]
        -   [Parameters][57]
    -   [clearCompletedButton][58]
        -   [Parameters][59]
-   [View][60]
    -   [Parameters][61]

## Todo

Sets up a brand new Todo list.

### Parameters

-   `name` **[string][62]** The name of your new to do list.

## Controller

Takes a model and view and acts as the controller between them

### Parameters

-   `model` **[Object][63]** The model instance
-   `view` **[Object][63]** The view instance

### setView

Loads and initialises the view

#### Parameters

-   `locationHash` **[string][62]** '' | 'active' | 'completed'

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

-   `id` **[number][64]** The ID of the item to remove from the DOM and
    storage

### removeCompletedItems

Will remove all completed items from the DOM and storage.

### toggleComplete

Give it an ID of a model and a checkbox and it will update the item
in storage based on the checkbox's state.

#### Parameters

-   `id` **[number][64]** The ID of the element to complete or uncomplete
-   `completed` **[Object][63]** => reference to the checkbox. The checkbox to check the state of complete
                             or not
-   `silent` **([boolean][65] \| [undefined][66])** Prevent re-filtering the todo items

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

-   `force` **([boolean][65] \| [undefined][66])** forces a re-painting of todo items.

### \_updateFilterState

Simply updates the filter nav's selected states

#### Parameters

-   `currentPage`

## Model

Creates a new Model instance and hooks up the storage.

### Parameters

-   `storage` **[Object][63]** A reference to the client side storage class

### create

Creates a new todo model

#### Parameters

-   `title` **[string][62]?** The title of the task
-   `callback` **[function][67]?** The callback to fire after the model is created

### read

Finds and returns a model in storage. If no query is given it'll simply
return everything. If you pass in a string or number it'll look that up as
the ID of the model to find. Lastly, you can pass it an object to match
against.

#### Parameters

-   `query` **([string][62] \| [number][64] \| [object][63])?** A query to match models against
-   `callback` **[function][67]?** The callback to fire after the model is found

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

-   `id` **[number][64]** The id of the model to update
-   `data` **[Object][63]** The properties to update and their new value
-   `callback` **[function][67]** The callback to fire when the update is complete.

### remove

Removes a model from storage

#### Parameters

-   `id` **[number][64]** The ID of the model to remove
-   `callback` **[function][67]** The callback to fire when the removal is complete.

### removeAll

WARNING: Will remove ALL data from storage.

#### Parameters

-   `callback` **[function][67]** The callback to fire when the storage is wiped.

### getCount

Returns a count of all todos

#### Parameters

-   `callback`

## Store

Creates a new client side storage object and will create an empty
collection if no collection already exists.

### Parameters

-   `name` **[string][62]** The name of our DB we want to use
-   `callback` **[function][67]** Our fake DB uses callbacks because in
    real life you probably would be making AJAX calls

### find

Finds items based on a query given as a JS object

#### Parameters

-   `query` **[Object][63]** The query to match against (i.e. {foo: 'bar'})
-   `callback` **[function][67]** The callback to fire when the query has
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

-   `callback` **[function][67]** The callback to fire upon retrieving data

### save

Will save the given data to the DB. If no item exists it will create a new
item, otherwise it'll simply update an existing item's properties

#### Parameters

-   `updateData` **[Object][63]** The data to save back into the DB
-   `callback` **[function][67]** The callback to fire after saving
-   `id` **[number][64]** An optional param to enter an ID of an item to update

### remove

Will remove an item from the Store based on its ID

#### Parameters

-   `id` **[number][64]** The ID of the item you want to remove
-   `callback` **[function][67]** The callback to fire after saving

### drop

Will drop all storage and start fresh

#### Parameters

-   `callback` **[function][67]** The callback to fire after dropping the data

## Template

Sets up defaults for all the Template methods such as a default template

### show

Creates an <li> HTML string and returns it for placement in your app.

NOTE: In real life you should be using a templating engine such as Mustache
or Handlebars, however, this is a vanilla JS example.

#### Parameters

-   `data` **[Object][63]** The object containing keys you want to find in the
                         template to replace.

#### Examples

```javascript
view.show({
id: 1,
title: "Hello World",
completed: 0,
});
```

Returns **[string][62]** HTML String of an <li> element

### itemCounter

Displays a counter of how many to dos are left to complete

#### Parameters

-   `activeTodos` **[number][64]** The number of active todos.

Returns **[string][62]** String containing the count

### clearCompletedButton

Updates the text within the "Clear completed" button

#### Parameters

-   `completedTodos` **\[type]** The number of completed todos.

Returns **[string][62]** String containing the count

## View

View that abstracts away the browser's DOM completely.
It has two simple entry points:

-   bind(eventName, handler)
    Takes a todo application event and registers the handler
-   render(command, parameterObject)
    Renders the given command with the options

### Parameters

-   `template`

[1]: #todo

[2]: #parameters

[3]: #controller

[4]: #parameters-1

[5]: #setview

[6]: #parameters-2

[7]: #showall

[8]: #showactive

[9]: #showcompleted

[10]: #additem

[11]: #parameters-3

[12]: #removeitem

[13]: #parameters-4

[14]: #removecompleteditems

[15]: #togglecomplete

[16]: #parameters-5

[17]: #toggleall

[18]: #parameters-6

[19]: #_updatecount

[20]: #_filter

[21]: #parameters-7

[22]: #_updatefilterstate

[23]: #parameters-8

[24]: #model

[25]: #parameters-9

[26]: #create

[27]: #parameters-10

[28]: #read

[29]: #parameters-11

[30]: #examples

[31]: #update

[32]: #parameters-12

[33]: #remove

[34]: #parameters-13

[35]: #removeall

[36]: #parameters-14

[37]: #getcount

[38]: #parameters-15

[39]: #store

[40]: #parameters-16

[41]: #find

[42]: #parameters-17

[43]: #examples-1

[44]: #findall

[45]: #parameters-18

[46]: #save

[47]: #parameters-19

[48]: #remove-1

[49]: #parameters-20

[50]: #drop

[51]: #parameters-21

[52]: #template

[53]: #show

[54]: #parameters-22

[55]: #examples-2

[56]: #itemcounter

[57]: #parameters-23

[58]: #clearcompletedbutton

[59]: #parameters-24

[60]: #view

[61]: #parameters-25

[62]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[63]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[64]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number

[65]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[66]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/undefined

[67]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function