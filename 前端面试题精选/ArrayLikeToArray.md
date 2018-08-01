### 类数组对象转成数组对象

#### 类数组对象定义

* 拥有length属性，其它属性（索引）为非负整数
* 不具有数组所具有的方法 


常见的类数组有arguments和NodeList

《javascript权威指南》里面给出了一个鉴别对象是否是类数组的函数：
```
// Determine if o is an array-like object.
// Strings and functions have numeric length properties, but are 
// excluded by the typeof test. In client-side JavaScript, DOM text
// nodes have a numeric length property, and may need to be excluded 
// with an additional o.nodeType != 3 test.
function isArrayLike(o) {
    if (o &&                                // o is not null, undefined, etc.
        typeof o === 'object' &&            // o is an object
        isFinite(o.length) &&               // o.length is a finite number
        o.length >= 0 &&                    // o.length is non-negative
        o.length===Math.floor(o.length) &&  // o.length is an integer
        o.length < 4294967296)              // o.length < 2^32
        return true;                        // Then o is array-like
    else
        return false;                       // Otherwise it is not
}
```

#### 类数组对象转成对象方法

* 利用Array的slice方法，同样可用来复制数组
	```
	function toArray(object){
		try{
			return [].slice.call(object);
		} catch(e){
			var arr = [];  
			for(var i = 0,len = s.length; i < len; i++){   
						arr[i] = s[i];   
			}  
			return arr;
		}
	}
	```
* ES6 Array.from()方法
* ES6 ...扩展运算符 [...object]