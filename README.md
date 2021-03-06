# Ext.data.proxy.IndexedDB

  IndexedDB proxy implementation for Ext JS 4.x.
  IndexedDB is natively available in IE 10+, Firefox 4+, Chrome 10+, Opera 15+ Blackberry 10.0+.
  IndexedDB can also be polyfilled for other browsers via: https://github.com/axemclion/IndexedDBShim

  This project was forked from  https://github.com/grgur/Ext.data.proxy.IndexedDB in order to provide the following:
  1. Better support for multiple object stores
  2. Support for loading data stores limited by index values
  3. Implementation of start and limit on read operations.

To use this proxy, specify the following in your store's configuration.
```javascript
    ...
    proxy: {
        type: 'idb', //Proxy type for Ext.data.proxy.IndexedDB
        dbName: 'companyinfo', //Database name
        objectStoreName: 'employee', //Object store name 
        dbVersion: 1 //Database version
        indexes: [{
            name: 'companyNameIdx', //Name of index
            field: 'name',  //Field to index
            options: {unique: true} //Index values can only be used for one record.
        }]

    }
```

If you have multiple ExtJS stores that you want to save to an IndexedDB, use the 
IndexedDBManager to first initialize the database:
```javascript
    Ext.data.proxy.IndexedDBManager.initializeDB({
        dbName: 'companyinfo',        
        dbVersion: 1,
        objectStores: [{
            name: 'company',
            keyPath: 'id',
            indexes: [{
                name: 'companyNameIdx', 
                field: 'name', 
                options: {unique: true}
            }]
        }, {
            name: 'employee',
            keyPath: 'id',
            indexes: [
                name: 'companyIdIdx', 
                field: 'companyId', 
                options: {unique: false} //Index value can be used by multiple records. 
            }, {
                name: 'visitDateIdx', 
                field: 'visitDate', 
                options: {unique: false}
            }]
        }],    
        listeners: {
            dbopen: init
        }
    });

    function init() {
        // create the Data Store
        var companyStore = Ext.create('Ext.data.Store', {
            initialDataLoaded: false,
            autoSync: true,
            autoLoad: true,
            model: 'Company',
            proxy: {
                type: 'idb',
                dbName: 'companyinfo',
                objectStoreName: 'company',
                dbVersion: Ext.data.proxy.IndexedDBManager.getDBVersion()
            }
        });
        ...
    }
```
You can use the store's load function to interact with indexes:

```javascript
employeeStore.load({
    params: { //Load store via exact index value                                
        index: 'companyIdIdx', 
        indexValue: 123</b>
    }
});

employeeStore.load({
    params: { //Search for names between C - H
        index: 'firstNameIdx', 
        indexLower: 'C', 
        indexUpper: 'H'
    }
});         
```

```javascript
You can also do fuzzy (contains) searches to load:
//Finds names that contain mi in first or last name(For example, Mike, Smith, etc)
employeeStore.load({
    params: {
        containsSearch: 'mi', 
        containsKeys: [
            'firstName',
            'lastName'
        ]
    }
});
```                                     

## License

(The MIT License)

Copyright (c) 2013 John Kleinschmidt

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.