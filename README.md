# React-simple-dnd

This Library is simply a bunch of wrappers around another library: [React DnD (by Dan Abramov)](http://gaearon.github.io/react-dnd/).

React DnD is a library that implements Drag'nDrop in a “React way”: It doesn't touch the DOM, embraces unidirectional data flow and, most importantly, defines dragging logic as pure data.

React DnD is powerful and flexible enough to support virtually any scenarios involving Drag'nDrop, but this comes at a cost: React DnD requires a lot of boilerplate even for the most simple use cases.

React-simple-dnd is less flexible, but let you create Drag and Drop interfaces with fewer boilerplate and reduced complexity.

## Installing

```bash
$ npm install react-simple-dnd
```

## How to Use

There are two elements available: `<DragSource>` and `<DropTarget>`.

Additionaly, there's the `HTML5DragDrop` Higher Order Component that must be wrap the root component of your application and set up the Drag and Drop support.

See the [examples](https://github.com/cassiozen/react-simple-dnd/tree/master/examples) for complete usage cases.

### `<DragSource>`

#### Usage

##### Simple

```js
<DragSource onBeginDrag={this.handleBeginDrag} onEndDrag={this.handleEndDrag}>
  <div>
    Drag Me
  </div>
</DragSource>
```

##### Function as Children

You can have access to isDragging through function-as-children

```js
<DragSource onBeginDrag={this.handleBeginDrag} onEndDrag={this.handleEndDrag}>
  {(isDragging) => (
    <div className={isDragging && 'drag'}>
      Drag Me
    </div>
  )}
</DragSource>
```


#### Props

type: Optional. String. Only the drop targets registered for the same type will react to drag source. If not provided, a default value will be assigned.

onBeginDrag: Optional. Function. Called when the dragging starts.

onEndDrag:   Optional. Function. Called when the dragging stops.

**Important** React-DnD defines dragging logic as pure data. All other props passed to drag source will be made available to the DropTarget when dropped.


### `<DropTarget>`

#### Usage

##### Simple

```js
<DropTarget onDrop={this.handleDrop}>
  <div>
    Drop on me.
  </div>
</DropTarget>
```

##### Function as Children

You can have access to isOver (true if user is dragging a DragSource over this target) through function-as-children

```js
<DropTarget onDrop={this.handleDrop}>
  {(isOver) => (
    <div className={isOver && 'drag'}>
      Drag Me
    </div>
  )}
</DropTarget>
```


#### Props

types: Optional. String or Array of Strings. This drop target will only react to the drag sources of the specified type or types.

onDrop: Optional. Function. Called when the user Drops a Drag source on this target. The "type" and any custom props included on <DragSource> will be passed as args when invoking this function.

canDrop: Optional. Function. Called when the user tries to drop a Drag source on this target. Should return true or false whether the <DragSource> can be dropped in this target. The "type" and any custom props included on <DragSource> will be passed as args when invoking this function.


### HTML5DragDrop

Wrap the root component of your application with DragDropContext to set up React DnD.
This sets up the shared DnD state behind the scenes.

#### Usage

```js
import { HTML5DragDrop } from 'react-simple-dnd';

class YourApp {
  /* ... */
}

export default HTML5DragDrop(YourApp);
```
