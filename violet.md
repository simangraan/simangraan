<?php
error_reporting(1);
echo "Auto Login Wifi ID\n";
echo "Get Ip Dulu ...\n";
echo "[1] Windows\n";
echo "[2] Linux / Android\n";
echo "Kamu Pake apa ? : ";
$w = trim(fgets(STDIN));
if ( $w == 1) {
    echo shell_exec("ipconfig");
} else if($w == 2 ){
   echo shell_exec("ifconfig");
}else {
    echo "heuhhh... Ngetik yg bner euyy";
}
echo "\nCopy Ip mu ksni : ";
$myip = trim(fgets(STDIN));
echo "\nMasukin List Wifi ID mu : ";
$filenya = trim(fgets(STDIN));
$makan = file_get_contents("http://www.msftconnecttest.com/redirect");
$gw_id = preg_match_all('/gw_id=(.*?)&/', $makan, $hasilgw);
$mac = preg_match_all('/client_mac=(.*?)&/', $makan, $hasilmac);
$device = preg_match_all('/wlan=(.*?)&s/', $makan, $hasildevice);
echo $makan;
$gw = $hasilgw[1][0];
$macc = $hasilmac[1][0];
$devicee = $hasildevice[1][0];
echo "\nGett Info....\n";
sleep(3);
    $fn = fopen($filenya,"r");
 
    while(! feof($fn))  {
 
          $result = fgets($fn);
          $data = explode("|" , $result);
          $usernameku = $data[0];
          $passwordku = $data[1];
        // echo $usernameku." - ".$passwordku;
 
    $ch = curl_init();
    $headers = [
    'Content-Type: application/x-www-form-urlencoded; charset=utf-8',
    'Host: welcome2.wifi.id',
    'Referer: welcome2.wifi.id',
    'User-Agent: PostmanRuntime/7.20.1'
];
curl_setopt($ch, CURLOPT_URL,"https://welcome2.wifi.id/authnew/login/check_login.php?ipc=".$myip."&gw_id=".$gw."&mac=".$macc."&redirect=http://www.msftconnecttest.com/redirect&wlan=".$devicee."");
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_POSTFIELDS,
            'username='.$usernameku.'&password='.$passwordku);
 
// curl_setopt($ch, CURLOPT_POSTFIELDS,
//          http_build_query(array('postvar1' => 'value1')));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
 
$server_output = curl_exec($ch);
echo $server_output;
curl_close ($ch);
$hasil = json_decode($server_output);
if ($hasil->{"message"} == "LOGIN SUKSES") {
    echo "Get Akun......\n";
    sleep(3);
    echo "Sukses Login \n";
break;
} elseif ($hasil->{"message"} == "LOGIN DOUBLE DETECTED"){
    echo "Get Akun......\n";
    sleep(3);
    echo "Double Login \n";
} elseif ($hasil->{"message"} == "INVALID USERNAME dan PASSWORD"){
    echo "Get Akun......\n";
    sleep(3);
    echo "Gagal Login , Periksa Password \n";
} else {
    echo "Get Akun......\n";
    sleep(3);
    $hasil;
}
    }
    fclose($fn);
?>
