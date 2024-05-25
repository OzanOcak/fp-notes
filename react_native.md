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

## 3) expo-router passing params, and using it as a number

```javascript
<Link
   asChild
   href={{
     pathname: "/categories",
     params: { id: language.id },
   }}
>
```
then we can get the param by accessing key 

```javascript
   const languageIdParam = useLocalSearchParams()
   useEffect(() => console.log(languageIdParam.id), [])
```
you can also pass multipile parameters

```javascript
<Link
   asChild
   href={{
	pathname: "/words",
	params: { l: languageIdParam.id, c: category.id },
   }}
>
```
and we need to access by using their keys (ex: obj[`key`] )

```javascript
   const params = useLocalSearchParams()

   const lang = params.l
   const cat = params.c
   useEffect(() => console.log(lang, cat), [])
```
