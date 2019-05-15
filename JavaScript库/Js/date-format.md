**日期格式化**
===

> Create by **bytewang** on **2019/5/15 15:07:43**  
> Recently revised in **2019/5/15 15:07:48**


<br>

## 1.转化为指定格式（包含日期、时间）

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



## 2.日期格式化


	function getFormatDate(day) {
	    if(day==undefined || day==''){
	        return ''
	    }

	    if(day&&typeof day ==='string'&&day.indexOf('-')>=0){
	        day=day.replace(/-/g, "/");
	    }
	    day=new Date(day);
	    var Year = 0;
	    var Month = 0;
	    var Day = 0;
	    var CurrentDate = "";
		//初始化时间

    	Year = day.getFullYear();//ie火狐下都可以
	    Month = day.getMonth() + 1;
	    Day = day.getDate();
	
		    CurrentDate += Year + "-";
	    if (Month >= 10) {
	        CurrentDate += Month + "-";
	    } else {
	        CurrentDate += "0" + Month + "-";
	    }
	    if (Day >= 10) {
	        CurrentDate += Day;
	    } else {
	        CurrentDate += "0" + Day;
	    }

    	return CurrentDate;
	}


例如：

		let do_date = new Date() // "Wed May 01 2019 00:00:00 GMT+0800 (中国标准时间)"     
		let date = this.getFormatDate(do_date)  //2019-05-14


## 3.本年

	let getThisYear = function () {
	    var d = new Date();
	    var start = new Date(d.getFullYear(), 0, 1); //去年  d.getFullYear()-2
	    var end = new Date(d.getFullYear(), 11, 31);
	    return [start, end];
	};

例如：

		let dateRange = this.getThisYear() //默认本年
		let begin_date = this.getFormatDate(dateRange[0])  //2019-01-01
		let end_date = this.getFormatDate(dateRange[1])  //2019-12-31



## 4.本月（可以指定月份）

		let getCurrentMonth = function (date) {
		    var d = date||new Date();
		    var start = new Date(d.getFullYear(), d.getMonth(), 1);
		    var end = new Date(d.getFullYear(), d.getMonth() + 1, 0);
		    return [start, end];
		};

例如：

		let dateRange = this.getCurrentMonth() //默认当前月份
		let begin_date = this.getFormatDate(dateRange[0])  //2019-05-01
		let end_date = this.getFormatDate(dateRange[1])  //2019-05-31

		let dateRange = this.getCurrentMonth(new Date("2018-08-08"))  //指定时间
		let begin_date = this.getFormatDate(dateRange[0])  //2018-08-01
		let end_date = this.getFormatDate(dateRange[1])  //2018-08-31  


## 5.上月

	let getPreMonth = function (date) {
	    var d = date||new Date();
	    var start = new Date(d.getFullYear(), d.getMonth() - 1, 1);
	    var end = new Date(d.getFullYear(), d.getMonth(), 0);
	    return [start, end];
	};

## 6.下月

	let getPreMonth = function (date) {
		var d =date|| new Date();
	    var start = new Date(d.getFullYear(), d.getMonth() +1, 1);
	    var end = new Date(d.getFullYear(), d.getMonth()+2, 0);
	    return [start, end];
	};


## 7.本周

	let getCurrentWeek = function () {
	    //起止日期数组
	    var startStop = new Array();
	    //获取当前时间
	    var currentDate = this.getCurrentDate();
	    //返回date是一周中的某一天
	    var week = currentDate.getDay();
	    //返回date是一个月中的某一天
	    var month = currentDate.getDate();
	
	    //一天的毫秒数
	    var millisecond = 1000 * 60 * 60 * 24;
	    //减去的天数
	    var minusDay = week != 0 ? week - 1 : 6;
	    //本周 周一
	    var monday = new Date(currentDate.getTime() - (minusDay * millisecond));
	    //本周 周日
	    var sunday = new Date(monday.getTime() + (6 * millisecond));
	    //添加本周时间
	    startStop.push(monday); //本周起始时间
	    //添加本周最后一天时间
	    startStop.push(sunday); //本周终止时间
	    //返回
	    return startStop;
	};

例如：

		let dateRange = this.getCurrentWeek() //默认本周
		let begin_date = this.getFormatDate(dateRange[0])  //2019-05-13
		let end_date = this.getFormatDate(dateRange[1])  //2019-05-19

## 8.上周
	let getPreWeek = function () {
	    var current = this.getCurrentWeek();
	    var start = current[0];
	    var end = current[1];
	    return [new Date(start.getFullYear(), start.getMonth(), start.getDate() - 7), new Date(end.getFullYear(), end.getMonth(), end.getDate() - 7)];
	};