#test
----------------------------------
## JavaWeb ##
### 1.HttpServletRequest 获取客户端IP ###
**X-Forwarded-For**:简称XFF头，它代表客户端，也就是HTTP的请求端真实的IP，  
只有在通过了HTTP 代理或者负载均衡服务器时才会添加该项。  

    public String getRemortIP(HttpServletRequest request) {
      if (request.getHeader("x-forwarded-for") == null) {
       return request.getRemoteAddr();
      }else
       return request.getHeader("x-forwarded-for");
    }

###2.request.getContextPath()获取项目根路径

- <%=request.getContextPath()%>是为了解决相对路径的问题，可返回站点的根路径。
request.getContextPath()适合在jsp中使用，在JS中无法使用。  
- 在JS中可以使用  

    	var localObj = window.location;  
    	var contextPath = localObj.pathname.split("/")[1];

###3.JSON转换为JavaBean

在JavaWeb中，通过request.getParameter()获取前台页面传来的JSON字符串（String），转换成bean。

    // 获取JSON字符串
	String personInfo = request.getParameter("personInfo");
    // 解析为JSON对象
	JSONObject jsonObj = JSONObject.fromObject(personInfo);
    // 转换为Bean，需要一个事先写好的JavaBean的支持
	PersonInfoBean bean = (PersonInfoBean) JSONObject.toBean(jsonObj,
			PersonInfoBean.class);
参考：[Json与javaBean之间的转换工具类](http://www.oschina.net/code/snippet_931591_17607)

###4.Web实现屏幕滚动切换效果

使用Mootools.js库实现左右滚动切换效果。  
为解决Mootools中$与JQuery冲突，采用命名空间将Mootools代码限定在(function($)){})(document.id)中，document.id为Mootools$的别名。

 	  (function($) {
 	  	var whichchannel = 0;
 	  	document.addEvent('domready', function() {
 	  		//滚动事件
 	  		var myFx = new Fx.Tween("ntp-contents", {
 	  			duration: 500 //动画持续时间（毫秒）
 	  		});
 	  		document.addEvent("mousewheel", function(e) {
 	  			if (e.wheel < 0) {
 	  				toLeft(myFx);
 	  			} else {
 	  				toRight(myFx);
 	  			}
 	  		});
 	  		// 绑定切换事件
 	  		$("pre").addEvent("click", function() {
 	  			toRight(myFx);
 	  		});
 	  		$("next").addEvent("click", function() {
 	  			toLeft(myFx);
 	  		});
 	  	});
 	  	function toLeft(myFx) {
 	  		if (myFx.isRunning())
 	  			return;
 	  		if (whichchannel == 1)
 	  			return; // 两屏显示
 	  		whichchannel++;
 	  		$("pre").removeClass("swiper_select");// 切换按钮
 	  		$("next").addClass("swiper_select");
 	  		mg = $$("#ntp-contents")[0].getStyle("marginLeft");
 	  		myFx.start("marginLeft", mg.toInt() - slideWidth);
 	  	}
 	  	function toRight(myFx) {
 	  		if (myFx.isRunning())
 	  			return;
 	  		if (whichchannel == 0)
 	  			return;
 	  		whichchannel--;
 	  		$("pre").addClass("swiper_select");// 切换按钮
 	  		$("next").removeClass("swiper_select");
 	  		mg = $$("#ntp-contents")[0].getStyle("marginLeft");
 	  		myFx.start("marginLeft", mg.toInt() + slideWidth);
 	  	}
 	  })(document.id)
	    //基本的html结构
	    <div id="ntp-contents">
	    	<div id="tiles">
	    		<div id="tile_1"></div>
	    		<div id="tile_2"></div>	
	    	</div>
	    	<div>
	    		<span id="pre"></span>
	    		<span id="next"></span>
	    	</div>
	    </div>

## 在线编程网站 ##
[coder](http://codingbat.com/)：`http://codingbat.com/`

## Linux Kernel ##
在网站**kernel.org**上，有Linux各种版本的内核源代码，如果你想从根本上学习操作系统，也可以通过[LFS](http://www.linuxfromscratch.org/lfs/)快速地学习内核构建的过程。 


## 开源学习 ##
* ruby	Ruby On Rails	：动态语言，简洁清新  
* java	Tomcat	：经典的面向对象静态语言，长盛不衰，优秀项目多如牛毛  
* python	scipy, nltk, django, ansi	：最接近人类语言的通用语言，在开源的科学计算领域一骑绝尘，在数据挖掘、web开发、系统管理等领域也为表现突出  

## 前端技术 ##

### 开发工具
#### Sublime Text  
**安装package control组件**：  

*  按Ctrl+`，调出console；  
*  粘贴以下代码到底部命令行并回车(Sublime Text 2)：

>     import urllib2,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation') 


安装完成之后，可以使用[Package Control](https://packagecontrol.io/)安装插件： 
 
*  按下Ctrl+Shift+P调出命令面板；
*  输入install 调出 Install Package 选项并回车，然后在列表中选中要安装的插件。  

**Sublime Text常用插件**：  

|     Name      |  Description           |
| --------------|:----------------------:|
|     Emmet     |    快速编辑             |
| advanceNewfile| 快速创建文件(ctrl+alt+n) |
| docblocker    | 快速完成注释             |
| autoPrefixer  | CSS自动添加前缀          |
| CSS Format    | CSS格式化               |
| JsFormat      | JS格式化                |
| HtmlTidy      | html格式化(要自定义快捷键)|
| ColorPicker   | ctrl+shift+c 打开调色盘 |

**搭建Java开发环境**：  

*  [Sublime Text 2搭建Java开发环境](http://blog.csdn.net/chszs/article/details/8232051)

### sass  
:  sass是采用的Ruby语言编写的一款css预处理语言，它诞生于2007年，是最早成熟css预处理语言。  
SASS界面编译工具--koala  
[sass学习--w3cplus](http://www.w3cplus.com/sassguide/)
### requireJS
:  RequireJS 是一个JavaScript模块加载器。RequireJS会让你以不同于往常的方式去写JavaScript。你将不再使用script标签在HTML中引入JS文件，

###css hack
[CSS hack技巧大全](http://www.duitang.com/static/csshack.html)
##WEB前端优化

[Yahoo前端优化军规](http://blog.csdn.net/jincenlong58/article/details/9318239)  

优化工具：Yslow  

![](http://i.imgur.com/fgl8j30.jpg)

##ORACLE

###PL/SQL
- [PL/SQL Developer如何连接64位的Oracle图解](http://blog.csdn.net/cselmu9/article/details/8070728)
- PL/SQL 快捷输入设置：
    * 在PL/SQL下的Tools-Preference-Editor-AutoReplace下设置Definition File(根据自己的习惯进行设置)：  
>     sf=select * from
>     ss=select a.*,rowid from
>     s=select
>     fu= for update;
>     w=where
>     u=update
>     cp=create or replace procedure
>     ct=create table
>     cts=create tableas select * from
>     scf=select count(1) from
>     i=insert into
>     ob= order by
>     gb= group by
>     dis=distinct
>     cc=count(1)
>     li=like '%%'
>     inn=is not null



##算法##

###枚举算法
