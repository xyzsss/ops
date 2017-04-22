# env: bash
# 2017-04-21 23:54:46

# [Need the part first] (https://raw.githubusercontent.com/xyzsss/Notes/realmaster/services/SSH_withkey_login)
# ssh port reset
# redirect defaut port 22 to 2345 by iptables



# twisted install
wget https://pypi.python.org/packages/5f/14/41881d2f8a4afefed7ad80c9ecdc0501054f5f981fb43326b20057fb772c/Twisted-14.0.1.tar.bz2#md5=742a97879d63c341b398bc909bbdcdab 
bzip2 -d Twisted-14.0.1.tar.bz2
tar xvf Twisted-14.0.1.tar
cd Twisted-14.0.1
python setup.py install
cd ..
rm -rf Twisted-14.0.1*

# pycrypto install
yum  install python-crypto zip unzip -y 

useradd -m kippo
wget https://github.com/desaster/kippo/archive/master.zip
unzip master.zip
mv kippo-* /home/kippo/
chown kippo.kippo /home/kippo/ -Rf

su - kippo
mv kippo-*  kippo
cd kippo
cp kippo.cfg.dist kippo.cfg

sed -ie 's/ssh_port = 2222/ssh_port = 2345/' kippo.cfg
sed -ie 's/ssh_version_string.*/ssh_version_string = SSH-2.0-OpenSSH_5.9/' kippo.cfg
cat kippo.cfg |grep 'ssh_port'
cat kippo.cfg |grep 'ssh_version_string'
cd data
echo "root:#$%^&*FGHJ"  > userdb.txt
./start.sh

exit