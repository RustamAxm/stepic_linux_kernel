# study log
## Make node
```
rustam@rustam-ZenBook:~/stepic_linux_kernel/file_operation$ sudo mknod /dev/chrdev c 700 0
rustam@rustam-ZenBook:~/stepic_linux_kernel/file_operation$ sudo chmod a+rw /dev/chrdev 
rustam@rustam-ZenBook:~/stepic_linux_kernel/file_operation$ ls -la /dev/chrdev 
crw-rw-rw- 1 root root 700, 0 мар 25 13:42 /dev/chrdev
rustam@rustam-ZenBook:~/stepic_linux_kernel/file_operation$ sudo rmmod chrdev 
rustam@rustam-ZenBook:~/stepic_linux_kernel/file_operation$ sudo insmod chrdev.ko
rustam@rustam-ZenBook:~/stepic_linux_kernel/file_operation$ echo "w" > /dev/chrdev 
rustam@rustam-ZenBook:~/stepic_linux_kernel/file_operation$ echo "w" > /dev/chrdev 
rustam@rustam-ZenBook:~/stepic_linux_kernel/file_operation$ sudo rmmod chrdev 
```

## journalctl -f
```
мар 25 13:43:50 rustam-ZenBook kernel: 
                                           Hello, loading 
мар 25 13:43:50 rustam-ZenBook kernel: CHRDEV "mychrdev" major requested (700) is greater than the maximum (511)
мар 25 13:44:39 rustam-ZenBook kernel: 
                                           OPENING DEVICE mychrdev 
                                          
                                           
мар 25 13:44:39 rustam-ZenBook kernel: COUNTER = 1
мар 25 13:44:39 rustam-ZenBook kernel: module refcounter = 1 
мар 25 13:44:39 rustam-ZenBook kernel: 
                                           WRITE mychrdev nbytes = 2 ppos = 2 
мар 25 13:44:39 rustam-ZenBook kernel: 
                                           RELAESE dev mychrdev 
мар 25 13:44:52 rustam-ZenBook kernel: 
                                           OPENING DEVICE mychrdev 
                                          
                                           
мар 25 13:44:52 rustam-ZenBook kernel: COUNTER = 2
мар 25 13:44:52 rustam-ZenBook kernel: module refcounter = 1 
мар 25 13:44:52 rustam-ZenBook kernel: 
                                           WRITE mychrdev nbytes = 2 ppos = 2 
мар 25 13:44:52 rustam-ZenBook kernel: 
                                           RELAESE dev mychrdev 
мар 25 13:46:10 rustam-ZenBook sudo[8437]:   rustam : TTY=pts/1 ; PWD=/home/rustam/stepic_linux_kernel/file_operation ; USER=root ; COMMAND=/usr/sbin/rmmod chrdev
мар 25 13:46:10 rustam-ZenBook sudo[8437]: pam_unix(sudo:session): session opened for user root by (uid=0)
мар 25 13:46:10 rustam-ZenBook kernel: 
                                           Leaving
мар 25 13:46:10 rustam-ZenBook sudo[8437]: pam_unix(sudo:session): session closed for user root


```
