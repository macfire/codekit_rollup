# Rollup prepending function name with "_" when using Codekit

- Rollup Version: 1.24.0
- Operating System (or Browser):  macOS 10.13.6
- Node Version: v12.13.0

### How Do We Reproduce?

Using RollupJS from within CodeKit app (available at https://codekitapp.com)
CodeKit Version 3.10.2

**Note:** 
**I'm not sure if this is a Rollup.js issue or CodeKit app issue.**    
I've submitted an issue to CodeKit (https://github.com/bdkjones/CodeKit/issues/570)   
The CodeKit developer believes this to be a Rollup issue.

Core issue:
Using IIFE bundle format, the outer function variable name is being prepended with an underscore "_".    
This behavior started about August 2019.

Given source:

```javascript

let RollupTest = function () {
    console.log("This is a Rollup test")
};

export default RollupTest;

```

### Expected Behavior

Compiled:

```javascript
var RollupTest = (function () {
    'use strict';

    let RollupTest = function () {
        console.log("This is a Rollup test");
    };

    return RollupTest;

}());

```


### Actual Behavior

The named variable is prepended with an underscore "_"

Compiled:

```javascript
var _RollupTest = (function () {
    'use strict';

    let RollupTest = function () {
        console.log("This is a Rollup test");
    };

    return RollupTest;

}());

```