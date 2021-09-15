# PeCan CTF

## Shadow - Advanced Forensics

### Overview

### 


## PHP Circus - Advanced Web Explotation

### TL;DR

In the soure code, it checks if the md5 hash of the password is equal to "0". PHP has some problems in it's md5 hashing algorithm, thus causing the hash "0e462097431906509019562988736854" to equal "0". If you look up "php magic md5" you will find multiple hashes. If we enter "240610708" we get the flag `PeCaN{^&^Sh0ulD-HaV3_B33n-===\_n0T==}`
