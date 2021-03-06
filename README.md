# WIP - IndexedDB Examples

*Examples of how to use IndexedDB*

### Support

<p align="center"><img width="500px" height="300px" src="https://raw.githubusercontent.com/gokulkrishh/IndexedDB/master/indexeddb.png"></p>

[Full specs](https://www.w3.org/TR/IndexedDB/)

### API


#### Open Database Connection

```js
var dbRequest = indexedDB.open("myDatabase", 1);
```

To open an database, just use ```open``` method with database name. Second argument is version of database.

##### Tips

```js
var dbRequest = indexedDB.open("myDatabase", 1.5);
```

In above example, 1.5 version will be rounded to 1. So use whole number instead of decimal for DB version.

#### Events

```js
dbRequest.onerror = function(event) {
  //On error event
};
```

```js
dbRequest.onsuccess = function(event) {
  //On success event
};
```

```js
//This event is triggered when creating a schema
dbRequest.onupgradeneeded = function(event) {

};
```

#### Create a store

```js
var db;
var store;
var index;
dbRequest.onupgradeneeded = function(event) {
  db = event.target.result;
  //To create Store, find screenshot below for this
  store = db.createObjectStore("MyStore", {keyPath: "id"});

  index = store.createIndex("Index", ["name"]);
};
```

*After creating store*
<p align="center"><img src="https://raw.githubusercontent.com/gokulkrishh/IndexedDB/master/Object-Store.png" style="max-width: 100%"/></p>

*After creating Index - Name*
<p align="center"><img src="https://raw.githubusercontent.com/gokulkrishh/IndexedDB/master/Name-Index.png" style="max-width: 100%"/></p>

#### To handle generic error for particular DB

```js
//Handle error for above DB only
db.onerror = function(event) {
  console.log("Error Code: ", event.target.errorCode);
}
```

#### Transaction

```js
var dbTransaction = db.transaction("MyStore", "readwrite");
var myStore = tx.objectStore("MyStore");

//To store data
store.put({id: 1, name: "Gokul", age: 25});
store.put({id: 1, name: "Krishh", age: 20});
```

#### Query stored data

```js
var user = store.get(1);
var userName = index.get("Krishh");

user.onsuccess = function() {
  console.log(userName.result.id);  // 1
  console.log(userName.result.name);  // Gokul
};

userName.onsuccess = function() {
  console.log(userName.result.name);  // Krishh
};

//Close the DB, once transaction is done
dbTransaction.oncomplete = function() {
  db.close();
};
```

### More Tutorials
[Very simple IndexeDB example](https://gist.github.com/BigstickCarpet/a0d6389a5d0e3a24814b)

[Learn IndexeDB on Tutorialspoint](https://www.tutorialspoint.com/html5/html5_indexeddb.htm)

[Short video tutorial](https://www.youtube.com/watch?v=W9cg2grW82k)

[Medium article - Offline Storage for Progressive Web Apps](https://medium.com/dev-channel/offline-storage-for-progressive-web-apps-70d52695513c#.jx5zj6ewq)



### Wrapper Libraries

- [localForage](https://localforage.github.io/localForage/)

- [pouchdb](https://pouchdb.com/)

- [dexie](http://dexie.org/)

- [Jquery IndexedDB plugin](https://nparashuram.com/jquery-indexeddb/)

- [Dexie.js](http://dexie.org/)

- [IDBWrapper](https://github.com/jensarps/IDBWrapper)


#### Reference

- [MDN](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB)

- [IndexedDB](https://gist.github.com/BigstickCarpet/a0d6389a5d0e3a24814b)


##### MIT Licensed
