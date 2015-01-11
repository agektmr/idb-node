# polymer-idb

`polymer-idb` is a Polymer element that provides Indexed Database functionalities to Polymer.

# Install

```
$ bower install polymer-idb --save
```

# Usage
```
<polymer-idb database="sample" version="1" object-store="bookmark" key-path="url"></polymer-idb>
```

## Attributes
You need `polymer-idb` element with
- `database`: Database name
- `version`: Version number string
- `object-store`: Object Store name
- `key-path`: A key for the object store

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
