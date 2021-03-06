# 六、Linux进阶命令
## 1、curl 命令
  定义：curl 命令是一个利用URL规则在命令行下工作的文件传输工具，Http请求值得是客户端想服务端的请求消息，http请求主要分为get 和post请求两种。
  
  在linux 环境中，可以通过curl 或wget 命令模拟http请求。
  
  支持：DICT、FILE、FTP、FTPS、GOPHER、HTTP、HTTPS、IMAP
  
  curl命令是没有交互的命令。
  
  举例：curl -x 127.0.0.1:8888 https://www.baidu.com/
  
  （可使用Charles工具对8888端口进行代理，可查看发送的请求数据）
  
1）get 请求
- G：使用get请求
- d：指定请求数据

举例：  
curl https://www.baidu.com

curl -G  https://www.baidu.com

curl -X GET  https://www.baidu.com


2）post 请求

-d：指定post 请求体

举例：
curl -d ‘login=12345’  https://www.baidu.com
       
curl -X POST  https://www.baidu.com

3）其他请求
 - 保存响应内容：curl -o tmp.html  https://www.baidu.com
 - 输出通信的整个过程： curl -v  https://www.baidu.com
 - 不输出错误和进度信息： curl -s  https://www.baidu.com

实战：
```
curl -G 127.0.0.1:8888  https://www.baidu.com

curl -X GET  https://www.baidu.com

curl -x 127.0.0.1:8888 -X POST -d 'user=1234'  https://www.baidu.com

curl -x 127.0.0.1:8888 -d 'user=1234' -o tmp.html  https://www.baidu.com
```

## 2、jq命令

定义：jq是一个轻量级的json处理命令。可以对json数据进行分片、过滤、映射和转换。

可查看 https://stedolan.github.io/jq/

1.使用方法：

1） . : 格式优化

2） echo '{"a":11,"b":12}' | jq '.'
 
     
 2.常用方法：
 
 1）内容提取：`echo '{"foo":42,"bar":"less interesting data"}' | jq .foo`
 
 2）从数组中提取单个数据：`echo'[{"a":1,"b":2},{"c":3,"d":4}]' | jq .[0]`
 
 3）从数组中提取所有数据：`echo'[{"a":1,"b":2},{"c":3,"d":4}]' | jq .[]`
 
 4）过滤多个值：`echo'[{"a":1,"b":2},{"c":3,"d":4}]' | jq .[0,1]`
 
 5）数据重组组成数组：`echo'[{"a":1,"b":2},{"c":3,"d":4}]' | jq ‘[.a,.c]’`
 
 6）数据重组成对象：
```
echo'[{"a":1,"b":2},{"c":3,"d":4}]' | jq '{"tmp":.b}' 

echo'[{"a":1,"b":2},{"c":3,"d":4}]' | jq '{"f":.a,"f1":b}' | grep f
```
