~~~
<?php

//https://mxsky.cn/index.php/2018/168.html

function TKK()   
{
    $a = 1394951105;  
    $b = 1526272306;  
    return 320305 . '.' . ($b - $a);  
} 

function RL($a, $b)  
{	
	for($c = 0; $c < strlen($b) - 2; $c +=3) {  
        $d = $b{$c+2};  
        $d = $d >= 'a' ? charCodeAt($d,0) - 87 : intval($d);  
        $d = $b{$c+1} == '+' ? shr32($a, $d) : $a << $d;  
        $a = $b{$c} == '+' ? ($a + $d & 4294967295) : $a ^ $d;  
	}  
	return $a;  
} 

function charCodeAt($str, $index)
{
    $char = mb_substr($str, $index, 1, 'UTF-8');  

    if (mb_check_encoding($char, 'UTF-8'))  
    {  
        $ret = mb_convert_encoding($char, 'UTF-32BE', 'UTF-8');  
        return hexdec(bin2hex($ret));  
    }  
    else  
    {  
        return null;  
    }  
}

function shr32($x, $bits)
{	
    if($bits <= 0){  
        return $x;  
    }  
    if($bits >= 32){  
        return 0;  
    }  

    $bin = decbin($x);  
    $l = strlen($bin);  

    if($l > 32){  
        $bin = substr($bin, $l - 32, 32);  
    }elseif($l < 32){  
        $bin = str_pad($bin, 32, '0', STR_PAD_LEFT);  
    }  
	
    return bindec(str_pad(substr($bin, 0, 32 - $bits), 32, '0', STR_PAD_LEFT));  
}


function sign($str){
    $str = str_replace(array("/r/n", "/r", "/n"), "", $str);
    $slen = mb_strlen($str,'utf-8');//获取中文长度
    if($slen > 30) {
    $n= floor($slen/2)-5;
    $str = "".mb_substr($str,0,10,'utf-8').mb_substr($str,$n,10,'utf-8').mb_substr($str,-10,10,'utf-8');
    }
    $tkk = explode('.', TKK());

    $h = $tkk[0]; 
    $i = $tkk[1];

    for($d = array(), $e = 0, $f = 0; $f <$slen; $f++) {
    $g= charCodeAt($str,$f);
    if (128 > $g) {

            $d [$e++] = $g;  
        } else {  
            if (2048 > $g) {  
                $d [$e++] = $g >> 6 | 192;  
            } else {  
                if (55296 == ($g & 64512) && $f + 1 < mb_strlen ( $str, 'UTF-8' ) && 56320 == (charCodeAt ( $str, $f+1 ) & 64512)) {  
                    $g = 65536 + (($g & 1023) << 10) + (charCodeAt ( $str, ++$f ) & 1023);  
                    $d [$e++] = $g >> 18 | 240;  
                    $d [$e++] = $g >> 12 & 63 | 128;  
                } else {  
                    $d [$e++] = $g >> 12 | 224;  
                    $d [$e++] = $g >> 6 & 63 | 128;  
                }  
            }  
            $d [$e++] = $g & 63 | 128;  
        } 

    }
    $s = $h;
    for($ss=0;$ss<count ( $d );$ss++){
    $s+=$d[$ss];
    $s= RL($s,"+-a^+6");
    }
    $s = RL ($s,"+-3^+b+-f" );
    $s ^= $i;
    if (0 > $s) {

        $s = ($s & 2147483647) + 2147483648;  
    }  

    $s = fmod ( $s, pow ( 10, 6 ) );
    return $s . "." . ($s ^ $h);
}
/*
function huoqu(){
    $cookie_file = dirname(__FILE__).'/bdcookie.txt';
    $url = "http://fanyi.baidu.com/#zh/en/%E4%BD%A0%E5%A5%BD";
    $ch = curl_init();
	
     curl_setopt($ch, CURLOPT_URL, $url); 
     curl_setopt($ch, CURLOPT_HEADER, 1); 
     $header = array("Host:fanyi.baidu.com",
        'Content-Type:application/x-www-form-urlencoded; charset=UTF-8',
        'Cookie:C1A439E6479360E8903C9AD7A36A3134',//需要填写cookie
        'Referer:http://fanyi.baidu.com/',
      'User-Agent:Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36');
     curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); //如果把这行注释掉的话，就会直接输出 
     curl_setopt($ch,CURLOPT_HTTPHEADER,$header);
     curl_setopt($ch, CURLOPT_COOKIEJAR,  $cookie_file); //存储cookies
     $result=curl_exec($ch); 
     curl_close($ch); 
	 
     preg_match_all("%token: '(.*?)'%", $result, $matches);
    //preg_match("%token: '(.*?)'%", $result,$token);
	var_dump($token);
    return $token[1];
}
*/


