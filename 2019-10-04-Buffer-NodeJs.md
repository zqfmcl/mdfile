---
title: Buffer-NodeJs
date: 2019-10-04 10:00:00
tags: NodeJs
---

<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

- [Buffer类](#buffer类)
  - [创建](#创建)
    - [新的API](#新的api)
  - [写入](#写入)
  - [读取](#读取)
    - [String.fromCharCode()](#stringfromcharcode)
    - [stringObject.charCodeAt(index)](#stringobjectcharcodeatindex)
  - [将 Buffer 转换为 JSON 对象](#将-buffer-转换为-json-对象)
  - [合并缓冲区](#合并缓冲区)
  - [拷贝缓冲区](#拷贝缓冲区)
  - [缓冲区裁剪](#缓冲区裁剪)
  - [缓冲区长度](#缓冲区长度)
  - [静态方法](#静态方法)

<!-- tocstop -->

## Buffer类

### 创建

------

- 方法 1

创建长度为 10 字节的 Buffer 实例：

```
var buf = new Buffer(10);
```

- 方法 2

通过给定的数组创建 Buffer 实例：

```
var buf = new Buffer([10, 20, 30, 40, 50]);
```

- 方法 3

通过一个字符串来创建 Buffer 实例：

```
var buf = new Buffer("www.abc.com", "utf-8");
```

------

> 以上方法在Node.js v6.0后废弃，不建议使用。

#### 新的API

- Buffer.from()
- Buffer.alloc()
- Buffer.allocUnsafe

```js
// 创建一个长度为 10、且用 0 填充的 Buffer。
const buf1 = Buffer.alloc(10);

// 创建一个长度为 10、且用 0x1 填充的 Buffer。
const buf2 = Buffer.alloc(10, 1);

// 创建一个长度为 10、且未初始化的 Buffer。
// 这个方法比调用 Buffer.alloc() 更快，
// 但返回的 Buffer 实例可能包含旧数据，
// 因此需要使用 fill() 或 write() 重写。
const buf3 = Buffer.allocUnsafe(10);

// 创建一个包含 [0x1, 0x2, 0x3] 的 Buffer。
const buf4 = Buffer.from([1, 2, 3]);

// 创建一个包含 ASCII 字节数组 [0x74, 0x65, 0x73, 0x74] 的 Buffer。
const buf5 = Buffer.from('test');

// 创建一个包含 UTF-8 字节数组 [0x74, 0xc3, 0xa9, 0x73, 0x74] 的 Buffer。
const buf6 = Buffer.from('tést', 'utf8');
```

> 创建Buffer类长度是固定的，不可以更改。
> 打印Buffer，会以16进制编码格式显示。

### 写入

语法：

```
buf.write(string[, offset[, length]][, encoding])
```

- string - 写入的字符串。
- offset - 开始写入的buf位置索引值，默认为 0。
- length - 写入的字节数，默认为 buffer.length
- encoding - 使用的编码。默认为 'utf8' 。
  - 支持类型：ASCII、UTF-8、UTF-16LE/UCS-2、Base64、Binary、Hex

```js
buf = new Buffer(256);
len = buf.write("www.abc.com");

console.log("写入字节数 : "+  len);
```

### 读取

#### buf.toString([encoding[, start[, end]]])

把`Buffer`的编码转换成字符。

- encoding - 使用的编码。默认为 'utf8' 。
- start - 指定开始读取的索引位置，默认为 0。
- end - 结束位置，默认为缓冲区的末尾。

```js
var buf = new Buffer(26);

for (var i = 0 ; i < 26 ; i++) {
  buf[i] = i + 97;
}

console.log( buf.toString('ascii'));       // 输出: abcdefghijklmnopqrstuvwxyz
console.log( buf.toString('ascii',0,5));   // 输出: abcde
console.log( buf.toString('utf8',0,5));    // 输出: abcde
console.log( buf.toString(undefined,0,5)); // 使用 'utf8' 编码, 并输出: abcde

```

#### String.fromCharCode()

字符串静态方法， 把 `Unicode` 值转化成字符。

```js
var bf = new Buffer('miaov', 'utf-8');
console.log(bf);

for (var i=0; i<bf.length; i++) {
    //console.log( bf[i].toString(16) );

    console.log( String.fromCharCode( bf[i] ) );
}

//结果
<Buffer 6d 69 61 6f 76>
m
i
a
o
v
```

#### stringObject.charCodeAt(index)

把字符转化成`Unicode`值。

```js
var str="Hello world!"
document.write(str.charCodeAt(1))
//101
```

### 将 Buffer 转换为 JSON 对象

```
buf.toJSON()
```

```js
var buf = new Buffer('www.abc.com');
var json = buf.toJSON(buf);

console.log(json);

//[ 119, 119, 119, 46, 114, 117, 110, 111, 111, 98, 46, 99, 111, 109 ]
```

### 合并缓冲区

```
Buffer.concat(list[,totalLength])
```

- list - 用于合并的 Buffer 对象数组列表。
- totalLength - 指定合并后Buffer对象的总长度。

### 拷贝缓冲区

```
buf.copy(targetBuffer[, targetStart[, sourceStart[, sourceEnd]]])
```

- targetBuffer - 要拷贝的 Buffer 对象。
- targetStart - 数字,写入的Buffer对象的开始位置, 可选, 默认: 0
- sourceStart - 数字,拷贝Buffer对象的开始位置 可选, 默认: 0
- sourceEnd - 数字, 拷贝Buffer对象的结束位置，Â可选, 默认: buffer.length

```js
var buffer1 = new Buffer('ABC');
// 拷贝一个缓冲区
var buffer2 = new Buffer(3);
buffer1.copy(buffer2);
console.log("buffer2 content: " + buffer2.toString());

//buffer2 content: ABC
```

### 缓冲区裁剪

```
buf.slice([start[, end]])
```

- start - 数字, 可选, 默认: 0
- end - 数字, 可选, 默认: buffer.length

```js
var buffer1 = new Buffer('abc');
// 剪切缓冲区
var buffer2 = buffer1.slice(0,2);
console.log("buffer2 content: " + buffer2.toString());
//buffer2 content: ab
```

### 缓冲区长度

```
buf.length
```

### 静态方法

- Buffer.isEncoding(encoding)

判断是否支持这个编码方式。

- Buffer.isBuffer(obj)

测试这个 `obj` 是否是一个 `Buffer`。

- Buffer.byteLength(string, [encoding])

将会返回这个字符串真实**字节长度**。

```js
var str='heoo林喔';
console.log(Buffer.byteLength(str));
console.log(Buffer.byteLength(str,'utf-8'));
console.log(Buffer.byteLength(str,'ascii'));
console.log(Buffer.byteLength(str,'base64'));

//结果
10
10
6
4
```

不同的编码方式，字节长度会不一样。

- Buffer.concat(list, [totalLength])

```js
var str1 = 'miaov';
var str2 = '妙味';

var list = [new Buffer(str1), new Buffer(str2)];
console.log(list);
```