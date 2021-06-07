# Node Control Parser

A dependency-less node module to parse debian control files.

This supports single paragraph (like in a control file or Release file) 
or multi paragraph like in a Packages file.

The values are in a Map of values. If its set to multi it will return an 
array of Maps.

## Usage
First require the module

```js
const control = require('control-parser');
```
Then you can call it with a string.
```js
control(`Example: This is an example
MultiLine: This is a
  multiline property!
Hello: World`);
```
This example returns 
```js
Map(3) {
  'Example' => 'This is an example',
  'MultiLine' => 'This is a\n  multiline property!',
  'Hello' => 'World'
}
```
### Options:
Currently there is one option, multi. It defaults to `false`. 
When set to true it will read multi-paragraph files and return 
an array of Maps. If set to `false` it will read a single-paragraph
file and return a Map. If a multi-paragraph file is passed while 
this is false it will error.

This here
```js
control(`Example: This is an example
Hello: World

Hello: This is a second paragraph!
Info: Each paragraph is separate and can have the same 
  keys or different ones`,
{multi: true});
```
Will return 
```js
[
  Map(2) { 'Example' => 'This is an example', 'Hello' => 'World' },
  Map(2) {
    'Hello' => 'This is a second paragraph!',
    'Info' => 'Each paragraph is separate and can have the same \n  keys or different ones'
  }
]
```