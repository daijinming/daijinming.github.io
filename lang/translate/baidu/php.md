<?php
//参数1：访问的URL，参数2：post数据(不填则为GET)，参数3：提交的$cookies,参数4：是否返回$cookies
function curl_request($url,$post='',$header,$cookie='', $returnCookie=0){

    $curl = curl_init();
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_USERAGENT, 'Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.1; Trident/6.0)');
    curl_setopt($curl, CURLOPT_FOLLOWLOCATION, 1);
    curl_setopt($curl, CURLOPT_AUTOREFERER, 1);
    curl_setopt($curl, CURLOPT_REFERER, "http://fanyi.baidu.com");
	curl_setopt($curl,CURLOPT_SSL_VERIFYPEER,FALSE);
    if($post) {
        curl_setopt($curl, CURLOPT_POST, 1);
        curl_setopt($curl, CURLOPT_POSTFIELDS, http_build_query($post));
    }
	
	if($header)
	{
		curl_setopt($curl,CURLOPT_HTTPHEADER,$header);
	}
	
    if($cookie) {
        curl_setopt($curl, CURLOPT_COOKIE, $cookie);
    }
	
    curl_setopt($curl, CURLOPT_HEADER, $returnCookie);
    curl_setopt($curl, CURLOPT_TIMEOUT, 10);
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
    $data = curl_exec($curl);
	//echo $data;
    if (curl_errno($curl)) {
        return curl_error($curl);
    }
    curl_close($curl);
    if($returnCookie){
        list($header, $body) = explode("\r\n\r\n", $data, 2);
        preg_match_all("/Set\-Cookie:([^;]*);/", $header, $matches);
        $info['cookie']  = substr($matches[1][0], 1);
        $info['content'] = $body;
        return $info;
    }else{
        return $data;
    }
}

##浏览器中获得的头信息
$header = array(
	"Cookie: PSTM=1551316669; BDUSS=wzRlVaLXRwSjRGOG50eHdNRS1uRjdGNmRSflJocy05N3lIdnQtUkVNSERDNTljQVFBQUFBJCQAAAAAAAAAAAEAAABCKuMhZGFpamlubWluZ2NuAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMN-d1zDfndcNG; BAIDUID=C1A439E6479360E8903C9AD7A36A3134:FG=1; REALTIME_TRANS_SWITCH=1; FANYI_WORD_SWITCH=1; HISTORY_SWITCH=1; SOUND_SPD_SWITCH=1; SOUND_PREFER_SWITCH=1; BIDUPSID=270717646B9BBDC5B496E8BA0BAFE6BE; to_lang_often=%5B%7B%22value%22%3A%22en%22%2C%22text%22%3A%22%u82F1%u8BED%22%7D%2C%7B%22value%22%3A%22zh%22%2C%22text%22%3A%22%u4E2D%u6587%22%7D%5D; from_lang_often=%5B%7B%22value%22%3A%22zh%22%2C%22text%22%3A%22%u4E2D%u6587%22%7D%2C%7B%22value%22%3A%22en%22%2C%22text%22%3A%22%u82F1%u8BED%22%7D%5D; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; BDRCVFR[feWj1Vr5u3D]=I67x6TjHwwYf0; PSINO=7; delPer=0; locale=zh; Hm_lvt_64ecd82404c51e03dc91cb9e8c025574=1553243136,1553246877,1553479518,1553491544; H_PS_PSSID=1437_21114_28723_28557_28697_28585_26350_28605; Hm_lpvt_64ecd82404c51e03dc91cb9e8c025574=1553491657",
	"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.108 Safari/537.36"
);


$html = curl_request("http://fanyi.baidu.com",null,$header,null);

$token = "";

preg_match("%token: '(.*?)'%", $html,$token);

echo $token[0];

$gtk = "";
preg_match("%window.gtk = '(.*?)';%", $html,$gtk);

echo $gtk[0];

##参考 python版本:百度翻译接口实例解析
https://blog.csdn.net/hongquan1991/article/details/80616491





?>
