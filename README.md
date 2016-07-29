node-uwp
==========

Enables Universal Windows Platform (UWP) API access for Node.js (Chakra build)
on Windows 10.

Example
-------

```javascript
const uwp = require('uwp');
const Windows = uwp.projectNamespace('Windows');

Windows.Storage.KnownFolders.documentsLibrary.createFileAsync(
  'sample.dat', Windows.Storage.CreationCollisionOption.replaceExisting)
  .done(
    function (file) {
      console.log('ok');
      uwp.close(); // all async operations are completed, release uwp
    },
    function (error) {
      console.error('error', error);
      uwp.close(); // all async operations are completed, release uwp
    }
);
```

Installation
------------

### Prerequisites

 * Windows 10 [1511 or above](http://windows.microsoft.com/en-us/windows-10/windows-update-faq)
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

---------------------------------------------------------------------------
Checkout our OSS effort with
[Node-ChakraCore](https://github.com/nodejs/node-chakracore). It supports the
most recent version of node.js and will also be useful if you are on Windows 7
or Windows 8.1. Note: <b>It does not support UWP.</b>
