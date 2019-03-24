从 From Data 中可以查看到许多参数。经过多次实验，发现发生改变的只有 i，salt 和 sign 三个参数值。其中 i 是要翻译的内容，salt 和 sign 的来历和作用前面已经介绍了。但在 API 中 sign 参数是带了 appKey(注册，后台生成) 的，我们没有这个。那么就需要研究一下如何生成 sign 的了。 
在众多请求中，发现一段 js 代码，如下： 

通过上述的 js 代码可知，salt 参数是通过系统时间，加上一个 [1, 10] 的随机数得到的， sign = md5(固定字符串 + 待翻译内容 + salt + 固定字符串) 得到的。这样我们就可以通过代码进行请求了，代码如下
public class YouDao {
    public static void main(String[] args) throws Exception {
        String from = "en";
        String to = "zh-CHS";
        String q = "Who am I? Where am I?";
        String url = "http://fanyi.youdao.com/translate_o?smartresult=dict&smartresult=rule";

        String u = "fanyideskweb";
        String d = q;
        long ctime = System.currentTimeMillis();
        String f = String.valueOf(ctime + (long)(Math.random() * 10 + 1));
        String c = "ebSeFb%=XZ%T[KZ)c(sy!";

        String sign = util.md5(u + d + f + c);

        Map<String, String> params = new HashMap<String, String>();
        params.put("i", q);
        params.put("from", from);
        params.put("to", to);
        params.put("smartresult", "dict");
        params.put("client", "fanyideskweb");
        params.put("salt", f);
        params.put("sign", sign);
        params.put("doctype", "json");
        params.put("version", "2.1");
        params.put("keyfrom", "fanyi.web");
        params.put("action", "FY_BY_CLICKBUTTION");
        params.put("typoResult", "false");

        CloseableHttpClient httpClient = HttpClients.createDefault();
        HttpPost request = new HttpPost(util.getUrlWithQueryString(url, params));

//        request.setHeader("Accept","application/json, text/javascript, */*; q=0.01");
//        request.setHeader("Accept-Encoding","gzip, deflate");
//        request.setHeader("Accept-Language","zh-CN,zh;q=0.9");
//        request.setHeader("Connection","keep-alive");
//        request.setHeader("Content-Type","application/x-www-form-urlencoded; charset=UTF-8");
        request.setHeader("Cookie","OUTFOX_SEARCH_USER_ID_NCOO=1537643834.9570553; OUTFOX_SEARCH_USER_ID=1799185238@10.169.0.83; fanyi-ad-id=43155; fanyi-ad-closed=1; JSESSIONID=aaaBwRanNsqoobhgvaHmw; _ntes_nnid=07e771bc10603d984c2dc8045a293d30,1525267244050; ___rl__test__cookies=" + String.valueOf(ctime));
//        request.setHeader("Host","fanyi.youdao.com");
//        request.setHeader("Origin","http://fanyi.youdao.com");
        request.setHeader("Referer","http://fanyi.youdao.com/");
        request.setHeader("User-Agent","Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36");
//        request.setHeader("X-Requested-With","XMLHttpRequest");

        CloseableHttpResponse httpResponse = httpClient.execute(request);
        HttpEntity httpEntity = httpResponse.getEntity();
        String result = EntityUtils.toString(httpEntity, "UTF-8");
        EntityUtils.consume(httpEntity);    // 关闭
        httpResponse.close();

        String res[] = result.split("\"");
        StringBuilder resd = new StringBuilder();
        for (int i = 0; i < res.length; i++) {
            if (res[i].equals("tgt")) {
                resd.append(res[i + 2]);
            }
        }
        System.out.println(resd.toString());
    }
其中，md5() 和 getUrlWithQueryString() 可以利用 JAVA DEMO 提供的方法。

https://blog.csdn.net/hujingshuang/article/details/80177784
