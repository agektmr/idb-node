# idb-node

`idb-node` is a Polymer element that provides Indexed Database functionalities to Polymer.

# Install
`git clone` this repository and install dependencies with `bower install`

# Usage
Load [`webcomponents.js`]()
```html
<script src="bower_components/webcomponentsjs/webcomponents.min.js"></script>
```

Import `idb-node`
```html
<link rel="import" href="bower_components/idb-node/idb-node.html">
```

Use this element with required attributes. Database and object stores will be created upon usage.
```html
<idb-node database-name="sample" version="1" object-store="bookmark" key-path="url"></idb-node>
```

## Attributes
You need `idb-node` element with
- `database-name` (required): Database name
- `version` (required): Version number string
- `object-store` (required): Object Store name
- `key-path` (optional): A key for the object store

## Methods
All methods return a promise
- `put(item)`: Put an object
- `putBulk(arrayOfItems)`: Put an array of objects
- `get(key)`: Get an object with a key of `key`
- `delete(key)`: Delete an object with a key of `key`
- `getAll()`: Get all objects in the store
- `deleteAll()`: Delete all objects in the store

## Events
- `idb-ready`: Fired when the database is ready to use

## Iron Meta
You can access database via [`iron-meta`](https://github.com/PolymerElements/iron-meta). `iron-meta` allows you to open database using monostate pattern. This is useful when you have many different instance of elements that access to a single database.
- Specify `iron-meta[type]` as `idb`.
- Get access to the element.
- You can obtain database instance with `byKey()` method.
- The key is constructed using database name + '-' + object store name.

**Make sure that database is ready before accessing it. You can use `idb-ready` event `idb-node` emits.**

demo.html
```html
<idb-node database-name="demo" version="1" object-store="icons" key-path="name"></idb-node>
<icon-elem icon="star"></icon-elem>
<icon-elem icon="square"></icon-elem>
```

icon-elem.html
```html
<dom-module id="icon-elem">
  <iron-meta id="meta" type="idb"></iron-meta>
</dom-module>
<script>
  Polymer({
    is: 'icon-elem',
    properties: {
      icon: {
        type: String,
        value: ''
      },
      db: {
        type: Object,
        value: {}
      }
    },
    ready: function() {
      this.db = this.$.meta.byKey('demo-icons');
      if (this.db.dbReady) {
        this.readDb();
      } else {
        this.db.addEventListener('idb-ready', readDb.bind(this));
      }
    },
    readDb: function() {
      this.db.get(function() {
        ...
      });
    }
  });
</script>
```
