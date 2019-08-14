For connection between machines without public ip address, but have access to internet.

A(no public ip address) -> B(public ip address) <- C(no public ip address)

A <---ssh reverse proxy---> C

## Usage
First, run
```
./ssh_nopasswd B_user@B_ip_address
```
Then:

For A, run this cmd:
```
./ssh_open_remote_port B_user@B_ip_address
```
then B opens a new public ssh port, default 9999;

sshd service of A must be open at the default 22 port;

or you need change environment variable as follows:
```
LOCAL_PORT=22 REMOTE_PORT=9999 ./ssh_open_remote_port B_user@B_ip_address
```
this script use -R and -N option of ssh binary, other ssh options are supported.

Now for C, use this cmd to login A:
```
ssh -p 9999 A_user@B_ip_address
```

## Keep alive
```
./ssh_open_remote_port_keep_alive B_user@B_ip_address
```
this script use cron service to keep alive.

also support LOCAL_PORT and REMOTE_PORT.


Ref:
* https://www.howtoforge.com/reverse-ssh-tunneling
* https://superuser.com/questions/588591/how-to-make-ssh-tunnel-open-to-public
