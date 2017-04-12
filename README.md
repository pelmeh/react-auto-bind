# react-auto-bind
Auto binding events in React.js

### Problem
Events need binding (it's routine when you will make many events)

```
class Timer extends React.Component {
  constructor (props) {
    super (props)
    this.onClick = this.onClick.bind(this)
    this.onFocus = this.onFocus.bind(this)
    this.onBlur = this.onBlur.bind(this)
    this.onKeyDown = this.onKeyDown.bind(this)
    ...
    this.eventNumber9999 = this.eventNumber9999.bind(this)
  }

  onClick () {
    // for working with state or props we need context
    ...
  }
  
  onFocus () {
    ...
  }
  
  onBlur () {
    ...
  }
  
  onKeyDown () {
    ...
  }
  
  // etc

  render() {
    // ugly connections
    return (
      <div onClick={this.onClick} onFocus={this.onFocus} onBlur={this.onBlur} onKeyDown={this.onKeyDown}>...</div>
    );
  }
}
```

### Resolve
Use this plugin. It's analysis you methods, find `key-methods` (React-action names ex.: `onClick`, `onBlur`, etc), make `autobilding` and proceed events to them.

```
// import actions.js

class Timer extends React.Component {
  constructor (props) {
    super (props)
    this.actions = actions.call(this)
    // done! No many bindings
  }

  onClick () {
    // Yes, we have a context here, automatically!
    ...
  }
  
  onFocus () {
    // And here too
    ...
  }
  
  onBlur () {
    ...
  }

  render() {
    // No many event listeners connetions, just one
    return (
      <div {...this.actions}>...</div>
    );
  }
}
```

Plugin `bind only used events`, no useless!


### Features

#### `Multiply using`

```
class Timer extends React.Component {
  constructor (props) {
    super (props)
    this.actionsForDiv = actions.call(this)
    this.actionsForInput = actions.call(this, '_')
    // _ it's prefix (for support multiply using)
  }
  
  onClick () {
    // div event
    ...
  }
  
  _onClick () {
    // input event
    ...
  }
  
  ...
```

#### `Support all react events`
(Clipboard, Composition, Keyboard, Focus, Form, Mouse, Selection, Touch, Wheel, Media, Image, Animation, Transition):
>'onClick', 'onContextMenu', 'onDoubleClick', 'onDrag', 'onDragEnd', 'onDragEnter', 'onDragExit', 'onDragLeave', 'onDragOver', 'onDragStart', 'onDrop', 'onMouseDown', 'onMouseEnter', 'onMouseLeave', 'onMouseMove', 'onMouseOut', 'onMouseOver', 'onMouseUp', 'onCopy', 'onCut', 'onPaste', 'onCompositionEnd', 'onCompositionStart', 'onCompositionUpdate', 'onKeyDown', 'onKeyPress', 'onKeyUp', 'onFocus', 'onBlur', 'onChange', 'onInput', 'onSubmit', 'onSelect', 'onTouchCancel', 'onTouchEnd', 'onTouchMove', 'onTouchStart', 'onScroll', 'onLoad', 'onError', 'onAnimationStart', 'onAnimationEnd', 'onAnimationIteration', 'onTransitionEnd', 'onAbort', 'onCanPlay', 'onCanPlayThrough', 'onDurationChange', 'onEmptied', 'onEncrypted', 'onEnded', 'onError', 'onLoadedData', 'onLoadedMetadata', 'onLoadStart', 'onPause', 'onPlay', 'onPlaying', 'onProgress', 'onRateChange', 'onSeeked', 'onSeeking', 'onStalled', 'onSuspend', 'onTimeUpdate', 'onVolumeChange', 'onWaiting'
