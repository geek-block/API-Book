# 第1章 介绍

API Box是一款由北京智博万维科技有限公司（以下简称“智博万维”）开发的产品，专为提供API线下服务而设计。通过联动智博万维的API SaaS服务产品API STORE，API Box可以帮助您轻松构建本地API服务应用。

智博万维开发的API Box，具有以下优点：

```
· 使用简单，易于上手；

· 占用资源少；

· 提供丰富多样的API。
```

通过本文档，用户可以快速了解API Box的安装及使用。

若有疑问，欢迎联系我们：support@geek-block.com。



# 第2章 安装

### 2.1 下载并解压

您可以从官方网站( https://www.geek-block.com/#/home/apiBox )下载该软件包，下面以发布的api-box-linux.zip为例。

在Linux / Unix / Mac平台上，使用root用户运行以下命令解压软件包：

```
$ unzip api-box-linux.zip
$ chmod -R 750 api-box
$ chmod -R 750 static/
```

在Windows平台上，您可以使用压缩软件解压软件包。

### 2.2 服务管理

#### 2.2.1 服务启动

在Linux / Unix / Mac平台上，运行以下命令以启动服务：

```
$ sh box_server.sh start
```

在Windows平台上，您可以双击api-box.exe以启动服务。

访问地址(http://localhost:18008)开始使用API Box。

#### 2.2.2 查看服务状态

在Linux / Unix / Mac平台上，运行以下命令以查看服务状态：

```
$ sh box_server.sh status
```

#### 2.2.3 服务重启

在Linux / Unix / Mac平台上，运行以下命令以重启服务：

```
$ sh box_server.sh restart
```

在Windows平台上，您可以关闭窗口并重新打开以重启服务。

#### 2.2.4 服务停止

在Linux / Unix / Mac平台上，运行以下命令以停止服务：

```
$ sh box_server.sh stop
```

#### 2.2.5 服务更新

在Linux / Unix / Mac平台上，更新服务前需要停止服务。

 ```
$ sh box_server.sh stop
 ```

执行以下命令以更新软件包：

```
$ sh box_server.sh update /data/api-box.tar.gz
```

更新成功后启动服务即可。

在Windows平台上，更新服务前需要停止服务。您可以使用压缩软件解压软件包覆盖文件后重启服务即可。

### 2.3 HTTPS设置

您可以在配置文件中选择是否启用HTTPS服务器，默认为启用。为了设置HTTPS，您首先需要获取TLS/SSL证书。

API Box支持三种类型的TLS/SSL证书:

**由证书颁发机构签名的单域证书**

这些证书为HTTPS请求提供加密安全性，并允许客户端验证API Box服务器的身份。

**证书颁发机构签发的通配证书**

这些证书为HTTPS请求提供加密安全性，并允许客户端验证API Box服务器的身份。

**自签证书**

自签名证书不由CA签名，您可以在自己的机器上生成。与CA签署的证书不同，自签名证书仅为HTTPS请求提供加密安全性，他们不允许客户端验证API Box服务器的身份。如果您无法获得CA签发的证书，我们建议使用自签名证书。如果使用此证书，每个API Box实例都需要一个唯一的自签名证书。



无论您的证书类型如何，API Box都支持由签名证书文件（.crt）和私钥文件（.key）文件对组成的证书。

#### 2.3.1 启动HTTPS

1）进入解压后的目录（第2章），编辑http.conf文件。

```
$ vim conf/http.conf
```

2) 添加配置

```
enableHTTPS = true
enableHttpTLS = true
hTTPSPort = 18443
hTTPSCertFile = "conf/server.crt"
hTTPSKeyFile = "conf/server.key"
```

•    当enableHTTPS和enableHttpTLS的值为true时，表示启动HTTPS。

•    hTTPSPort为HTTPS服务器的端口，默认使用18443端口。

•    hTTPSCertFile和hTTPSKeyFile分别为证书文件和私钥文件的路径，默认内置了一对证书文件和私钥文件，强烈建议您继续进行更换。

3)   重启服务

在Linux / Unix / Mac平台上，运行以下命令以重启服务：

```
$ sh box_server.sh restart
```

在Windows平台上，您可以关闭窗口并重新打开以重启服务。

#### 2.3.2 生成自签证书

