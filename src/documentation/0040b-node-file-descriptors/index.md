---
title: 'Working with file descriptors in Node.js'
description: 'How to interact with file descriptors using Node.js'
authors: flaviocopes, MylesBorins, fhemberger, LaRuaNa, ahmadawais
section: Getting Started
category: learn
---

Before you're able to interact with a file that sits in your filesystem, you must get a file descriptor.

A file descriptor is a reference to an open file, a number (id) returned by opening the file using the `open()` method offered by the `fs` module. This number (`fd`) uniquely identifies an open file in operating system:

```js
const fs = require('fs')

fs.open('/Users/joe/test.txt', 'r', (err, fd) => {
  //fd is our file descriptor
})
```

Notice the `r` we used as the second parameter to the `fs.open()` call.

That flag means we open the file for reading.

Other flags you'll commonly use are

* `r+` open the file for reading and writing, if file don't exist it won't be created.
* `w+` open the file for reading and writing, positioning the stream at the beginning of the file. The file is created if not existing
* `a` open the file for writing, positioning the stream at the end of the file. The file is created if not existing
* `a+` open the file for reading and writing, positioning the stream at the end of the file. The file is created if not existing

You can also open the file by using the `fs.openSync` method, which returns the file descriptor, instead of providing it in a callback:

```js
const fs = require('fs')

try {
  const fd = fs.openSync('/Users/joe/test.txt', 'r')
} catch (err) {
  console.error(err)
}
```

Once you get the file descriptor, in whatever way you choose, you can perform all the operations that require it, like calling `fs.close()` and many other operations that interact with the filesystem.
