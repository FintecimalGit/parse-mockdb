Parse MockDB
=====================

Master Build Status: [![Circle CI](https://circleci.com/gh/HustleInc/parse-mockdb/tree/master.svg?style=svg)](https://circleci.com/gh/HustleInc/parse-mockdb/tree/master)

Provides a mocked Parse RESTController compatible with version `1.6+` of the JavaScript SDK.

### Installation and Usage

```js
npm install parse-mockdb --save-dev
```

Enhancements: 
  To make specific test-scenarios somethimes is required to define custom createAt, updateAt or objectId, 
  so this fork is able to handle it. just add to the object the data to save:

```js
    created_at = createdAt
    updated_at = updatedAt
    object_id = objectId
```
  Dates can be defined as follow:
```js
    { iso: "2018-03-14T17:46:07.014Z" }
    { timestamp: 1521049641200 } 
    { stringDate: "14/03/2018 11:44:27", format: "DD/MM/YYYY HH:mm:ss"} // format is optional, and the default is: DD/MM/YYYY HH:mm:ss
```
```js

    data = { 
      object_id: 'zzzzz',
      created_at: { timestamp: 1521049641200 },
      field1: "aaa",
      field2: "dddd" 
    };

    const document = (new Parse.Object('collection_name')).set(data);

    document.save().then((object) => {
      console.log(object) // {"field1":"aaa","field2":"dddd","createdAt":"2018-03-14T17:47:21.200Z","updatedAt":"2018-03-14T17:53:15.985Z","objectId":"zzzzz"}  
    });
```

```js
'use strict';
const Parse = require('parse-shim');
const ParseMockDB = require('parse-mockdb');

ParseMockDB.mockDB(); // Mock the Parse RESTController

// Perform saves, queries, updates, deletes, etc... using the Parse JS SDK

ParseMockDB.cleanUp(); // Clear the Database
ParseMockDB.unMockDB(); // Un-mock the Parse RESTController
```

### Completeness

 - [x] Basic CRUD (save, destroy, fetch)
 - [x] Query operators ($exists, $in, $nin, $eq, $ne, $lt, $lte, $gt, $gte, $regex, $select, $inQuery, $all, $nearSphere)
 - [x] Update operators (Increment, Add, AddUnique, Remove, Delete)
 - [x] Parse.Relation (AddRelation, RemoveRelation)
 - [x] Parse query dotted notation matching eg `{ "name.first": "Tyler" })`
 - [ ] Parse class level permissions
 - [ ] Parse.ACL (row level permissions)
 - [ ] Parse special classes (Parse.User, Parse.Role, ...)
 - [ ] Parse lifecycle hooks (beforeSave - done, afterSave - done, beforeDelete - done, afterDelete)

### Tests

```sh
npm test
```