下面将介绍使用OpenSSL生成自签名证书。请先安装OpenSSL，您可以从官方网站( https://www.openssl.org/ )获取OpenSSL。

执行以下命令得到证书文件和私钥文件：

```
$ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.crt
```

其中server.crt文件即证书文件，server.key即私钥文件。



# 第3章 授权

首次使用API BOX需要进行授权。授权码绑定机器唯一信息，如更换机器需要重新申请。

### 3.1 获取授权申请文件

点击获取申请码，得到授权申请文件“request.license”。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_request.png)

进入**智博万维**官网( https://www.geek-block.com/#/user/info )的个人中心页面，将授权申请文件上传给我们。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_put_request.png)

上传成功后请耐心等待审核结果，预计审核将在1-3个工作日内完成。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_request_success.png)

### 3.2 上传授权文件

授权通过后，点击下载按钮得到授权文件“response.license“

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_download_response.png)

进入API BOX授权页面，将授权文件上传到API BOX，上传成功后将会显示授权信息。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_put_response.png)

# 第4章 添加API

您有以下两种途径添加API。

### 4.1 在线添加

#### 4.1.1 登录

您可以使用下载功能以获取API。返回API Box(http://localhost:18008/)首页

点击登录按钮，进入登录页面。 

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_login.png)

登录成功后，会自动跳转到个人中心页面，您可以在此页面查看个人信息。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_personal.png)

#### 4.1.2 下载API

点击下载按钮以进入下载页面，您可以在本页面下载您购买过的线下API。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_download_API.png)

#### 4.1.3 更新API

当下载页面的列表提示“update”时，您可以点击更新按钮以获取最新版的API。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_updateAPI.png)

### 4.2 离线添加

如果您的API BOX处于离线状态，您可以使用离线添加的功能以添加API离线包到本地。

#### 4.2.1 下载API离线包

您可以从官方网站( https://www.geek-block.com/#/home/mark )下载获取API离线包（后缀名为”.zb”）。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/download_outline_pkg.png)

#### 4.2.2 添加API

点击添加按钮以进入添加页面，您可以在本页面添加API离线包。

添加成功后，您可以在列表查看刚添加的API。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_add_API.png)

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_add_API2.png)

# 第5章 API使用

API BOX以Restful API的形式对外提供服务，您可以使用HTTP或HTTPS协议来调用服务。 

阅读前请先启动API BOX Server，下面以URL拨测_Linux API作为例子说明。

### 5.1 查看API详情

您可以从API BOX首页(http://localhost:18008)进入我的数据接口页面，点击查看详情按钮以查看API的详情介绍。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_API_introduction.png)

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_API_introduction2.png)

在此页面您可以查看API调用的请求参数说明。

### 5.2 API调用

您可以通过发起HTTP或HTTPS请求来调用API服务。

#### 5.2.1 使用测试功能调用API

您可以从API BOX首页(http://localhost:18008)进入我的数据接口页面，点击测试按钮以进入测试页面。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_test_page.png)

修改请求参数，点击测试按钮发送请求，即可调用API。您可以在调用完成后查看调用结果。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_test_result.png)

#### 5.2.2 使用代码调用API

您可以使用代码发起请求，下面将展示JAVA和Golang的调用示例代码。

##### 5.2.2.1 JAVA调用示例

1） 修改请求地址和请求方式

```
// 这里请修改为接口的调用地址
public static final String REQUEST_URL = "http://localhost:18008/script/scriptToAPI/app_url_check_rhel";
// 这里请修改为接口的请求方式
public static final String REQUEST_METHOD = "POST";
```

2)   根据文档修改请求参数

```
Map<String, Object> params = new HashMap<String, Object>();
// 以下参数为示例API所用，请根据实际情况填写正确的参数
// 此处填真实IP地址
params.put("host", "1.1.1.1");
params.put("port", "22");
// 此处填真实账号
params.put("username", "username");
// 此处填真实密码
params.put("password", "password");
params.put("rate", "1000");
params.put("timeout", "20000");
params.put("IS_MATCH", "");
params.put("MATCH_CONTENT", "");
params.put("INDEX_URL", "https://www.baidu.com");
```

3)   发起请求

```
// 调用
String result = call(params);
System.out.println(result);
```

4)   调用方法

