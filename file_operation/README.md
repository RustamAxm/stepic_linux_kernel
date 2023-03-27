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

### journalctl -f
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
## Make device in code impl
After insmod 
```
rustam@rustam-ZenBook:/dev$ ll | grep ch
drwxr-xr-x   2 root   root            4420 мар 27 22:46 char/
crw-------   1 root   root      254,     0 мар 27 22:17 gpiochip0
crw-------   1 root   root      500,     0 мар 27 22:46 my_chrdev
rustam@rustam-ZenBook:/dev$ sudo su 
[sudo] password for rustam: 
root@rustam-ZenBook:/dev# echo "w" > my_chrdev 
root@rustam-ZenBook:/dev# echo "w" > my_chrdev 
root@rustam-ZenBook:/dev# echo "w" > my_chrdev 
```
### journalctl -f
```
мар 27 22:46:28 rustam-ZenBook sudo[5753]:   rustam : TTY=pts/0 ; PWD=/home/rustam/stepic_linux_kernel/file_operation ; USER=root ; COMMAND=/usr/sbin/insmod chrdev.ko
мар 27 22:46:28 rustam-ZenBook kernel: 
                                           Hello, loading 
мар 27 22:46:28 rustam-ZenBook kernel: created device class mychrdev 
мар 27 22:46:28 rustam-ZenBook sudo[5753]: pam_unix(sudo:session): session opened for user root by (uid=0)
мар 27 22:46:28 rustam-ZenBook sudo[5753]: pam_unix(sudo:session): session closed for user root
мар 27 22:46:44 rustam-ZenBook systemd[1604]: Started VTE child process 5765 launched by gnome-terminal-server process 4558.
мар 27 22:46:57 rustam-ZenBook systemd[1604]: Started VTE child process 5773 launched by gnome-terminal-server process 4558.
мар 27 22:48:00 rustam-ZenBook sudo[5808]:   rustam : TTY=pts/2 ; PWD=/dev ; USER=root ; COMMAND=/usr/bin/su
мар 27 22:48:00 rustam-ZenBook sudo[5808]: pam_unix(sudo:session): session opened for user root by (uid=0)
мар 27 22:48:00 rustam-ZenBook su[5809]: (to root) rustam on pts/2
мар 27 22:48:00 rustam-ZenBook su[5809]: pam_unix(su:session): session opened for user root by (uid=0)
мар 27 22:48:20 rustam-ZenBook kernel: 
                                           OPENING DEVICE mychrdev 
                                          
                                           
мар 27 22:48:20 rustam-ZenBook kernel: COUNTER = 1
мар 27 22:48:20 rustam-ZenBook kernel: module refcounter = 1 
мар 27 22:48:20 rustam-ZenBook kernel: 
                                           WRITE mychrdev nbytes = 2 ppos = 2 
мар 27 22:48:20 rustam-ZenBook kernel: 
                                           RELAESE dev mychrdev 
мар 27 22:48:30 rustam-ZenBook kernel: 
                                           OPENING DEVICE mychrdev 
                                          
                                           
мар 27 22:48:30 rustam-ZenBook kernel: COUNTER = 2
мар 27 22:48:30 rustam-ZenBook kernel: module refcounter = 1 
мар 27 22:48:30 rustam-ZenBook kernel: 
                                           WRITE mychrdev nbytes = 2 ppos = 2 
мар 27 22:48:30 rustam-ZenBook kernel: 
                                           RELAESE dev mychrdev 
мар 27 22:48:31 rustam-ZenBook kernel: 
                                           OPENING DEVICE mychrdev 
                                          
                                           
мар 27 22:48:31 rustam-ZenBook kernel: COUNTER = 3
мар 27 22:48:31 rustam-ZenBook kernel: module refcounter = 1 
мар 27 22:48:31 rustam-ZenBook kernel: 
                                           WRITE mychrdev nbytes = 2 ppos = 2 
мар 27 22:48:31 rustam-ZenBook kernel: 
                                           RELAESE dev mychrdev 
мар 27 22:48:48 rustam-ZenBook su[5809]: pam_unix(su:session): session closed for user root
мар 27 22:48:48 rustam-ZenBook sudo[5808]: pam_unix(sudo:session): session closed for user root
мар 27 22:52:19 rustam-ZenBook sudo[5863]:   rustam : TTY=pts/0 ; PWD=/home/rustam/stepic_linux_kernel/file_operation ; USER=root ; COMMAND=/usr/sbin/rmmod chrdev
мар 27 22:52:19 rustam-ZenBook kernel: 
                                           Leaving

```

