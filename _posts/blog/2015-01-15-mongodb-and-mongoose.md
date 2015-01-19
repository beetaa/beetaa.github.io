---
layout: post
title: Mongodb 和 Mongoose 使用
description: Mongodb 和 Mongoose 有很多坑，也有很多梯子，慢慢整理。
category: blog
---

Mongodb 和 Mongoose 有很多坑，也有很多梯子，慢慢整理。

## 一、使用 Model.collection.insert 解决新建大量数据的问题
<hr/>

## 二、使用地理位置索引快速获取随机数据

1. 在 mongoose 中定义并索引地理位置字段
    
    var place = new Schema({
        userId: ObjectId,
        username: String,
        geo: {type: [Number], index: '2d', default: [Math.random(), 0]}
    });
    
2. 查找1条文档
    
    Place.findOne( { random_point : { $near : [Math.random(), 0] } } );
    
3. 查找多条文档
    
    Place.find( { random_point : { $near : [Math.random(), 0] } } ).limit( 4 );
    

### 附录1：用户认证好文收录

- [Mongoose (mongodb) batch insert?](http://stackoverflow.com/questions/16726330/mongoose-mongodb-batch-insert)
- [Random record from MongoDB](http://stackoverflow.com/questions/2824157/random-record-from-mongodb)
- [Geospatial Queries With Mongoose and Node.js](http://java.dzone.com/articles/geospatial-queries-mongoose)