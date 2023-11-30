# [jsTreeTable](https://culmat.github.io/jsTreeTable/)

jsTreeTable is a clone of [jQuery treetable](https://ludo.cubicphuse.nl/jquery-treetable/).
I wrote it, because integrating the original with Atlassian products was too complicated. 
This version is very light weight and provides some helper functions for dynamic tables.

## Features

* unobtrusive
* light weigth
* self contained: no external images, css ...
* helper functions for dynamic tables
* [jQuery treetable](https://ludo.cubicphuse.nl/jquery-treetable/) compatible

## Requirements
Some version of [jQuery](https://jquery.com/), i.e.

```html
<script src="https://code.jquery.com/jquery-2.2.4.min.js" integrity="sha256-BbhdlvQf/xTY9gja0Dq3HiwQF8LaCRTXxZKRutelT44=" crossorigin="anonymous"></script>
```

If you want to use the [slider](#slider) function, some version of [jQuery UI](https://jqueryui.com/), i.e.

```html
<link rel="stylesheet" href="https://code.jquery.com/ui/1.13.2/themes/smoothness/jquery-ui.css" />
<script src="https://code.jquery.com/ui/1.13.2/jquery-ui.min.js" integrity="sha256-lSjKY0/srUM9BE3dPm+c4fBo1dky2v27Gdjm2uoZaL0=" crossorigin="anonymous"></script>
```

jsTreeTable HEAD 
```html
<script src="https://culmat.github.io/jsTreeTable/treeTable.js"></script>
```
or [any release](https://github.com/culmat/jsTreeTable/tree/gh-pages/release).

```html
<script src="https://culmat.github.io/jsTreeTable/release/1.0/treeTable.js"></script>
```

jsTreeTable registers itself under the variable *com_github_culmat_jsTreeTable*.
You will want to declare a short hand alias or, if no conflicts exist register all methods in the scope of your choice:

```javascript
// define a short hand
var jsTT = com_github_culmat_jsTreeTable
alert(jsTT.jsTreeTable)

// register on the window object
com_github_culmat_jsTreeTable.register(this)
alert(jsTreeTable)

```


## Providing data
Either provide pre rendered tables ([see treeTable Example](doc/treeTable.html))...
```html
<table>
  <tr data-tt-id="1">
    <td>Parent</td>
  </tr>
  <tr data-tt-id="2" data-tt-parent-id="1">
    <td>Child</td>
  </tr>
</table>
```
... or dynamically create the table from any data structure, e.g. JSON obtained by an AJAX call. 
See [makeTree](#maketree) API.

## API

### depthFirst

Traverses a tree depth first, applying a given function to each node.

```javascript
function depthFirst(tree, func, childrenAttr)
```

paramter | description | required | default 
--- | --- | --- | ---
tree | the tree data as array of roots | X | 
func | the function to apply recursivly | X | 
childrenAttr | the attribute used to recursivly dig into the tree|  | 'children' 
**Returns** the input parameter tree.

[Example](https://culmat.github.io/jsTreeTable/doc/depthFirst.html)

###   makeTree

Transform a flat data structure into a hierarchical tree structure using id and parent attributes.

```javascript
function makeTree (data, idAttr, refAttr, childrenAttr)
```

paramter | description | required | default 
--- | --- | --- | ---
data | the flat data as array | X | 
idAttr | the attribute used to identify a node |  | 'id' 
refAttr |  the attribute used by the children to reference their parent |  | 'parent' 
childrenAttr | the attribute used to build the hierarchical tree structure|  | 'children' 
**Returns** an array of tree roots.

[Example](https://culmat.github.io/jsTreeTable/doc/makeTree.html)

###   renderTree 

Renders a tree data structure into a DOM table with CSS class *jsTT*, setting the following attributes

* data-tt-id
* data-tt-level
* data-tt-isnode / data-tt-isleaf
* data-tt-parent-id

```javascript
function renderTree(tree, childrenAttr, idAttr, attrs, renderer, tableAttributes)
```

paramter | description | required | default 
--- | --- | --- | ---
tree | the tree data | X | 
childrenAttr | the attribute used to navigate the hierarchical tree structure|  | 'children' 
idAttr | the attribute used to identify a node |  | 'id' 
attrs |  a map of attribute names and labels to be rendered | all attributes except the childrenAttr, label = name | 
renderer |  a rendreing function for custom rendering  |  | 
tableAttributes |  additional table attributes (ie id or class). Can be useful for styling. The css class *jsTT* will always be added.  |  | 

**Returns** an html table as javascript object.

[Example](https://culmat.github.io/jsTreeTable/doc/renderTree.html)

###   attr2attr

A simple helper funtion that copies attributes from javascript objects onto the DOM.
```javascript
function attr2attr(nodes, attrs)
```

paramter | description | required | default 
--- | --- | --- | ---
nodes | an array of nodes to process | X | 
attrs | an array of attribute names | X | 
**Returns** the input parameter nodes

###   treeTable 

Adds functions to expand / collapse a tree table.
Styling needs to be done externally.

```javascript
function treeTable(table)
```

paramter | description | required | default 
--- | --- | --- | ---
table | the table dom node with data-tt-* attributes | X | 

**Returns** the input parameter nodes

[Example](https://culmat.github.io/jsTreeTable/doc/treeTable.html)

###   appendTreetable 

```javascript
function 	(tree, options)
```

paramter | description | required | default 
--- | --- | --- | ---
tree | the tree data | X | 
options | see below |  | 

option | description | required | default 
--- | --- | --- | ---
idAttr | the attribute used to identify a node |  | 'id' 
childrenAttr | the attribute used to navigate the hierarchical tree structure|  | 'children' 
controls | controls you want to add to the top of the table  | | 
mountPoint | where to append the table into the DOM |  | $('body')
depthFirst | funtion to be applied prior to rendering see [depthFirst](#depthfirst)|  | 
renderer | see [renderTree](#rendertree) |  | 
renderedAttr |see [renderTree](#rendertree) | |
tableAttributes | see [renderTree](#rendertree) |  | 
replaceContent | wether to empty the mount point before appending, useful for activity indicators | | false 
initialExpandLevel | 1 .. infinity | |  
slider | wether to display an expand slider control | | false


**Returns** an html table as javascript object obtained by calling [renderTree](#rendertree)

[Example](https://culmat.github.io/jsTreeTable/doc/appendTreetable.html)

###   jsTreeTable 

A property holding the version of jsTreeTable

```javascript
alert(com_github_culmat_jsTreeTable.jsTreeTable)
```

[Example](https://culmat.github.io/jsTreeTable/doc/version.html)

## Source

[Github project](https://github.com/culmat/jsTreeTable/)

## Alternatives

[SlickGrid](https://wiki.github.com/mleibman/SlickGrid)

[jQuery treetable](https://ludo.cubicphuse.nl/jquery-treetable/)


