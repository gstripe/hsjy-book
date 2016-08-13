# jdk安装

## 此处安装jdk-7u80-linux-x64.tar.gz

```
# root
su root
# Download and unzip the packaged version.
wget ftp://hsftp:hsftp@10.188.180.99/devtools/jdk/jdk-7u80-linux-x64.tar.gz
tar -zxvf jdk-7u80-linux-x64.tar.gz
# change owner jdk1.7.0_80
chown -R hsit.hsit jdk1.7.0_80

# hsit
cd ~
vi .bash_profile
# edit add
export JAVA_HOME=/opt/jdk1.7.0_80
export PATH=$JAVA_HOME/bin:$PATH

```