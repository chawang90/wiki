# Tooltips with Tipsy

How we use the [Tipsy](https://github.com/jaz303/tipsy) library for creating tooltips.

## How to create tooltips

Simply add an element with `rel="tipsy"` and give it a `title`:

```html
<div rel="tipsy" title="Vegetarian">V</div>
<div rel="tipsy" title="Vegan">VG</div>
```

## Glue Code

You can see the code that powers this in `app/assets/javascripts/third_party/tipsy.js`

```javascript
Josephine.ThirdParty.Tipsy = {
  init: function() {
    $('[rel=tipsy]').tipsy({
      fade: false,
      gravity: 's',
      opacity: 1
    })
  }
}
```

Tada!
