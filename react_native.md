## 1) accesing database file created by expo-sql

use-load-assets.ts is load assets, carry out migration and activate slash screen. this is where we can access the sqlite database

```javascript
import * as FileSystem from "expo-file-system";

useEffect(() => {
  console.log(FileSystem.documentDirectory)   
},[])
```
then all we need to do open the link is logged in terminal.
