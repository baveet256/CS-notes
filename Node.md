
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

To install packages, which actually has all the external names of libraries installed, we need a package.json file / make our current project as a package.

On Root Project, create a file package.json, it is a configuration file for the project:

like, Name, version, scripts, dependencies {}, 

use npm init, automatically creates package.json file for me.

dependicies keeps track for all third party modules in the project.

node_modules/ has all the source code of 3rd party modules that are installed. 

node_modules are always ignored so yea if someone clones your repo, just do npm install, the package.json has the info of all the depencies and the same environment would be recreated there.


package-lock.json - Maintains depencies of dependencies. 





