# OK-polipo
One key for polipo
# Test Environment
```
4.5.5-300.fc24.x86_64
```
# Installation

```
sudo dnf install -y polipo

if [ -z "`grep '^#OK-polipo$' /etc/polipo/config`" ]; then

line_num="`sudo grep -n '# Uncomment this if you want to use a parent SOCKS proxy:' /etc/polipo/config | cut -d: -f1`"
echo $line_num

cat << end > $HOME/.OK-polipo.temp
#OK-polipo
socksParentProxy = "localhost:1080"
socksProxyType = socks5
#OK-polipo
end

sudo sed -E "$line_num r $HOME/.OK-polipo.temp" /etc/polipo/config -i

rm $HOME/.OK-polipo.temp

fi


```
# Bugs known
running `http_proxy=http://localhost:8123 curl ip.gs` and returning false on virtualbox:

```
host:
4.5.5-300.fc24.x86_64

virtualbox --help
Oracle VM VirtualBox Manager 5.1.14

slave:
4.5.5-300.fc24.x86_64
```
