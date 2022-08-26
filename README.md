# VNCDecrypt
Decrypt passwords stored in VNC files

VNC stores passwords as a hex string in `.vnc` files using a default encryption key.  The following openssl one-liner can be used to decrypt the string:

Assume the string from the .vnc file is `d7a514d8c556aade`

`echo -n d7a514d8c556aade | xxd -r -p | openssl enc -des-cbc --nopad --nosalt -K e84ad660c4721ae0 -iv 0000000000000000 -d -provider legacy -provider default | hexdump -Cv`

The output will look like this:

```
00000000  53 65 63 75 72 65 21 00                           |Secure!.|
00000008
```

Reference

https://miloserdov.org/?p=4854#6
