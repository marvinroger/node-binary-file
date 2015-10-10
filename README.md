binary-file
===========

[![NPM version](https://img.shields.io/npm/v/binary-file.svg)](https://www.npmjs.com/package/binary-file) ![Node version](https://img.shields.io/node/v/binary-file.svg)

Read and write binary types in files.
This library allows you to use the functions you would use on a Buffer, like readUInt32, directly on files.
It is promises-based.

```
npm install --save binary-file
```

## Use case

Say you want to parse a simple binary file for an an UInt32 containing the length of the string that follows. With binary-file, you can simply:

```javascript
'use strict';

let BinaryFile = require('binary-file');

let myBinaryFile;
new BinaryFile('./file.bin', 'r').then(function (instance) {
  myBinaryFile = instance;
  return myBinaryFile.readUInt32();
}).then(function (stringLength) {
  return myBinaryFile.readString(stringLength);
}).then(function (string) {
  console.log(`File read: ${string}`);
}).catch(function(err) {
  console.log(`There was an error: ${err}`);
});
```

You don't have to create a Buffer to write the data read from the file, you don't have to remember the position of the cursor: everything is handled by BinaryFile.

## API

### File

#### `new BinaryFile(path, mode, littleEndian = false)`

Create a new instance of BinaryFile.

* `path`: the path of the file to open
* `mode`: the mode in which to open the file. See [fs.open](https://nodejs.org/api/fs.html#fs_fs_open_path_flags_mode_callback)
* `littleEndian`: endianness of the file

Return a promise.

**fulfilled** with the class instance once the file is opened

#### `.size()`

Get the size in bytes of the file.

Return a promise.

**fulfilled** with the size of the file in bytes

#### `.tell()`

Get the position of the cursor in the file.

Return the position of the cursor in the file.

#### `.seek(position)`

Set the position of the cursor in the file

* `position`: the position where to place the cursor

Return the new position.

#### `.close()`

Close the file.

Return a promise.

**fulfilled** with `true` once the file is closed

### Read

#### `.read(length, position = null)`

Read a Buffer in the file.

* `length`: the number of bytes to read
* `position`: the position where to read the Buffer in the file. If not set, it will use the internal cursor. If set, the internal cursor won't move

Return a promise.

**fulfilled** with the Buffer once the reading is done

#### `.readInt8(position = null)`,
#### `.readUInt8(position = null)`,
#### `.readInt16(position = null)`,
#### `.readUInt16(position = null)`,
#### `.readInt32(position = null)`,
#### `.readUInt32(position = null)`,
#### `.readFloat(position = null)`,
#### `.readDouble(position = null)`

Read a binary type in the file.

* `position`: the position where to read the binary type in the file. If not set, it will use the internal cursor. If set, the internal cursor won't move

Return a promise.

**fulfilled** with the value read once the reading is done

#### `.readString(length, position = null)`

Read a string in the file.

* `length`: the number of bytes of the string to read
* `position`: the position where to read the string in the file. If not set, it will use the internal cursor. If set, the internal cursor won't move

Return a promise.

**fulfilled** with the string read once the reading is done

### Write

#### `.write(buffer, position = null)`

Read a Buffer in the file.

* `buffer`: the Buffer to write
* `position`: the position where to write the Buffer in the file. If not set, it will use the internal cursor. If set, the internal cursor won't move

Return a promise.

**fulfilled** with the number of bytes written once the writing is done

#### `.writeInt8(value, position = null)`,
#### `.writeUInt8(value, position = null)`,
#### `.writeInt16(value, position = null)`,
#### `.writeUInt16(value, position = null)`,
#### `.writeInt32(value, position = null)`,
#### `.writeUInt32(value, position = null)`,
#### `.writeFloat(value, position = null)`,
#### `.writeDouble(value, position = null)`

Write a binary type in the file.

* `value`: the value to write in the corresponding binary type
* `position`: the position where to write the binary type in the file. If not set, it will use the internal cursor. If set, the internal cursor won't move

Return a promise.

**fulfilled** with the number of bytes written once the writing is done

#### `.writeString(string, position = null)`

Write a string in the file.

* `string`: the string to write
* `position`: the position where to write the string in the file. If not set, it will use the internal cursor. If set, the internal cursor won't move

Return a promise.

**fulfilled** with the number of bytes written once the writing is done
