# misbehave

Turn Polymer v1 components into behaviors

[![Build Status](https://travis-ci.org/devinivy/misbehave.svg?branch=master)](https://travis-ci.org/devinivy/misbehave)

## Usage
Misbehave adds a method `element.toBehavior()` to all Polymer components which exports a behavior definition that can be used to effectively extend a component.  The misbehave library should be included as an HTML import after Polymer.

```html
<link rel="import" href="../polymer/polymer.html">
<link rel="import" href="../misbehave/misbehave.html">
<link rel="import" href="base-component.html">

<script>

  Polymer({

    is: 'ext-component',

    // ext-component now effectively extends the Polymer component base-component
    behaviors: [
      document.createElement('base-component').toBehavior()
    ]

  });

</script>
```
