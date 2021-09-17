# OverTheWire - Bandit

## Bandit14

`The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on`

### Commands used
 - ls
 - ssh
 - cat 

### Description

There is a file inside the home directory of bandit13 called `sshkey.private`. When we cat out the file we get:
```bash
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```
This file is an SSH private key. It is used to sign into a remote machine securely without having to use a password. Using this way is also inherently more secure because no-one would be able to social engineer you to get you to tell them your private key as it is impossible to remember (for most people). 

If we look at the man page for ssh (`man ssh`) and look for "private key" parameters by typing `/private key` it highlights the `-i identity_file` parameter. Now we can type
```bash
ssh -i sshkey.private bandit14@localhost
```
Once we are in we can use `cat` to print out the password for bandit 14 as all passwords are stored in `/etc/bandit_pass/banditNumber`
```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

## Bandit15

`The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.`

### Commands used
 - nc

### Description

The challenge description tells us that there is a service running on the current machine on port 30000. There are lots of tools we can use to interact with this network service including `telnet`, `nc` and `curl`. `telnet` and `nc` will work fine for this but I am going to show `nc` as it is more versatile than telnet.

If we look at the man page for `nc` we can see the basic usage of it:

```bash
NAME
       nc - TCP/IP swiss army knife

SYNOPSIS
       nc [-options] hostname port[s] [ports] ...
       nc -l -p port [-options] [hostname] [port]
```

This shows us how we can connect to the service on port 30000:
```bash
nc localhost 30000
```

Once we are on, there is no response until we submit the password for bandit14:

```bash
bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

And we get the password for bandit15

## Bandit16

`The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…`

### Commands used
 - openssl

This challenge tells us that there is a service running on port 30001 using SSL encryption! If we try the same command from last time:
```bash
bandit15@bandit:~$ nc localhost 30001
Helo!
```
The server does not respond. However, this is because `nc` is unencrypted! In order to interact with the service we have to use `openssl`. If we look at the man page for `openssl` it shows us that we need to specify a command to use to connect to the service:

```bash
NAME
       openssl - OpenSSL command line tool

SYNOPSIS
       openssl command [ command_opts ] [ command_args ]

       openssl list [ standard-commands | digest-commands | cipher-commands | cipher-algorithms | digest-algorithms | public-key-algorithms]

       openssl no-XXX [ arbitrary options ]
```

Looking at the list of commands show us that there is a command called `s_client` which has a `-connect` argument. We can use this to connect to the service:
```bash
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIEHxhZ+zANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwODA1MjEyMjEzWhcNMjIwODA1MjEyMjEzWjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBALqNmx6R
csRsPgzRcRsq5oQ4BC9AT/Yu473WbK4SRjHOWwuA4Oqk9w8SLKYZ39FrDEnXSZJw
xqKPR0AH72+l7Itv7X1H07VbeMTQoJVm6NsJm3cuyyxjRwfaIOUFsRtQQyvQlmw7
3CgTbd3wEk1CD+6jlksJj801Vd0uvZh1VVERAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBADjhbe3bTnDWsS4xt8FFg7PJIqNAxF6QjP+7xzJ4yMvWtPP6tVXo
F7SNI52juwH0nFDyM9KOrM/AknWqCYF+yfz6bLD7MaKZ+Kg3DiLaoVJOrVg6Y02+
0vq1rLsqGko5wamCFamx7X9CtFsV0WQjZdA53Na/VwehtlFpf/p20VAi
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: 6F863258C8F181D099E0F3CA63CB153D8B311831985FE278E8FD7F998E391469
    Session-ID-ctx:
    Master-Key: C294296D45472F770AB1E1C704BCD142FEE4B23BCBD732D659725AC54026E5866A842E20841F2A1A307B9F41AFBF1B41
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 3a a9 fe 3b 12 a1 ed 2b-8d a6 cf aa 23 c9 12 88   :..;...+....#...
    0010 - f3 58 60 69 3f 8d 76 f4-c5 e4 3c 3a df 2b bf ce   .X`i?.v...<:.+..
    0020 - 4d f6 ab 32 92 8d 0d b4-14 e4 97 5d ac f7 33 42   M..2.......]..3B
    0030 - 17 a4 3c ad b4 6d 4e fe-b2 17 0e 35 2f ef e8 38   ..<..mN....5/..8
    0040 - 60 f9 a1 53 33 f8 18 b2-9d 8e 2c 2a db 7f 42 7a   `..S3.....,*..Bz
    0050 - 38 7f 6f ae fc a3 ce a1-41 04 25 61 3b bf 82 bd   8.o.....A.%a;...
    0060 - 55 96 51 f4 cc c4 d7 53-2c 7d 29 16 32 0e 86 93   U.Q....S,}).2...
    0070 - b9 8a 70 e8 d3 c7 9a b9-03 6f b3 f3 05 e9 ca ae   ..p......o......
    0080 - 9f 7c fc 68 4f 89 9e a2-be fc 31 2f bc 1f 3c 1d   .|.hO.....1/..<.
    0090 - b0 ad 4b dc 7e 8b f2 22-0e cd 65 35 d7 62 79 9a   ..K.~.."..e5.by.

    Start Time: 1631859573
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

closed
```
This gives us the password.
