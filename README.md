$token = trim(shell_exec('curl -s -X PUT http://169.254.169.254/latest/api/token -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"'));
$az    = trim(shell_exec('curl -s -H "X-aws-ec2-metadata-token: ' . $token . '" http://169.254.169.254/latest/meta-data/placement/availability-zone'));

echo "Hostname: " . htmlspecialchars(gethostname()) . "<br>";
echo "AZ: " . htmlspecialchars($az ?: '-') . "<br>";