```
public static String call(Map<String, Object> params) throws Exception {
    HttpURLConnection conn = null;
    String result = null;
    try {
        String strUrl = REQUEST_URL;
        URL url = new URL(strUrl);
        conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod(REQUEST_METHOD);
        conn.setRequestProperty("User-agent", userAgent);
        conn.setUseCaches(false);
        conn.setConnectTimeout(DEF_CONN_TIMEOUT);
        conn.setReadTimeout(DEF_READ_TIMEOUT);
        conn.setInstanceFollowRedirects(false);
        conn.setDoInput(true);
        conn.setDoOutput(true);
        conn.connect();
        OutputStream out = conn.getOutputStream();
        out.write(urlEncode(params).getBytes());
        out.flush();
        result = stream2String(conn.getInputStream());
    } catch (Exception e) {
        e.printStackTrace();
    } finally {
        if (conn != null) {
            conn.disconnect();
        }
    }
    return result;
}
```

您可以在附录7.1章节查看JAVA调用示例的完整代码。

##### 5.2.2.2 Golang调用示例

1)   修改请求地址

```
// 这里请修改为接口的调用地址
url := "http://localhost:18008/script/scriptToAPI/app_url_check_rhel"
```

2)   根据文档修改请求参数

```
// 请求参数
values := url.Values{
// 此处填真实IP地址
   "host":          {"1.1.1.1"},
   "port":          {"22"},
// 此处填真实账号
   "username":      {"username"},
// 此处填真实密码
   "password":      {"password"},
   "rate":          {"1000"},
   "timeout":         {"20000"},
   "IS_MATCH":      {""},
   "MATCH_CONTENT": {""},
   "INDEX_URL":     {"https://www.baidu.com"},
}
```

3)   发起请求

```
// 调用服务
resp, err := http.PostForm(postUrl, values)
```

您可以在附录7.2章节查看Golang调用示例的完整代码。

#### 5.2.3 使用命令调用API

您可以使用命令以发起请求，但我们不推荐这种用法。

```
$ curl -i -X POST -H 'Content-type':'application/x-www-form-urlencoded' -d "host=1.1.1.1&port=80&username=username&password=password&sort=start_time&order=desc&pageNum=1&pageSize=5&protocol=http&hostState=all" http://localhost:18008/web/api/dbbackup_jobs_example
```

### 5.3 加密模式下的API调用

开启加密模式后，API调用前可以根据secret参数选择是否对请求参数进行加密，具体开启方式及加密算法请查看第8章。

在加密模式下用户可以根据secret参数选择是否对请求参数进行加密。secret参数作为标志位，默认secret=0。

a)   当secret=0时，表示本次请求的请求参数加密；

b)  当secret=1时，表示本次请求的请求参数不加密。

#### 5.3.1 使用测试功能调用API

您可以在测试页面打开“是否加密”开关以加密本次请求的请求参数。

![images](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/box_check_encrypt.png)

#### 5.3.2 使用代码调用API

您可以使用代码发起请求，下面将展示JAVA和Golang的调用示例代码。

##### 5.3.2.1 JAVA调用示例

加密模式下，在5.2.2.1章节的第2步根据文档修改参数时，您需要设置secret参数的值为1并且对其他请求参数的值进行加密（加密方法请查看第6章），其他步骤不变。	

```
Map<String, Object> params = new HashMap<String, Object>();
// 此处填加密后的真实IP地址
params.put("host", "N3l0Ro7CMO4Tf4bkREeWUA==");
params.put("port", "79jEaCh8+d6B3/DI6Vv2UQ==");
// 此处填加密后的真实账号
params.put("username", "xioA5W8AkY6PUtJaBsbQWw==");
// 此处填加密后的真实密码
params.put("password", "DfVESPOGsvVRAg23l5hMOQ==");
params.put("rate", "MjG/cwy05Pv5Yqt0SzwSNA==");
params.put("timeout", "91tAoMyy1X9z3rqFGNafjQ==");
params.put("IS_MATCH", "");
params.put("MATCH_CONTENT", "");
params.put("INDEX_URL","eYXxdz2Lwj+bZcEf7kCEqK6iPNBHZaZ5VeDNuRagoAU=");
// 加密模式下添加的参数
params.put("secret", "1");
```

您可以选择设置secret参数的值为0，那么您将不需要对请求参数的值进行加密。

```
Map<String, Object> params = new HashMap<String, Object>();
// 以下参数为示例API所用，请根据实际情况填写正确的参数
// 此处填真实IP地址
params.put("host", "1.1.1.1");
params.put("port", "22");
// 此处填真实账号
params.put("username", "username");
// 此处填真实密码
params.put("password", "password");
params.put("rate", "1000");
params.put("timeout", "20000");
params.put("IS_MATCH", "");
params.put("MATCH_CONTENT", "");
params.put("INDEX_URL", "https://www.baidu.com");
// 加密模式下添加的参数 secret=0 不启动加密
params.put("secret", "0");
```

