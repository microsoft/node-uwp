node-uwp
==========

Enables Universal Windows Platform (UWP) API access for Node.js (Chakra build)
on Windows 10.

Example
-------

```javascript
var uwp = require('uwp');
uwp.projectNamespace("Windows");

Windows.Storage.KnownFolders.documentsLibrary.createFileAsync(
  "sample.dat", Windows.Storage.CreationCollisionOption.replaceExisting)
  .done(
    function (file) {
      console.log("ok");
      uwp.close(); // all async operations are completed, release uwp
    },
    function (error) {
      console.error("error", error);
      uwp.close(); // all async operations are completed, release uwp
    }
);
```

Installation
------------

### Prerequisites

 * Windows 10 [November update](http://windows.microsoft.com/en-us/windows-10/windows-update-faq)
 * [Visual Studio](https://www.visualstudio.com/vs-2015-product-editions)
 * [Node.js (Chakra)](http://aka.ms/node-chakra-installer)

Run under Node.js (Chakra) command prompt:

```sh
npm install uwp
```

APIs
----

This package exports 2 functions.

### projectNamespace(name)

Project a UWP namespace of given name.

* **Note**: This function will keep Node process alive so that your app can
  continue to run and handle UWP async callbacks. You need to call
  [close()](#close) when UWP usage is completed.

<a name="close"></a>
### close()

Close all UWP handles used by this package. Call this when all UWP usage is
completed.
