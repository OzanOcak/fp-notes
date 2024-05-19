## 1) accesing database file created by expo-sql

use-load-assets.ts is load assets, carry out migration and activate slash screen. this is where we can access the sqlite database

```console
npx expo install expo-file-system
```

```javascript
import * as FileSystem from "expo-file-system";

useEffect(() => {
  console.log(FileSystem.documentDirectory)   
},[])
```
then all we need to do open the link is logged in terminal.

## 2) showing right time for current timestamp 

```javasctipt
createdAt: text("created_at")
		.default(sql`CURRENT_TIMESTAMP`)
		.notNull(),
```

current time stamp is 4 hours off replace it with

```javascript
    .default(sql`(strftime('%Y-%m-%dT%H:%M:%fZ', 'now'))`)
```


