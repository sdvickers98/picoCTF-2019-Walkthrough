# Bases
100 points

# Description
*"What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases."*

# Solution
"Bases" is a hint that this string is [base64](https://en.wikipedia.org/wiki/Base64) encoded. We can solve this one from the command line:
```
$ echo bDNhcm5fdGgzX3IwcDM1 > temp.txt
$ base64 -d temp.txt
```

<details>
  <summary>Flag:</summary>
  picoCTF{l3arn_th3_r0p35}
</details>

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
