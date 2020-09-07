# john_pollard 
500 points

### Description
*"Sometimes RSA certificates are breakable"*

### Solution
The problem gives a file containing this:
```
-----BEGIN CERTIFICATE-----
MIIB6zCB1AICMDkwDQYJKoZIhvcNAQECBQAwEjEQMA4GA1UEAxMHUGljb0NURjAe
Fw0xOTA3MDgwNzIxMThaFw0xOTA2MjYxNzM0MzhaMGcxEDAOBgNVBAsTB1BpY29D
VEYxEDAOBgNVBAoTB1BpY29DVEYxEDAOBgNVBAcTB1BpY29DVEYxEDAOBgNVBAgT
B1BpY29DVEYxCzAJBgNVBAYTAlVTMRAwDgYDVQQDEwdQaWNvQ1RGMCIwDQYJKoZI
hvcNAQEBBQADEQAwDgIHEaTUUhKxfwIDAQABMA0GCSqGSIb3DQEBAgUAA4IBAQAH
al1hMsGeBb3rd/Oq+7uDguueopOvDC864hrpdGubgtjv/hrIsph7FtxM2B4rkkyA
eIV708y31HIplCLruxFdspqvfGvLsCynkYfsY70i6I/dOA6l4Qq/NdmkPDx7edqO
T/zK4jhnRafebqJucXFH8Ak+G6ASNRWhKfFZJTWj5CoyTMIutLU9lDiTXng3rDU1
BhXg04ei1jvAf0UrtpeOA6jUyeCLaKDFRbrOm35xI79r28yO8ng1UAzTRclvkORt
b8LMxw7e+vdIntBGqf7T25PLn/MycGPPvNXyIsTzvvY/MXXJHnAqpI5DlqwzbRHz
q16/S1WLvzg4PsElmv1f
-----END CERTIFICATE-----
```

This is a public RSA certificate. We can find *n* and *e* from this using python, but it might just be easier to use an
[online PEM parser](https://report-uri.com/home/pem_decoder). If we go to the bottom of the parsed data, we will find the
hex values for *n* and *e*. You can convert those to decimal with python or by going [here](https://www.rapidtables.com/convert/number/hex-to-decimal.html).
We get these values:
```python
n = 4966306421059967
e = 65537
```

This is a pretty small value of *n* to use for RSA encryption. If we use the [same website](https://www.alpertron.com.ar/ECM.HTM) from
the last walkthrough to factor *n*, we get:
```
p = 73176001
q = 67867967
```

This one has kind of a weird flag. It's just *p* and *q*, comma-separated with no spaces.
<details>
  <summary>Flag:</summary>
  picoCTF{73176001,67867967}
</details>

And that's the last cryptography problem in picoCTF! We got to work our way up from some pretty basic ciphers to some more complex encryption algorithms that are 
commonly used today. I really hope you've enjoyed these problems and that they've made you more interested in cryptography!

[Return to Cryptography](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
