# file_get_contents: Unable to find the wrapper https did you forget to enable it when you configured

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

[叶落无痕123](https://blog.csdn.net/u012767761) 2019-06-22 09:45:32 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/articleReadEyes.png) 1273 ![img](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect.png) 收藏

分类专栏： [PHP](https://blog.csdn.net/u012767761/category_6882234.html) [微信开发](https://blog.csdn.net/u012767761/category_6903236.html) [小程序](https://blog.csdn.net/u012767761/category_7352965.html)

file_get_contents(): Unable to find the wrapper "https"- did you forget to enable it when you configured PHP?

[转载地址](http://blog.sina.com.cn/s/blog_4754299501018qsr.html)

1.windows下的PHP，只需要到php.ini中把extension=php_openssl.dll前面的;删掉，重启服务就可以了。 
2.linux下的PHP，就必须安装openssl模块，安装好了以后就可以访问了。 
3.如果服务器你不能修改配置的话，那么就使用curl函数来替代file_get_contents函数，当然不是简单的替换啊。还有相应的参数配置才能正常使用curl函数。 
对curl函数封装如下：

```
php] view plain copy print?



function http_request($url,$timeout=30,$header=array()){  



        if (!function_exists('curl_init')) {  



            throw new Exception('server not install curl');  



        }  



        $ch = curl_init();  



        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);  



        curl_setopt($ch, CURLOPT_HEADER, true);  



        curl_setopt($ch, CURLOPT_URL, $url);  



        curl_setopt($ch, CURLOPT_TIMEOUT, $timeout);  



        if (!empty($header)) {  



            curl_setopt($ch, CURLOPT_HTTPHEADER, $header);  



        }  



        $data = curl_exec($ch);  



        list($header, $data) = explode("\r\n\r\n", $data);  



        $http_code = curl_getinfo($ch, CURLINFO_HTTP_CODE);  



        if ($http_code == 301 || $http_code == 302) {  



            $matches = array();  



            preg_match('/Location:(.*?)\n/', $header, $matches);  



            $url = trim(array_pop($matches));  



            curl_setopt($ch, CURLOPT_URL, $url);  



            curl_setopt($ch, CURLOPT_HEADER, false);  



            $data = curl_exec($ch);  



        }  



 



        if ($data == false) {  



            curl_close($ch);  



        }  



        @curl_close($ch);  



        return $data;  



}
```