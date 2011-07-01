# Ext.data.proxy.IndexedDB
      
  IndexedDB proxy implementation for Ext JS 4. A good choice for powering your project examples without need for server-side middleware and database.
  
     ...
		proxy: {
			type: 'idb',
			dbName: 'companies',
			objectStoreName: 'company',
			dbVersion: '1.15',
         	writer: {
	             type: 'json',
	             writeAllFields: false
	         },
			initialData: [
				{
					name: 'IBM',
					employees: 33,
					incorporation: new Date(),
					id: Ext.id()
				},{
					name: 'Hilton',
					employees: 411,
					incorporation: new Date(),
					id: Ext.id()
				}
			]
		},
		...



## License 

(The MIT License)

Copyright (c) 2009-2011 Grgur Grisogono &lt;grguru@gmail.com&gt;

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