# PeCan CTF

## Shadow - Advanced Forensics

### Overview

### 


## PHP Circus - Advanced Web Explotation

### TL;DR

In the soure code, it checks if the md5 hash of the password is equal to "0". PHP has some problems in it's md5 hashing algorithm, thus causing the hash "0e462097431906509019562988736854" to equal "0". If you look up "php magic md5" you will find multiple hashes. If we enter "240610708" we get the flag `PeCaN{^&^Sh0ulD-HaV3_B33n-===\_n0T==}`

### What did I do?
 - When I first looked at the challenge, the first thing that I always do for webex is press Ctrl+U to view the source, this revealed nothing and I noticed there was a "See the source code" link.
 - In the source code:
```php
<?php
 require ("flagtoMD5.php");
 require("flag.php");
  
  //View PHP source code
  if (isset($_GET['source'])) {
    highlight_file(__FILE__);
    die();
  }

  //Match MD5
  if (isset($_GET['password']))
  {
    if (hash("md5", $_GET['password']) == "0")
    {
        getFlag();
    }
    else
    {
        echo "Sorry that is incorrect";
    }
  }  

?>
```
 - We can see that it gets the password parameter from the url, hashes it with md5 and checks if it is equal to "0"
 - If it equals "0" then it prints the flag, otherwise it will echo "Sorry that is incorrect"
 - I had already heard about the php magic hashes before but just for this writeup I looked up "php md5 hash 0" and it came up with [this](https://www.whitehatsec.com/blog/magic-hashes/) resource
 - It shows the hash that equals "0" and you will need to paste that into the password box to win!
