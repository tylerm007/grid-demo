#Grid Demo

A sample of interactions made possible with [Espresso Grid](http://github.com/EspressoLogicCafe/espresso-grid) using an Espresso Logic API. This is a demo public project, and as a result is read-only, to do more with your grid, register @ [Espresso Logic](http://espressologic.com).

### Filtering
Espresso Grids by default have enabled searches, and demonstrated in our html example are several pre-configured searches that make sense when trying to filter purchase orders: paid/unpaid, or by an amount total. After initializing the grid, the container listens for the "GridReady" event.
```javascript
var state;
grid.on('GridReady', function (event, data) {
	//state.operators is an array of our search operators
	//state.table.named will contain our collection of searchable columns
	state = data;
});
```

The container can then easily broadcast searches:
```javascript
var filterOjbect = {
	column: state.table.named['paid'], //PurchaseOrder.paid column
	operator: state.operators[3], //equals operator object
	text: searchValue
};
grid.broadcast('ControlRunSearch', [filterObject])
```

###Custom Styles
Espresso Grids also listen for styles from the parent, either by passing css hrefs on initialization:
```javascript
var grid = espressoGrid.init({
	css: { fileHandle: 'href' }	
});
```
Or as shown in the html example provided by broadcasts to the "ControlRawCSS" event
```javascript
grid.broadcast('ControlRawCSS', styles);
```

###Column Definitions
Columns can also be defined on initialization, though sometimes it may be preferred to add or remove columns after start up. In this demo, we do the latter by listening for "EventColumnsRefreshed" event, which broadcasts an array of column definitions whenever they have changed. Then in the container, a user can optionally check or uncheck a column, which is broadcast back to Espresso Grid on the fly.
```javascript
var colDefs;
grid.on('EventColumnsRefreshed', function (event, defs) {
	colDefs = defs;
});

//after some user interaction,
//we can arbitrarily remove a column by broadcasting a spliced array
colDefs.splice(1, 1);
grid.broadcast('ControlColumnDefinitions', colDefs);
```