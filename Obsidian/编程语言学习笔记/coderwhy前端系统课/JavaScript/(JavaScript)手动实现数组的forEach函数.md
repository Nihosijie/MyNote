通过手动实现arr.forEach()函数，我们可以加强对回调函数、this的使用和数组遍历方法的理解。
### 定义和用法：
arr.forEach()方法允许为数组的每个元素运行一次函数。
语法：
```javascript
arr.forEach(function(item, index, array) {
	// 对数组元素的处理
})
```

例子:
```javascript
var names = ["张三", "李四", "王五"]
names.forEach(function(item, index, array) {
	console.log(`${array}中第${index}个元素是${value}`)
})

/*
输出：
张三,李四,王五中第0个元素是张三
张三,李四,王五中第1个元素是李四
张三,李四,王五中第2个元素是王五
*/
```

现在，我们开始尝试自己写出一个函数实现上述效果

## 版本1 kForEach()

我们根据`forEach()`方法会对每个数组元素运行一次函数的特点，创建一个方法。
```javascript
function kForEach(fn) {
	for (let i = 0; i < names.length, i++) {
		fn(names[i], i, names)
	}
}
```
这个方法中我们传入了回调方法，通过for循环来保证对数组的每个元素使用一次回调方法。
调用示例：
```javascript
kForEach(function(item, value, array) {
	console.log(`${array}中第${index}个元素是${value}`)
})

/*
输出：
张三,李四,王五中第0个元素是张三
张三,李四,王五中第1个元素是李四
张三,李四,王五中第2个元素是王五
*/
```
在使用时，我们通过回调函数接收数组的item, value和array，并将其输出出来，

在这个版本中我们实现了同样的输出效果，但是这个版本中`names`是被写死在函数中的，不方便复用，所以我们将其改进到版本2

## 版本2 kForEach()
在这个版本中，我们给kForEach() 加一个形参arr，表示要调用的函数
```javascript
function kForEach(fn, arr) {
	for(let i = 0; i < arr.length; i++) {
		fn(arr[i], i, arr)
	}
}
```
我们使用这个函数来遍历names和\[1, 2, 3, 4, 5\]
```javascript
kForEach(function(value, index, arr) {
	console.log(`${array}中第${index}个元素是${value}`)
}, names)
/* 输出
张三,李四,王五 的第 0 个元素是 张三
张三,李四,王五 的第 1 个元素是 李四
张三,李四,王五 的第 2 个元素是 王五
*/

kForEach(function(value, index, arr) {
	console.log(`${array}中第${index}个元素是${value}`)
}, [1, 2, 3, 4, 5])

/* 输出
1,2,3,4,5 的第 0 个元素是 1
1,2,3,4,5 的第 1 个元素是 2
1,2,3,4,5 的第 2 个元素是 3
1,2,3,4,5 的第 3 个元素是 4
1,2,3,4,5 的第 4 个元素是 5
*/

```

在这个版本中，我们通过传入数组增强了代码的复用性，但是arr.forEach()方法可通过 `.` 操作符直接调用，我们这个版本还有改进的空间

## 版本3 kForEach()
在这个版本中，我们将kForEach()方法绑定到了names数组上，将for循环中的`arr`改为`this`，这里的`this`指向了调用方法的names。
```javascript
 // 版本三

names.kForEach = function(fn){
	for(let i = 0; i < this.length; i++) {
		fn(this[i], i, this)
 	}
 }

 names.forEach(function(item, index, array) {
 	console.log(`${array} 的第 ${index} 个元素是 ${item}`)
 })

/*
输出
张三,李四,王五 的第 0 个元素是 张三
张三,李四,王五 的第 1 个元素是 李四
张三,李四,王五 的第 2 个元素是 王五
*/

```
在这个版本中，我们成功让names可以通过 `.` 运算符调用我们的kForEach()方法，但是其他数组仍无法通过 `.` 运算符调用这个方法，我们继续改进。

## 最终版本 kForEach()
数组Array拥有原型方法，数组类型的元素可使用的属性和方法都被包含于其中，我们可以将我们的 kForEach() 方法绑定到Array.prototype中，以使所有数组都可以调用我们的kForEach() 方法.
```javascript
 Array.prototype.kForEach = function (fn) {
 	for (let i = 0; i < this.length; i++) {
	 	fn(this[i], i, this)
	 }
 }

 names.kForEach(function (item, index, array) {
 	console.log(`${array} 的第 ${index} 个元素是 ${item}`)
 })
/*
输出
张三,李四,王五 的第 0 个元素是 张三
张三,李四,王五 的第 1 个元素是 李四
张三,李四,王五 的第 2 个元素是 王五
*/
 var nums = [1, 2, 3, 4, 5]
 nums.kForEach(function (item, index, array) {
 	console.log(`${array} 的第 ${index} 个元素是 ${item}`)
 })
/*
输出
1,2,3,4,5 的第 0 个元素是 1
1,2,3,4,5 的第 1 个元素是 2
1,2,3,4,5 的第 2 个元素是 3
1,2,3,4,5 的第 3 个元素是 4
1,2,3,4,5 的第 4 个元素是 5
*/
```

最后看一遍使用arr.foEach()的输出结果
```javascript
names.forEach(function(item, index, item) {
	console.log(`${array} 的第 ${index} 个元素是 ${item}`)
}) 
/*
输出
张三,李四,王五 的第 0 个元素是 张三
张三,李四,王五 的第 1 个元素是 李四
张三,李四,王五 的第 2 个元素是 王五
*/

nums.forEach(function(item, index, item) {
	console.log(`${array} 的第 ${index} 个元素是 ${item}`)
}) 
/*
输出
1,2,3,4,5 的第 0 个元素是 1
1,2,3,4,5 的第 1 个元素是 2
1,2,3,4,5 的第 2 个元素是 3
1,2,3,4,5 的第 3 个元素是 4
1,2,3,4,5 的第 4 个元素是 5
*/
```
和我们自己定义的kForEach()使用效果是一致的。

就像arr.forEach()的实现，其他数组方法例如map(),find()/findIndex()等我们也可以手动实现，大家看完这篇文章后可以自己思考一下如何实现。