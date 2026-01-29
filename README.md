
$ch = curl_init("http://169.254.169.254/latest/api/token");

curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "PUT");

curl_setopt($ch, CURLOPT_HTTPHEADER, ["X-aws-ec2-metadata-token-ttl-seconds: 21600"]);

$token = curl_exec($ch);

curl_close($ch);



$ch = curl_init("http://169.254.169.254/latest/dynamic/instance-identity/document");

curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

curl_setopt($ch, CURLOPT_HTTPHEADER, ["X-aws-ec2-metadata-token: $token"]);

$json = curl_exec($ch);

curl_close($ch);



$d = json_decode($json, true);



echo "Hostname: " . gethostname() . "<br>";

echo "AZ: " . $d['availabilityZone'];

