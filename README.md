# CCMTV
some docs
CCMTV手机端支付
=====================================
> author: jay

支付宝
--------
#### 第三方浏手机览器中 
```php
header("Content-type: text/html; charset=utf-8");
function visitAlipay($uri,$data){
        $ch = curl_init ();
        curl_setopt ( $ch, CURLOPT_URL, $uri );
        curl_setopt ( $ch, CURLOPT_POST, 1 );
        curl_setopt ( $ch, CURLOPT_HEADER, 0 );
        curl_setopt ( $ch, CURLOPT_RETURNTRANSFER, 1 );
        curl_setopt ( $ch, CURLOPT_POSTFIELDS, $data );
        $return = curl_exec ( $ch );
        curl_close ( $ch );
        return $return;
    }  

$str = visitAlipay("http://www.ccmtv.cn/inc/alipay_mobile/wappay/ccmtvAlipay.php",[
    'out_trade_no'=>$out_trade_no,//$info['ordernum'],
    'subject'=>$payparams->aboutstr,
    'total_amount'=>$order_message['money'],
    'body'=>$payparams->aboutstr,
    'notify_url'=>'http://shgme.ccmtv.cn/do/notify_url.php',//验证方法
	'return_url'=>'http://shgme.ccmtv.cn',//支付成功返回的路径
    ]);
echo $str;
exit;
```
####  微信内不能调起支付宝 需提示用户前去浏览器内调起
```php
if (strpos($_SERVER['HTTP_USER_AGENT'], 'MicroMessenger') !== false ) {
//微信浏览器
#当前完整浏览器地址
$url = 'http://'.$_SERVER['HTTP_HOST'].$_SERVER['PHP_SELF'].'?'.$_SERVER['QUERY_STRING'];
$html = "<h1 style='margin:200px auto;font-size:36px;text-align:center;width:60%'>微信暂不支持支付，请点击右上角选择其它浏览器打开或复制链接到其它浏览器</h1>";
echo $html;
}
```


微信
------------------

#### 微信内支付 （公众号支付）

```php
header("Content-type: text/html; charset=utf-8");
require('./ccmtvWxinpay.php');//服务器物理地址 /alidata/www/default/upload_files/2017_upload_files/jay/Wxpay/example/ccmtvWxinpay.php
$data = [
        'Out_trade_no'=>time(),
        'Attach'=>'Attach',
        'Total_fee'=>'0.01',
        'Body'=>'body', 
        'Goods_tag'=>'Goods_tag',
        'Notify_url'=>'http://www.ccmtv.cn/upload_files/2017_upload_files/jay/Wxpay/example/notify.php',
    ];
new \CCMTV\CCMTVWxinpay($data);
```
#### 第三方浏览器唤醒微信支付（H5支付）
```php
 待封装
```
