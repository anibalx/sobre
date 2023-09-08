```
  cat /etc/os-release
  grep '^NAME' /etc/os-release
  grep '^NAME' /etc/os-release | sed -r 's/NAME="(.*)"/\1/g'
```


```
  lsb_release -a
```


```
  hostnamectl
```
