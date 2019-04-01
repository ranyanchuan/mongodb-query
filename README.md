# mongodb-query

### 数组查询
##### 数组元素模糊匹配
```
db.users.find({badges:"black"},{"_id":1,badges:1})
// 如下示例，数组字段badges每个包含该元素black的文档都将被返回
{ "_id" : 1, "badges" : [ "blue", "black" ] }
{ "_id" : 4, "badges" : [ "red", "black" ] }
{ "_id" : 6, "badges" : [ "black", "blue" ] }
		
```

##### 匹配数组中任意元素
```
db.users.find({"badges" : {$in:[ "black", "blue"]}})  
// badges 中包含 black 或者 blue 元素
{ "_id" : 1, "badges" : [ "blue", "black" ] }
{ "_id" : 4, "badges" : [ "red", "black" ] }
{ "_id" : 6, "badges" : [ "black", "blue" ] }
```
##### 数组元素精确匹配

```
db.users.find({badges:["black","blue"]},{"_id":1,badges:1})
//如下示例，数组字段badges的值为["black","blue"]的文档才能被返回(数组元素值和元素顺序全匹配)
{ "_id" : 6, "badges" : [ "black", "blue" ] }

```

##### 通过数组下标返回指定的文档
```
db.users.find({"badges.1":"black"},{"_id":1,badges:1})
// 数组的下标从0开始，指定下标值则返回对应的文档
//如下示例，返回数组badges中第一个元素值为black的文档
{ "_id" : 1, "badges" : [ "blue", "black" ] }
{ "_id" : 4, "badges" : [ "red", "black" ] }
```
##### 范围条件任意元素匹配查询
```
db.users.find( { finished: { $gt: 15, $lt: 20}},{"_id":1,finished:1})
//查询数组finished的元素值既大于15，又小于20的文档
{ "_id" : 1, "finished" : [ 17, 3 ] }
{ "_id" : 2, "finished" : [ 11, 25 ] }
{ "_id" : 6, "finished" : [ 18, 12 ] }

db.users.insert({"_id":7,finished:[19]})
//下面插入一个新的文档，仅包含单个数组元素
WriteResult({ "nInserted" : 1 })	
```