//参数1：访问的URL，参数2：post数据(不填则为GET)，参数3：提交的$cookies,参数4：是否返回$cookies
function curl_request($url,$post='',$cookie='', $returnCookie=0){

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
    if($cookie) {
        curl_setopt($curl, CURLOPT_COOKIE, $cookie);
    }
    curl_setopt($curl, CURLOPT_HEADER, $returnCookie);
    curl_setopt($curl, CURLOPT_TIMEOUT, 10);
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
    $data = curl_exec($curl);
	echo $data;
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

function request_url_data($str,$f,$t)
{
	
	$gtk = TKK();
	
	echo $str . "_" . $gtk;
	//return;
	
	echo sign($str);
	//return;
	
	//return;
	$token = "2bb598d37401bc29b489de1d4a32a72f";
    
	$sign = "288018.34339";
	
	
    $url = "http://fanyi.baidu.com/v2transapi";
    $post_data =array();
    $post_data['query']=$str;
    $post_data['sign']=$sign;
    $post_data['from']=$f;
    $post_data['to']=$t;
    $post_data['simple_means_flag']=3;
    $post_data['token']=$token;
	$post_data['transtype']="realtime";
	
    $header = array("Host:fanyi.baidu.com",

        'Content-Type:application/x-www-form-urlencoded; charset=UTF-8',
        'Cookie:BAIDUID=6ACA16DE0551132BDA0AD7C868BA2875:FG=1; __guid=37525047.3425545495696378400.1520760922495.3843; REALTIME_TRANS_SWITCH=1; FANYI_WORD_SWITCH=1; HISTORY_SWITCH=1; SOUND_SPD_SWITCH=1; SOUND_PREFER_SWITCH=1; BIDUPSID=6ACA16DE0551132BDA0AD7C868BA2875; PSTM=1520761193; BDUSS=lVub25vazk5S2taTGphZXE0UVowc2hqSDBqUUZ0OWpUdnFMV3FVa3NHSWhuTTlhQUFBQUFBJCQAAAAAAAAAAAEAAACm1h8SwdMxMjMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACEPqFohD6had; BDRCVFR[feWj1Vr5u3D]=I67x6TjHwwYf0; PSINO=7; H_PS_PSSID=1446_21118_18559_17001; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; locale=zh; monitor_count=8; Hm_lvt_64ecd82404c51e03dc91cb9e8c025574=1520856590,1520863193,1520944633,1521003596; Hm_lpvt_64ecd82404c51e03dc91cb9e8c025574=1521003596;',
        'Referer:http://fanyi.baidu.com/',
      'User-Agent:Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36');

    $cookie = "PSTM=1551316669; BDUSS=wzRlVaLXRwSjRGOG50eHdNRS1uRjdGNmRSflJocy05N3lIdnQtUkVNSERDNTljQVFBQUFBJCQAAAAAAAAAAAEAAABCKuMhZGFpamlubWluZ2NuAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMN-d1zDfndcNG; BAIDUID=C1A439E6479360E8903C9AD7A36A3134:FG=1; REALTIME_TRANS_SWITCH=1; FANYI_WORD_SWITCH=1; HISTORY_SWITCH=1; SOUND_SPD_SWITCH=1; SOUND_PREFER_SWITCH=1; BIDUPSID=270717646B9BBDC5B496E8BA0BAFE6BE; to_lang_often=%5B%7B%22value%22%3A%22en%22%2C%22text%22%3A%22%u82F1%u8BED%22%7D%2C%7B%22value%22%3A%22zh%22%2C%22text%22%3A%22%u4E2D%u6587%22%7D%5D; from_lang_often=%5B%7B%22value%22%3A%22zh%22%2C%22text%22%3A%22%u4E2D%u6587%22%7D%2C%7B%22value%22%3A%22en%22%2C%22text%22%3A%22%u82F1%u8BED%22%7D%5D; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; Hm_lvt_64ecd82404c51e03dc91cb9e8c025574=1553241878,1553243136,1553246877,1553479518; H_PS_PSSID=1437_21114_20697_28723_28557_28697_28585_26350_28605; delPer=0; PSINO=2; locale=zh; Hm_lpvt_64ecd82404c51e03dc91cb9e8c025574=1553484487"; //注意填写cookie
     
    $result = curl_request($url,$post_data,$cookie,1);
	var_dump($result);
    $s = $result["content"];
    $s =json_decode($s);
	echo $s->error;
	
    
    if($s->error=="997" or !empty($s->error)){
		echo  "对不起cookie过期！";
    }
    echo  $s->trans_result->data[0]->dst;
}

$str = "hello world";
$fL = "en";
$tL = "zh";
//hello world_320305.131321201

request_url_data($str,$fL,$tL);



?>
~~~
