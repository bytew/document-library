**代码简洁实例**
===

> Create by **bytewang** on **2019/1/29 11:24:23**  
> Recently revised in **2019/1/29 19:46:44**

<br>

## 1.链式操作
在访问对象嵌套的属性时，无法事先确定对象的属性是否存在？有时就得写这样的代码。 

    let data
	if(myObj && myObj.firstProp && myObj.firstProp.secondProp && myObj.firstProp.secondProp.actualData) {
		data = myObj.firstProp.secondProp.actualData
	}
	
如何使代码更简洁。 
使用optional chaining方法，用法如下   

    let data = myObj?.firstProp?.secondProp?.actualData   

目前，optional chaining还不是官方标准的一部分，但它是个stage-1的实验性功能。需要在babelrc中加入@babel/plugin-proposal-optional-chaining来启用它。



## 2.真值和假值
在使用默认值时，通常需要检查存在的值。一般直接使用真值和假值，常用写法：
    
	if(myBool === true){}
	if(myString.length > 0){}
	if(isNaN(myNumber)){}	
	
可以写成：
  
	if(myBool){}
	if(myString){}
	if(!myNumber){}	

**假值** 

- 长度为0的字符串
- 数字0
- false
- underfined
- null
- NaN

**真值**

- 空数组
- 空对象
- 任何东西

当检查真值或假值时，不需要明确写出比较，这相当于使用双等号 == 而不是三等号 ===。一般来说，这种用法的行为与预想是一致的，但有可能会遇到bug。比如，我最常遇到但就是有关数字0的bug。



## 3.命名

- 常量  

一段时候后，还能记得86400000是什么吗？

	setTimeout(start,86400000);
	
如果这样呢

	let MILLISECOND_IN_A_DAY = 86400000;
	setTimeout(start,MILLISECOND_IN_A_DAY);
这样会不会更好



- 函数  

看函数名就应该知道它是干啥的   

	function addToDate(date, month) {
  		// ...
	}

	const date = new Date();

	// 很难知道是把什么加到日期中
	addToDate(date, 1);

如果这样呢  

	function addMonthToDate(month, date) {
  		// ...
	}

	const date = new Date();
	addMonthToDate(1, date);