##### 5.3.2.2 Golang调用示例

加密模式下，在5.2.2.2章节的第2步根据文档修改参数时，您需要设置secret参数的值为1并且对其他请求参数的值进行加密（加密方法请查看第6章），其他步骤不变。

```
// 请求参数
values := url.Values{
   // 此处填加密后的真实IP地址
   "host": {"TfRq7RQq/CIY6TWIKIfZTQ=="},
   "port": {"79jEaCh8+d6B3/DI6Vv2UQ=="},
   // 此处填加密后的真实账号
   "username": {"Jux6zGhKGO58Jx7GWBuFQw=="},
   // 此处填加密后的真实密码
   "password":      {"/mjkaXjovenpHU2hZw5aDA=="},
   "rate":          {"aBmYnASyUhnAFWi3qEapxQ=="},
   "timeout":       {"vbT8uDIA79dBSiQ0lTUWHA=="},
   "IS_MATCH":      {""},
   "MATCH_CONTENT": {""},
   "INDEX_URL":     {"eYXxdz2Lwj+bZcEf7kCEqK6iPNBHZaZ5VeDNuRagoAU="},
   // 加密模式下添加的参数 secret=1 启用加密
   "secret": {"1"},
}
```

您可以选择设置secret参数的值为0，那么您将不需要对请求参数的值进行加密。

```
// 请求参数
values := url.Values{
   // 此处填真实IP地址
   "host": {"1.1.1.1"},
   "port": {"22"},
   // 此处填真实账号
   "username": {"username"},
   // 此处填真实密码
   "password":      {"password"},
   "rate":          {"1000"},
   "timeout":         {"20000"},
   "IS_MATCH":      {""},
   "MATCH_CONTENT": {""},
   "INDEX_URL":     {"https://www.baidu.com"},
// 加密模式下添加的参数 secret=0 不启用加密
   "secret": {"0"},
}
```

#### 5.3.3 使用命令调用API

加密模式下，我们不推荐使用命令调用API。

### 5.4 开启身份验证下的API调用

开启身份校验后，API调用前需要在请求头设置box-Authorization，具体开启方式请查看第6章。

在开启身份校验后，如果调用请求没有正确的box-Authorization参数，请求将会返回600614错误码。

#### 5.4.1 使用代码调用API

您可以使用代码发起请求，下面将展示JAVA和Golang的调用示例代码。

##### 5.4.1.1 JAVA调用示例

加密模式下，在5.2.2.1章节的第2步根据文档修改参数时，您需要添加box-Authorization参数，它的值即配置文件中boxAuth的值，其他步骤不变。

```
Map<String, Object> params = new HashMap<String, Object>();
// 以下参数为示例API所用，请根据实际情况填写正确的参数
// 此处填真实IP地址
params.put("host", "1.1.1.1");
params.put("port", "22");
// 此处填真实账号
params.put("username", "username");
// 此处填真实密码
params.put("password", "password");
params.put("rate", "1000");
params.put("timeout", "20000");
params.put("IS_MATCH", "");
params.put("MATCH_CONTENT", "");
params.put("INDEX_URL", "https://www.baidu.com");
params.put("box-Authorization", "WyxuOqy6qtCGagjWxRXDNBJivE7Lm6eKeMUu1sOh3FgjnO9TwqJkGbo8CjpuzuJr");
```

##### 5.4.1.2 Golang调用示例

加密模式下，在5.2.2.2章节的第2步根据文档修改参数时，您需要添加box-Authorization参数，它的值即配置文件中boxAuth的值，其他步骤不变。

```
// 请求参数
values := url.Values{
// 此处填真实IP地址
   "host":          {"1.1.1.1"},
   "port":          {"22"},
// 此处填真实账号
   "username":      {"username"},
// 此处填真实密码
   "password":      {"password"},
   "rate":          {"1000"},
   "timeout":         {"20000"},
   "IS_MATCH":      {""},
   "MATCH_CONTENT": {""},
   "INDEX_URL":     {"https://www.baidu.com"},
// 此处填写配置文件中对应的调用密钥
"box-Authorization":     {" WyxuOqy6qtCGagjWxRXDNBJivE7Lm6eKeMUu1sOh3FgjnO9TwqJkGbo8CjpuzuJr"},
}
```

