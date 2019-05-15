**日期格式化**
===

> Create by **bytewang** on **2019/5/15 15:07:43**  
> Recently revised in **2019/5/15 15:07:48**


<br>

## 1.转化为指定格式

	function getFormatTime(date, fmt) {
  		date = date.replace(/-/g, "/"); //兼容Safari浏览器
  		date = new Date(date)
	  	var o = {
		    "M+": date.getMonth() + 1, //月份
		    "d+": date.getDate(), //日
		    "h+": date.getHours(), //小时
		    "m+": date.getMinutes(), //分
		    "s+": date.getSeconds(), //秒
		    "q+": Math.floor((date.getMonth() + 3) / 3), //季度
		    "S": date.getMilliseconds() //毫秒
	 	};
		  if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (date.getFullYear() + "").substr(4 - RegExp.$1.length));
		  for (var k in o)
		    if (new RegExp("(" + k + ")").test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
		  return fmt;
	}

例如：

		let do_date = "2019-05-14 10:10:54"     
		let time = this.getFormatTime(do_date."hh:mm")  //10:10    yyyy-MM-dd hh:mm:ss