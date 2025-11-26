```js
db.collection.save(
   <document>
)
```

collection 是需要操作的表明

document表示支持单个文档

 ISODate 是 MongoDB 的时间类型，它表示的是**格林尼治时间**，它会将包装的时间以格林尼治时间格式插入到数据库中。

```js
 gmtCreated: ISODate('2020-05-12T22:50:43.744+08:00')
```

```js
gmtCreated: new Date()
```

new Date() 会将当前时间以isodate类型插入到数据库中，并且他还有存储空间等优势

save也可以批量插入

```js
db.collection.save(
   [ document1 , document2, ... ],
)
```

save也可以同主键覆盖写入

_id  是主键

如果不加主键会自动添加一个_id值，并且属性是ObjectId ，一个24位的字符串，每个字节两位十六进制数字

使用ObjectId而不是自增的id是因为在多个服务器上同步自动增加主键值既费力还费时

如果指定了_id那么就存入string类型的id



db.collection.find()

db.collection.find({})可以找到所有的数据信息



简单更新

```js
db.ykd_product.update(
  {
    name: '杰克琼斯运动寸衫',
  },
  {
    $set: {
      crossedPrice: 999,
      currentPrice: 599,
    },
  }
);
```

如果想在执行更新时，不存在则插入值，那么写入第三个upsert参数true，不需要时可以省略 upsert



