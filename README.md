#Grid Demo

A sample of controls and instructions an (Espresso Grid)[]

### Getting Started
Outputting an extensible grid starts with loading the library, creating an iframe, and initializing the espressoGrid, which can be done with five lines of code:
```	
<script src="https://eval.espressologic.com/grid/espresso-grid.min.js"></script>
<script>var frame = espressoGrid.init({id: 'uniqueID'});</script>
<iframe id="uniqueID" src="https://eval.espressologic.com/grid/?gridID=uniqueID"></iframe>
```
The default grid without an auth config object attribute is a readonly instance of our Espresso Demo API. The configuration object allows for a lot more container control, of course, and includes parameters for manipulating everything from grid styles to grid controls.
```javascript
var grid = espressoGrid.init({a#Grid Demo

A sample of interactions made possible with [Espresso Grid](http://github.com/EspressoLogicCafe/espresso-grid) using an Espresso Logic API. We are using a read-only, public project, to do more with your grid, register @ [Espresso Logic](http://espressologic.com).

### Filtering
Espresso Grids by default have searches enabled, and demonstrated in our example here are several pre-configured searches that make sense when trying to filter purchase orders: paid/unpaid, or by an amount total. After initializing the grid, the container listens for the "GridReady" event.
```javascript
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
	id: 'uniqueID',
	auth: {
		username: 'demo',
		password: 'Password1',
		apiBase: 'https://eval.espressologic.com/rest/livedemo/demo/v1',
		endpoint: 'demo:customer'
	},
	columns: [{field:'name', displayName:'Name'}],
	controls: {
		undo: true,
		search:true,
		fetch: true,
		insert: true,
		save: true,
		del: true
	},
	controlBox: 'bottom',
	parentControls: { undo: true, search:true, fetch: true, insert: true, save: true, del: true },
	//css: { cssFileHandle: '//yourFileHref.css' },
	//js: { jsFileHandle: '//yourFileSrc.js' }
});
```