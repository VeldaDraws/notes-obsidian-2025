1. AWS CLI Basics
2. Linux Refresher (Cloud9)
3. EC2, EFS Lab Notes (Linux Instance)

## AWS CLI Basics
```bash
aws --version     # check if installed correctly
```
## Linux Refresher (Cloud9)
```bash
cat /proc/version
```
Output example: `Linux version 5.10.234-225.921.amzn2.x86_64 ... ... ...`
##### Yum package install example
```bash
sudo yum -y install httpd php-mbstring
```
Output:
```
Installed size: 2.8 M
Downloading packages:
(1/2): oniguruma-5.9.6-1.amzn2.0.7.x86_64.rpm                                      | 127 kB  00:00:00     
(2/2): php-mbstring-8.2.28-1.amzn2.0.1.x86_64.rpm    ..........
```
##### Apache Server / `httpd`
```bash
sudo httpd -v
```
- Server version
- Server built
```bash
service httpd status
```
Output:
```
Redirecting to /bin/systemctl status httpd.service
● httpd.service - The Apache HTTP Server ....
```

```bash
php --version
```
##### Starting web server and database example
```bash
sudo chkconfig httpd on

sudo service httpd start

sudo service httpd status

### install database (MariaDB)

sudo yum install -y mariadb-server

sudo mariadb --version

sudo systemctl enable mariadb

### start database and check status

sudo chkconfig mariadb on

sudo service mariadb start

sudo service mariadb status

### Allow editing of web server files:
ln -s /var/www/ /home/ec2-user/environment

sudo chown ec2-user:ec2-user /var/www/html
```
## EC2, EFS Lab (Linux Instance)
#### (Inside Linux-Based EFS Instance SSH session)
See also: [Connect to your Linux instance using SSH](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-to-linux-instance.html)
```bash
sudo mkdir efs
```
- In the EFS console, choose Attach to open Amazon EC2 mount instructions.
- Copy entire command in "Using the NFS client" section
	- Looks something like `sudo mount -t nfs4 -o ... ...`
##### Get a full summary of available/used disk space
```bash
sudo df -hT
```
- `df -hT`
	- Helps to verify that the file system is mounted
	- [Full `df` syntax on man7.org](https://www.man7.org/linux/man-pages/man1/df.1.html)
	- [GNU documentation](https://www.gnu.org/software/coreutils/manual/html_node/df-invocation.html#df-invocation)
	- `-h` allows human readability. Size will show succinctly.
	- `-T` shows file system type. (`ext4`, `nfs4`, etc.)