#### 5.4.2 使用命令调用API

加密模式下，我们不推荐使用命令调用API。



# 第6章 身份验证

### 6.1 启用身份校验

您可以在配置文件中选择是否启用身份校验。

1)   进入http.conf挂载位置（第二章 2.2），编辑http.conf文件。

```
$ vim conf/http.conf
```

2)   添加配置

```
enableAuth=true
boxAuth=WyxuOqy6qtCGagjWxRXDNBJivE7Lm6eKeMUu1sOh3FgjnO9TwqJkGbo8CjpuzuJr
```

当enableAuth的值为true时，表示开启身份校验。此时，boxAuth表示身份校验的密钥且boxAuth可以是任意长度的随机字符串。

3)   重启服务

在Linux / Unix / Mac平台上，运行以下命令以重启服务：

```
$ sh box_server.sh restart
```

在Windows平台上，您可以关闭窗口并重新打开以重启服务。



# 第7章 IP拦截

### 7.1 启用IP拦截

您可以在配置文件中选择是否启用IP拦截。

1)   进入http.conf挂载位置（第二章 2.2），编辑http.conf文件。

```
$ vim conf/http.conf
```

2)   添加配置

```
enableIPTables=true
ipTables=192.168.18.1;192.168.18.2;192.168.18.3
```

当enableIPTables的值为true时，表示开启IP拦截。此时，ipTables表示允许通行的IP地址列表，其中用分号做分割符。

3)   重启服务

在Linux / Unix / Mac平台上，运行以下命令以重启服务：

```
$ sh box_server.sh restart
```

在Windows平台上，您可以关闭窗口并重新打开以重启服务。



# 第8章 加密模式

### 8.1 启用加密模式

您可以在配置文件中选择是否启用加密模式。 

1)   进入http.conf挂载位置（第二章 2.2），编辑http.conf文件。

```
$ vim conf/http.conf
```

2)   添加配置

```
enableSecret = true
aesKey = SPxA9kAdss5yyeEH
ivKey = LXQqqeslloZL11vx
```

当enableSecret的值为true时，表示开启加密模式。此时，aesKey和ivKey的值必须是长度为16位的随机字符串。

3)   重启服务

在Linux / Unix / Mac平台上，运行以下命令以重启服务：

```
$ sh box_server.sh restart
```

在Windows平台上，您可以关闭窗口并重新打开以重启服务。

### 8.2 加密算法

加密算法使用AES算法，加密模式是CBC，填充方式是PKCS5Padding，密钥长度为16位，向量长度为16位，密文使用Base64进行编码。您可以在配置文件里修改密钥和向量，分别对应6.1章节的aesKey和ivKey。

#### 8.2.1 JAVA加密示例

您可以在附录7.3章节查看JAVA加密示例的完整代码。

#### 8.2.2 Golang加密示例

您可以在附录7.3章节查看Golang加密示例的完整代码。

#### 8.2.3 Javascript加密示例

