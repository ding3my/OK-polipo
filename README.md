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

cat << end > $HOME/.OK-polipo
#OK-polipo
socksParentProxy = "localhost:1080"
socksProxyType = socks5
#OK-polipo
end

sudo sed -E "$line_num r $HOME/.OK-polipo" /etc/polipo/config -i

rm $HOME/.OK-polipo

fi


```

