<?php
$text=$_GET["text"];

//$text = "hello world";

$now = time();
$noww = $now + rand(1, 10);
$a = "fanyideskweb";
$b = "ebSeFb%=XZ%T[KZ)c(sy!";
$sign = md5($a.$text.$noww.$b);
$url = 'http://fanyi.youdao.com/translate?smartresult=dict&smartresult=rule';
$header = array('token:JxRaZezavm3HXM3d9pWnYiqqQC1SJbsU','language:zh','region:GZ');
$content = array(
    "action" => "FY_BY_REALTIME",
	"client" => "fanyideskweb",
	"doctype" => "json",
	"from	" => "AUTO",
	"i" =>$text,
	"keyfrom" => "fanyi.web",
	"salt" =>$noww,
	"sign" =>$sign ,
	"smartresult" => "dict",
	"to" => "AUTO",
	"typoResult" => "false",
	"version" => "2.1"
);
$response = tocurl($url, $header, $content);
$data = json_decode($response, true);
echo $data['translateResult'][0][0]['tgt'];
/**
 * 发送数据
 * @param String $url   请求的地址
 * @param Array $header 自定义的header数据
 * @param Array $content POST的数据
 * @return String
 */
function tocurl($url, $header, $content){
  $ch = curl_init();
  if(substr($url,0,5)=='https'){
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false); // 跳过证书检查
    curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, true); // 从证书中检查SSL加密算法是否存在
  }
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
  curl_setopt($ch, CURLOPT_URL, $url);
  curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
  curl_setopt($ch, CURLOPT_POST, true);
  curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($content));
  $response = curl_exec($ch);
  if($error=curl_error($ch)){
    die($error);
  }
  curl_close($ch);
  return $response;
}
?>
