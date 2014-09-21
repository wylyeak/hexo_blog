title: JavaWeb中 url中传递中文参数乱码的处理
date: 2011-12-04 14:06:51
tags:
- javaweb
- url
- 乱码
- 超链接

---

在使用tomcat做容器的时候,tomcat默认的字符集是iso-8859-1,所以在使用的时候会造成中文的乱码的问题;

一般的POST请求,通过struts 或者 过滤器 配置下 就能解决.

超链接中如果传递参数为中文,就会出现乱码的情况,所以采用以下方法可以解决之:

<!-- more -->

网上的一般方法为:

1. 修改tomcat默认字符集(不推荐,一般托管的服务器是没法接触到tomcat文件的)
2. 在中文连接请求之前js对中文执行encodeURI或者encodeURIComponent方法
3. 编码重组

页面端直接输出中文的链接
``` html
<a href="sevlet?test=中文">test</a>
```
页面中该是怎样就怎样
在后台对字符编码测试,如果是iso-8859-1则进行编码重组.
``` java
//如果字符串是采用iso-889-1编码的话,则下个判断会返回true
if(Charset.forName("ISO-8859-1").newEncoder().canEncode(key)){
   try {
       key = new String(key.getBytes("ISO-8859-1"),"gbk");
   } catch (UnsupportedEncodingException e) {
       e.printStackTrace();
   }
}
```
