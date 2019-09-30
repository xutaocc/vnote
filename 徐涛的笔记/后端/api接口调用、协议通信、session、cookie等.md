# 协议通信、接口、https、session、cookie等

## request对象获取请求行、请求头信息

<pre>

一、作用

封存了当前请求的所有请求信息

二、使用

获取请求头的信息包括：

1.请求行：请求方式 请求URL/URI 协议版本

//获取请求行
		     String method=req.getMethod();
		     StringBuffer url=req.getRequestURL();
		     String uri=req.getRequestURI();
		     String scheme=req.getScheme();
		     System.out.println("请求行："+method+" "+uri+" "+scheme);
2.请求头：键值对

 //获取请求头
		     Enumeration enumeration=req.getHeaderNames();
		     System.out.println("请求头：");
		     while(enumeration.hasMoreElements()) {
		    	 String name=(String)enumeration.nextElement();
		    	 String value=req.getHeader(name);
		    	 System.out.println(name+" "+value);
		     }
3.请求数据

  //获取请求实体
		     req.getParameter("键名");       //返回指定的用户数据
		     req.getParameterValues("键名"); //返回同键不同值的string数组，如前台页面的多选框
		     req.getParameterNames();        //返回所有用户请求数据的枚举集合
 

运行结果：

请求行：GET /sx/s2 http
请求头：
host localhost:8080
connection keep-alive
cache-control max-age=0
upgrade-insecure-requests 1
user-agent Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36
accept text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
accept-encoding gzip, deflate, br
accept-language zh-CN,zh;q=0.9
注意：如果是URL则：完整的浏览器访问地址（http://localhost:8080/sx/s2）

注意：如果是URI则：虚拟项目名+对应的servlet名字（/sx/s2）

注意：获取请求实体数据的时候，无论是get方式还是post方式，都是用 req.getParameter("键名"); 
 ———————————————— 
版权声明：本文为CSDN博主「世宇同学」的原创文章，遵循CC 4.0 by-sa版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_40327259/article/details/83277006

</pre>

## session和cookie


