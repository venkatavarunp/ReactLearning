# JavaScript
## Import and Export 
we can import and export files,variables,libraries across the folder using import and export
```javascript
export let apikey="adasfasdfsdafg";
```
```javascript
import {apikey} from './Util';
```
we can also use `default` export and we can only have one default export per file 
```javascript
export default "asdasfasfasf";
```
```javascript
import apikey from "./util.js";
```
we can import multiple variables using `*`
```javascript
export let apikey="adasfasdfsdafg";
export let token="adasfasdfsdafg";
```
```javascript
import * as util from './Util';
console.log(util.apikey);
console.log(util.token);
```
Here util is an object and we grouped the variables 
**`as` keyword can also be used for aliasing 
```javascript
import {apikey,token as content} from './Util';
console.log(apikey);
console.log(content);
``` 
