
NodeJS Module Wrapper
```javascript
(function wrapper (exports, require, module, __filename, __dirname) {  
       
    
 });
```

Every source code in nodejs, is stored in NodeJS wrapper and that runs when executed like wrapper();


require checks / starts searching

First, if there is 3rd party
Second, built in module,
Third, Error Throw now


require('./math.js') , search math in current directory

./ current
../ one directory up
../../ 2 directory up



On Root Project, create a file package.json, it is a configuration file for the project:

like, Name, version, scripts, dependencies {}, 

use npm init, automatically creates package.json file for me.

dependicies keeps track for all third party modules in the project