> 总结：
+ 正常情况浏览器关闭session会话结束，对应为关闭浏览器再打开每次JSESSIONID,A97064CBBDEE1F83474047244E63A123都不一样。登录记住功能另说（[记住我token功能原理](https://blog.csdn.net/uotail/article/details/90281775)）
+ cookie可以设置失效时间，一般在有效期内同一个客户端会一直保留这个cookie。

### 彻底理解[彻底理解cookie，session，token](https://www.cnblogs.com/moyand/p/9047978.html)


### session的使用说明[链接](https://blog.csdn.net/qq_35029061/article/details/82914687)



#### 一、Session会话
<pre>
session对象用于在会话范围内，记录每个客户端的访问状态，以便于跟踪每个客户端的操作状态，在会话存储的信息，在浏览器发出后续请求时可以获取这些会话的有效数据。  

     从客户打开浏览器连接到服务器，到客户关闭浏览器离开这个服务器，称做一个会话。当客户访问服务器是，可能会反复连接这个服务器上的几个页面、反复刷新一个页面或不断地向一个页面提交信息等，服务器应当通过某种方法知道这是同一个客户，这时就需要session对象。

     在jsp页面中可以直接使用session对象（jsp的内置对象），也可以通过pageContext.getSession()或者request.getSession重新回去session对象。 

session的工作原理如下：

    客户首次访问服务器的一个页面时，服务器就会为该用户分配一个session对象，同时为这个session指定唯一的ID，并且将该ID发送到客户端并写入到cookie中，使得客户端与服务器的session建立一一对应的关系；  

    当客户端继续访问服务器端的其它资源时，服务器不再为该客户分配新的session对象，直到客户端浏览器关闭、超时或调用session的invalidate（）方法使其失效，客户端与服务器的会话结束。

    当客户重新打开浏览器访问网站时，服务器会重新为客户分配一个session对象，并重新分配sessionID。  
</pre>
#### 二、Session的使用
```java
// 获取session
HttpSession session = req.getSession();
// 获取session传过来的值
String 字段名=(String)session.getAttribute("session的字段名");


```

1、public void setAttribute(String name,String value)设定指定名字的属性的值，并将它添加到session会话范围内，如果这个属性是会话范围内存在，则更改该属性的值。  

2、public Object getAttribute(String name)在会话范围内获取指定名字的属性的值，返回值类型为object，如果该属性不存在，则返回null。  

3、public void removeAttribute(String name)，删除指定名字的session属性，若该属性不存在，则出现异常。  

4、public void invalidate（），使session失效。可以立即使当前会话失效，原来会话中存储的所有对象都不能再被访问。  

5、public String getId( )，获取当前的会话ID。每个会话在服务器端都存在一个唯一的标示sessionID，session对象发送到浏览器的唯一数据就是sessionID，它一般存储在cookie中。  

6、public void setMaxInactiveInterval(int interval) 设置会话的最大持续时间，单位是秒，负数表明会话永不失效。  

7、public int getMaxInActiveInterval（）,获取会话的最大持续时间。  

8、使用session对象的getCreationTime()和getLastAccessedTime()方法可以获取会话创建的时间和最后访问的时间，但其返回值是毫秒，一般需要使用下面的转换来获取具体日期和时间。 
 ———————————————— 
版权声明：本文为CSDN博主「wespten」的原创文章，遵循CC 4.0 by-sa版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_35029061/article/details/82914687


### cookie的读写
[链接](https://www.cnblogs.com/zhoulitong/p/6412308.html)
```java
写入cookies

 

	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {		
		Cookie c1 = new Cookie("password","123");
		response.addCookie(c1);
		
		Cookie c2 = new Cookie("client_ip",request.getRemoteAddr());
		
		//设置cookie的生命周期为一个小时，单位为秒
		c2.setMaxAge(60*60);
		response.addCookie(c2);
		
		response.getWriter().println("SetCookies OK!");
	}


读取cookies

 

	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		
		Cookie[] Cookies = request.getCookies();
		for(int i =0;i<Cookies.length;i++){
			Cookie c = Cookies[i];
			response.getWriter().println(c.getName() + "," + c.getValue());
		}
	}


```

---

### 测试小demo
```java
package web;

import javax.servlet.ServletException;
import javax.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Enumeration;

public class Myservlet extends HttpServlet{

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        PrintWriter out = response.getWriter();
        
        Cookie c1 = new Cookie("userInfo","student");
        //设置cookie的生命周期为一个小时，单位为秒
        c1.setMaxAge(20);
        //增加cookie
        response.addCookie(c1);
        response.getWriter().println("SetCookies OK!");

        //增加cookie后下次访问得到相关cookie信息
        Cookie[] Cookies = request.getCookies();
        for(int i =0;i<Cookies.length;i++){
            Cookie c = Cookies[i];
            response.getWriter().println(c.getName() + "," + c.getValue());
            System.out.println("cookie信息："+c.getName() + "," + c.getValue());
        }
        HttpSession session = request.getSession();
        //获取session传过来的值
        session.setAttribute("userSession","xutao");
        String sessionValue=(String)session.getAttribute("userSession");
        System.out.println("session绑定userSession值为："+session.getAttribute("userSession"));
        out.println("");
        out.close();
    }
}





package web;

import javax.servlet.ServletException;
import javax.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Enumeration;

public class SecondServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        PrintWriter out = response.getWriter();
        String method=request.getMethod();
        StringBuffer url=request.getRequestURL();
        String uri=request.getRequestURI();
        String scheme=request.getScheme();
        System.out.println("请求行："+method+" "+uri+" "+scheme);



        Enumeration enumeration=request.getHeaderNames();
        System.out.println("请求头：");
        while(enumeration.hasMoreElements()) {
            String name=(String)enumeration.nextElement();
            String value=request.getHeader(name);
            System.out.println(name+" "+value);
        }


        Cookie[] Cookies = request.getCookies();
        HttpSession session = request.getSession();
        //response.getWriter().println("dier个servlet");
        for(int i =0;i<Cookies.length;i++){
            Cookie c = Cookies[i];
            response.getWriter().println("cookie："+c.getName() + "," + c.getValue());
        }





        out.close();
    }
}



<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
		  http://java.sun.com/xml/ns/javaee/web-app_4_0.xsd"
           version="4.0">
    <!-- 基本配置 -->
    <servlet>
        <servlet-name>myServlet</servlet-name>
        <servlet-class>web.Myservlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>myServlet</servlet-name>
        <url-pattern>/MyFirstServlet</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>SecondServlet</servlet-name>
        <servlet-class>web.SecondServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>SecondServlet</servlet-name>
        <url-pattern>/SecondServlet</url-pattern>
    </servlet-mapping>
</web-app>


```

### token [token](https://blog.csdn.net/vMars_K/article/details/94768858)

## 接口调用的学习
### 使用postman测试上传图片接口[链接](https://jingyan.baidu.com/article/425e69e614f472be14fc166f.html)

### 百度云文字识别调用
1. [获取Access Token](http://ai.baidu.com/docs#/Auth/top),得到token
https://aip.baidubce.com/rest/2.0/ocr/v1/general?access_token=24.5c068b8a3b84ac12395bf1cee8667604.2592000.1569508704.282335-14841593

> 获取应用ak和sk [链接](https://console.bce.baidu.com/ai/#/ai/ocr/app/list)

>在应用管理里面获取对应应用的API Key和Secret Key[链接](https://console.bce.baidu.com/ai/?fromai=1#/ai/ocr/overview/index)，

<pre>
获取Access Token
请求URL数据格式

向授权服务地址https://aip.baidubce.com/oauth/2.0/token发送请求（推荐使用POST），并在URL中带上以下参数：

grant_type： 必须参数，固定为client_credentials；
client_id： 必须参数，应用的API Key；
client_secret： 必须参数，应用的Secret Key；
例如：

https://aip.baidubce.com/oauth/2.0/token?grant_type=client_credentials&client_id=Va5yQRHlA4Fq5eR3LT0vuXV4&client_secret=0rDSjzQ20XUj5itV6WRtznPQSzr5pVw2&
获取access_token示例代码

bashPHPJavaPythonC++C#Node
#!/bin/bash
curl -i -k 'https://aip.baidubce.com/oauth/2.0/token?grant_type=client_credentials&client_id=【百度云应用的AK(API Key)】&client_secret=【百度云应用的SK(Secret Key)】'
说明： 方式一鉴权使用的Access_token必须通过API Key和Secret Key获取。

服务器返回的JSON文本参数如下：

access_token： 要获取的Access Token；
expires_in： Access Token的有效期(秒为单位，一般为1个月)；
其他参数忽略，暂时不用;
例如：

{
  "refresh_token": "25.b55fe1d287227ca97aab219bb249b8ab.315360000.1798284651.282335-8574074",
  "expires_in": 2592000,
  "scope": "public wise_adapt",
  "session_key": "9mzdDZXu3dENdFZQurfg0Vz8slgSgvvOAUebNFzyzcpQ5EnbxbF+hfG9DQkpUVQdh4p6HbQcAiz5RmuBAja1JJGgIdJI",
  "access_token": "24.6c5e1ff107f0e8bcef8c46d3424a0e78.2592000.1485516651.282335-8574074",
  "session_secret": "dfac94a3489fe9fca7c3221cbf7525ff"
}
若请求错误，服务器将返回的JSON文本包含以下参数：

error： 错误码；关于错误码的详细信息请参考下方鉴权认证错误码。
error_description： 错误描述信息，帮助理解和解决发生的错误。
例如认证失败返回：

{
    "error": "invalid_client",
    "error_description": "unknown client id"
}

</pre>

2. 百度调用demo-ajax

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

	</head>
	<body>
	</body>
	<script>


		//传入图片路径，返回base64
		function getBase64(img) {
			function getBase64Image(img, width, height) { //width、height调用时传入具体像素值，控制大小 ,不传则默认图像大小
				var canvas = document.createElement("canvas");
				canvas.width = width ? width : img.width;
				canvas.height = height ? height : img.height;

				var ctx = canvas.getContext("2d");
				ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
				var dataURL = canvas.toDataURL();
				return dataURL;
			}
			var image = new Image();
			image.crossOrigin = '';
			image.src = img;
			var deferred = $.Deferred();
			if (img) {
				image.onload = function() {
					deferred.resolve(getBase64Image(image)); //将base64传给done上传处理
				}
				return deferred.promise(); //问题要让onload完成后再return sessionStorage['imgTest']
			}
		}

		var url = "https://s2.ax1x.com/2019/08/31/mzs6m9.png";
		getBase64(url).then(function(base64) {
			//console.log(base64); //处理成功打印在控制台

			var base64Str = base64;
			//console.log(base64Str);
			var base64Result = base64Str.substring(base64Str.indexOf(",") + 1);//去base64码头部
			//console.log(base64Result);


			$.ajax({
				url: 'https://aip.baidubce.com/rest/2.0/ocr/v1/general?access_token=24.5c068b8a3b84ac12395bf1cee8667604.2592000.1569508704.282335-14841593',
				type: 'post',
				headers: {
					'Content-Type': "application/x-www-form-urlencoded",
				},
				dataType: 'json',
				data: {
					image: base64Result
				}, //｛url:'https://s2.ax1x.com/2019/08/31/mzaIVf.png'},
				async: true, //默认值: true。默认设置下，所有请求均为异步请求。如果需要发送同步请求，请将此选项设置为false。
				success: function(data) {
					console.log(data);
				},
				error: function() {
					console.log("出错了");
				},
			});


		}, function(err) {
			console.log(err); //打印异常信息
		});
	</script>
</html>


```

### 腾讯存储桶的学习调用

#### java-sdk[链接](https://blog.csdn.net/suewar3/article/details/85053955)

```java
package com.hx.apistydy.controller;

import com.qcloud.cos.COSClient;
import com.qcloud.cos.ClientConfig;
import com.qcloud.cos.auth.BasicCOSCredentials;
import com.qcloud.cos.auth.COSCredentials;

import com.qcloud.cos.exception.CosClientException;
import com.qcloud.cos.exception.CosServiceException;
import com.qcloud.cos.model.*;
import com.qcloud.cos.region.Region;
import org.junit.Test;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

import java.io.File;

//@Controller
public class FirstController {
    //API密钥管理-https://console.cloud.tencent.com/cam/capi
    private static final String APPID = "1259134219";//对应APPID
    private static final String ACCESSKEY = "";//对应SecretId
    private static final String SECRETKEY = "";//对应SecretKey

    //存储桶信息-https://console.cloud.tencent.com/cos5/bucket
    private static final String BUCKETNAME = "";//存储桶名字
    private static final String REGIONID = "ap-chengdu";//所属地域
    private static final String KEY="MyFile1/geek.exe";//定义一个文件名
    // 1 初始化用户身份信息(secretId, secretKey)
    COSCredentials cred = new BasicCOSCredentials(ACCESSKEY, SECRETKEY);
    // 2 设置bucket的区域, COS地域的简称请参照 https://cloud.tencent.com/document/product/436/6224
    // clientConfig中包含了设置region, https(默认http), 超时, 代理等set方法, 使用可参见源码或者接口文档FAQ中说明
    ClientConfig clientConfig = new ClientConfig(new Region(REGIONID));
    // 3 生成cos客户端
    COSClient cosClient = new COSClient(cred, clientConfig);


    @Test
    public void testUploadFile(){

        File localFile = new File("D:\\geek.exe");
        PutObjectRequest putObjectRequest = new PutObjectRequest(BUCKETNAME, KEY, localFile);

        // 设置存储类型, 默认是标准(Standard), 低频(standard_ia),一般为标准的
        putObjectRequest.setStorageClass(StorageClass.Standard);

        COSClient cc = cosClient;//getCosClient();
        try {
            PutObjectResult putObjectResult = cc.putObject(putObjectRequest);
            // putobjectResult会返回文件的etag
            String etag = putObjectResult.getETag();
            System.out.println(etag);
        } catch (CosServiceException e) {
            e.printStackTrace();
        } catch (CosClientException e) {
            e.printStackTrace();
        }
        // 关闭客户端
        cc.shutdown();


    }

    @Test
    public void downFile(){
        File downFile = new File("E:\\software\\1.jpg");
        COSClient cc = cosClient;//getCosClient();
        GetObjectRequest getObjectRequest = new GetObjectRequest(BUCKETNAME, KEY);

        ObjectMetadata downObjectMeta = cc.getObject(getObjectRequest, downFile);
        cc.shutdown();
        String etag = downObjectMeta.getETag();
        System.out.println(etag);
    }

}

```
#### js-sdk[链接](https://blog.csdn.net/qq_41485414/article/details/80134908)

```html

<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script src="cos-js-sdk-v5.js" type="text/javascript" charset="utf-8"></script>
		<script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.js"></script>
	</head>

	<body>
		<input id="fileSelector" type="file" name="filename">
		<button id="startUp" type="button">提交11</button>
		<img src="" id="img0" class="img-thumbnail">
	</body>
	<script type="text/javascript">
		var selectedFile;
		var filename;
		$("#fileSelector").change(function() {
			selectedFile = document.getElementById('fileSelector').files[0];
			filename = selectedFile.name;
		});

		$('#startUp').on('click', function() {
			console.log(11)
			var cos = new COS({
				SecretId: '',
				SecretKey: '',
			})
			console.log(cos);
			cos.putObject({
				Bucket: 'xt-1259134219',
				Region: 'ap-chengdu',
				Key: filename,
				StorageClass: 'STANDARD',
				Body: selectedFile, // 上传文件对象
				onProgress: function(progressData) {
					console.log(JSON.stringify(progressData));
				}
			}, function(err, data) {
				console.log(err || data);
				console.log(data.Location);
			});


		})

		function test() {

		}
	</script>
</html>


```