Javascript进行AES加密需要依赖cryptojs，您可以从cryptojs官网(http://cryptojs.altervista.org/)获取cryptojs。

您可以在附录9.4章节查看Javascript加密示例的完整代码。



# 第9章 附录

### 9.1 JAVA调用示例

```
package com.zbww.license;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.UnsupportedEncodingException;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLEncoder;
import java.util.HashMap;
import java.util.Map;

/**
 * JAVA示例代码
 * 
 * @author 北京智博万维科技有限公司
 */
public class JavaExamplePost {

	public static final String DEF_CHARSET = "utf-8";
	public static final int DEF_CONN_TIMEOUT = 30000;
	public static final int DEF_READ_TIMEOUT = 30000;
	public static final String userAgent = "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.75 Safari/537.36";

	// 这里请修改为接口的调用地址
	public static final String REQUEST_URL = "http://localhost:18008/script/scriptToAPI/app_url_check_rhel";

	public static final String REQUEST_METHOD = "POST";

	public static void main(String[] args) {
		try {
			Map<String, Object> params = new HashMap<String, Object>();
			// 以下参数为示例API所用，请根据实际情况填写正确的参数
			// 此处填加密后的真实IP地址
//			params.put("host", "N3l0Ro7CMO4Tf4bkREeWUA==");
//			params.put("port", "79jEaCh8+d6B3/DI6Vv2UQ==");
//			// 此处填加密后的真实账号
//			params.put("username", "xioA5W8AkY6PUtJaBsbQWw==");
//			// 此处填加密后的真实密码
//			params.put("password", "DfVESPOGsvVRAg23l5hMOQ==");
//			params.put("rate", "MjG/cwy05Pv5Yqt0SzwSNA==");
//			params.put("timeout", "91tAoMyy1X9z3rqFGNafjQ==");
//			params.put("IS_MATCH", "");
//			params.put("MATCH_CONTENT", "");
//			params.put("INDEX_URL", "eYXxdz2Lwj+bZcEf7kCEqK6iPNBHZaZ5VeDNuRagoAU=");
//			// 加密模式下添加的参数
//			params.put("secret", "1");

			// 此处填真实IP地址
			params.put("host", "1.1.1.1");
			params.put("port", "22");
			// 此处填真实账号
			params.put("username", "username");
			// 此处填真实密码
			params.put("password", "password");
			params.put("rate", "1000");
			params.put("timeout", "20000");
			params.put("IS_MATCH", "");
			params.put("MATCH_CONTENT", "");
			params.put("INDEX_URL", "https://www.baidu.com");

			// 调用
			String result = call(params);
			System.out.println(result);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	/**
	 * 调用API
	 *
	 * @param strUrl 请求地址
	 * @param params 请求参数
	 * @param method 请求方法
	 * @return 请求返回值
	 * @throws Exception
	 */
	public static String call(Map<String, Object> params) throws Exception {
		HttpURLConnection conn = null;
		String result = null;
		try {
			String strUrl = REQUEST_URL;
			URL url = new URL(strUrl);
			conn = (HttpURLConnection) url.openConnection();
			conn.setRequestMethod(REQUEST_METHOD);
			conn.setRequestProperty("User-agent", userAgent);
			conn.setUseCaches(false);
			conn.setConnectTimeout(DEF_CONN_TIMEOUT);
			conn.setReadTimeout(DEF_READ_TIMEOUT);
			conn.setInstanceFollowRedirects(false);
			conn.setDoInput(true);
			conn.setDoOutput(true);
			conn.connect();
			OutputStream out = conn.getOutputStream();
			out.write(urlEncode(params).getBytes());
			out.flush();
			result = stream2String(conn.getInputStream());
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			if (conn != null) {
				conn.disconnect();
			}
		}
		return result;
	}

	/**
	 * 将返回结果为字符串型的API的返回结果数据流转为字符串
	 *
	 * @param in 调用API获得的返回结果数据流
	 * @return 返回结果字符串
	 */
	public static String stream2String(InputStream in) {
		String ret = null;
		try {
			StringBuffer sb = new StringBuffer();
			BufferedReader reader = new BufferedReader(new InputStreamReader(in, DEF_CHARSET));
			String strRead = null;
			while ((strRead = reader.readLine()) != null) {
				sb.append(strRead);
			}
			ret = sb.toString();
		} catch (Exception e) {
			e.printStackTrace();
		}
		return ret;
	}

	/**
	 * 将Map型转为请求参数型
	 *
	 * @param data 参数Map
	 * @return
	 * @throws UnsupportedEncodingException
	 */
	public static String urlEncode(Map<String, Object> data) throws UnsupportedEncodingException {
		StringBuilder sb = new StringBuilder();
		for (Map.Entry<String, Object> i : data.entrySet()) {
			sb.append("&").append(i.getKey()).append("=").append(URLEncoder.encode(i.getValue() + "", "utf-8"));
		}
		sb.delete(0, 1);
		return sb.toString();
	}
}
```

### 9.2 Golang调用示例

```
package main

import (
   "fmt"
   "io/ioutil"
   "net/http"
   "net/url"
)

/**
 * Golang示例代码
 * @author 北京智博万维科技有限公司
 */
func main() {

   // 请求地址
   postUrl := "http://localhost:18008/script/scriptToAPI/app_url_check_rhel"

   // 请求参数
   //values := url.Values{
   // // 此处填加密后的真实IP地址
   // "host": {"N3l0Ro7CMO4Tf4bkREeWUA=="},
   // "port": {"79jEaCh8+d6B3/DI6Vv2UQ=="},
   // // 此处填加密后的真实账号
   // "username": {"xioA5W8AkY6PUtJaBsbQWw=="},
   // // 此处填加密后的真实密码
   // "password":      {"DfVESPOGsvVRAg23l5hMOQ=="},
   // "rate":          {"aBmYnASyUhnAFWi3qEapxQ=="},
   // "timeout":       {"vbT8uDIA79dBSiQ0lTUWHA=="},
   // "IS_MATCH":      {""},
   // "MATCH_CONTENT": {""},
   // "INDEX_URL":     {"eYXxdz2Lwj+bZcEf7kCEqK6iPNBHZaZ5VeDNuRagoAU="},
   // // 加密模式下添加的参数 secret=1 启用加密
   // "secret": {"1"},
   //}

   // 请求参数
   values := url.Values{
      // 此处填真实IP地址
      "host": {"1.1.1.1"},
      "port": {"22"},
      // 此处填真实账号
      "username": {"username"},
      // 此处填真实密码
      "password":      {"password"},
      "rate":          {"1000"},
      "timeout":       {"20000"},
      "IS_MATCH":      {""},
      "MATCH_CONTENT": {""},
      "INDEX_URL":     {"https://www.baidu.com"},
   }

   // 向API BOX发起请求
   resp, err := http.PostForm(postUrl, values)
   if nil != resp {
      defer resp.Body.Close()
   }
   if nil != err {
      fmt.Println(err)
   } else {
      // 读取响应体
      resBody, _ := ioutil.ReadAll(resp.Body)
      // 输出
      fmt.Println(string(resBody))
   }
}
```

### 9.3 JAVA加密示例

```
import javax.crypto.Cipher;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Base64;

/**
 * AES-CBC-128 PKCS5Padding
 * @author 北京智博万维科技有限公司
 */
public class AESExample {
    // 密钥
    private static final String KEY = "SPxA9kAdss5yyeEH";
    // 向量
    private static final String ivKEY = "LXQqqeslloZL11vx";
    // 算法
    private static final String ALGOR = "AES";
    // 模式
    private static final String ALGORITHMSTR = "AES/CBC/PKCS5Padding";
    // 编码格式
    private static final String CHARSET = "utf-8";

    /**
     * 加密
     * 
     * @param sSrc
     * @param sKey
     * @return
     * @throws Exception
     */
    public static String Encrypt(String src) throws Exception {
        if (KEY == null) {
            System.out.println("key不能为空");
            return null;
        }
        // 判断key是否为16位
        if (KEY.length() != 16) {
            System.out.println("key长度不等于16位");
            return null;
        }
        byte[] raw = KEY.getBytes(CHARSET);
        SecretKeySpec skeySpec = new SecretKeySpec(raw, ALGOR);
        // 算法/模式/补码方式
        Cipher cipher = Cipher.getInstance(ALGORITHMSTR);
        // 使用CBC模式，需要一个向量iv，可增加加密算法的强度
        IvParameterSpec iv = new IvParameterSpec(ivKEY.getBytes());
        cipher.init(Cipher.ENCRYPT_MODE, skeySpec, iv);
        byte[] encrypted = cipher.doFinal(src.getBytes());
        // 使用BASE64做编码
        return new Base64().encodeToString(encrypted);
    }

    /**
     * 解密
     * 
     * @param sSrc
     * @param sKey
     * @return
     * @throws Exception
     */
    public static String Decrypt(String src) throws Exception {
        try {
            // 判断key是否正确
            if (KEY == null) {
                System.out.println("key不能为空");
                return null;
            }
            // 判断Key是否为16位
            if (KEY.length() != 16) {
                System.out.println("key长度不等于16位");
                return null;
            }
            byte[] raw = KEY.getBytes(CHARSET);
            SecretKeySpec skeySpec = new SecretKeySpec(raw, ALGOR);
            Cipher cipher = Cipher.getInstance(ALGORITHMSTR);
            IvParameterSpec iv = new IvParameterSpec(ivKEY.getBytes());
            cipher.init(Cipher.DECRYPT_MODE, skeySpec, iv);
            byte[] encrypted1 = new Base64().decode(src);// 先用base64解密
            try {
                byte[] original = cipher.doFinal(encrypted1);
                String originalString = new String(original);
                return originalString;
            } catch (Exception e) {
                System.out.println(e.toString());
                return null;
            }
        } catch (Exception ex) {
            System.out.println(ex.toString());
            return null;
        }
    }

    public static void main(String[] args) throws Exception {
        // 此处是需要加密的内容
        String content = "1.1.1.1";
        System.out.println("加密前：" + content);
        System.out.println("密钥：" + KEY);
        System.out.println("向量：" + ivKEY);
        String encrypt = Encrypt(content);
        System.out.println("加密后：" + encrypt);
        String decrypt = Decrypt(encrypt);
        System.out.println("解密后：" + decrypt);
    }
}
```

### 9.4 Golang加密示例

```
package main

import (
    "bytes"
    "crypto/aes"
    "crypto/cipher"
    "encoding/base64"
    "fmt"
)

/**
 * AES加密
 * 算法模式及填充方式：AES-CBC-128 PKCS5Padding
 * 编码： UTF-8
 * 作者：北京智博万维科技有限公司
 */

/**
 * AES加密
 */
func Encrypt(src, key, iv []byte) []byte {
    aesCipher, err := aes.NewCipher(key)
    if err != nil {
        fmt.Errorf("encrypt error, msg:%s", err)
        return nil
    }
    content := paddingPKCS5(src, aesCipher.BlockSize())
    encrypted := make([]byte, len(content))
    encrypter := cipher.NewCBCEncrypter(aesCipher, iv)
    encrypter.CryptBlocks(encrypted, content)
    return encrypted
}

/**
 * AES解密
 */
func Decrypt(src, key, iv []byte) []byte {
    decrypted := make([]byte, len(src))
    aesBlockDecrypter, err := aes.NewCipher(key)
    if err != nil {
        fmt.Errorf("decrypt error, msg:%s", err)
        return nil
    }
    decrypter := cipher.NewCBCDecrypter(aesBlockDecrypter, iv)
    decrypter.CryptBlocks(decrypted, src)
    return unPaddingPKCS5(decrypted)
}

/**
 * PKCS5包装
 */
func paddingPKCS5(cipherText []byte, blockSize int) []byte {
    padding := blockSize - len(cipherText)%blockSize
    padText := bytes.Repeat([]byte{byte(padding)}, padding)
    return append(cipherText, padText...)
}

/**
 * PKCS5解包装
 */
func unPaddingPKCS5(encrypt []byte) []byte {
    padding := encrypt[len(encrypt)-1]
    return encrypt[:len(encrypt)-int(padding)]
}

func main() {
    // 密钥
    key := "SPxA9kAdss5yyeEH"
    // 向量
    iv := "LXQqqeslloZL11vx"
    // 此处是需要加密的内容
    content := "1.1.1.1"
    fmt.Printf("加密前：%s\n", content)
    fmt.Printf("密钥：%s\n", key)
    fmt.Printf("向量：%s\n", iv)
    encrypt := Encrypt([]byte(content), []byte(key), []byte(iv))
    encryptStr := base64.StdEncoding.EncodeToString(encrypt)
    fmt.Printf("加密后：%s\n", encryptStr)
    decrypt, _ := base64.StdEncoding.DecodeString(encryptStr)
    decryptStr := string(Decrypt(decrypt, []byte(key), []byte(iv)))
    fmt.Printf("解密后：%s\n", decryptStr)
}
```

### 9.5 Javascript加密示例

```
// 加密
function Encrypt (word, sKey, sIV) {
    var key  = CryptoJS.enc.Latin1.parse(sKey);
    var iv   = CryptoJS.enc.Latin1.parse(sIV);
    var encrypted = CryptoJS.AES.encrypt(word, key, {iv:iv, mode: CryptoJS.mode.CBC, padding: CryptoJS.pad.Pkcs7 })
    return encrypted.toString()
}
// 解密
function Decrypt (word, sKey, sIV) {
    var key  = CryptoJS.enc.Latin1.parse(sKey);
    var iv   = CryptoJS.enc.Latin1.parse(sIV);
    let decrypt = CryptoJS.AES.decrypt(word, key, { iv: iv, mode: CryptoJS.mode.CBC, padding: CryptoJS.pad.Pkcs7 });
    let decryptedStr = decrypt.toString(CryptoJS.enc.Utf8);
    return decryptedStr.toString();
}
// 密钥
var key = "SPxA9kAdss5yyeEH";
// 向量
var iv = "LXQqqeslloZL11vx";
// 此处是需要加密的内容
var content = "1.1.1.1";
console.log("加密前：" + content);
console.log("密钥：" + key);
console.log("向量：" + iv);
var encrypt = Encrypt(content, key, iv);
console.log("加密后：" + encrypt);
var decrypt = Decrypt(encrypt, key, iv);
console.log("解密后：" + decrypt);
```

