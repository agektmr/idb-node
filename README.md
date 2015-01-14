# polymer-idb

`polymer-idb` is a Polymer element that provides Indexed Database functionalities to Polymer.

# Install
`git clone` this repository and install dependencies with `bower install`

# Usage
Load [`webcomponents.js`]()
```
<script src="bower_components/webcomponentsjs/webcomponents.min.js"></script>
```

Import `polymer-idb`
```
<link rel="import" href="bower_components/polymer-idb/polymer-idb.html">
```

Use this element with required attributes. Database and object stores will be created upon usage.
```
<polymer-idb database="sample" version="1" object-store="bookmark" key-path="url"></polymer-idb>
```

## Attributes
You need `polymer-idb` element with
- `database` (required): Database name
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
