**代码简洁实例**
===

> Create by **bytewang** on **2019/1/29 11:24:23**  
> Recently revised in **2019/1/29 11:24:32**

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



## 2.更多实例