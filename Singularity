Bootstrap: docker
From: debian:9

%files

sources.list /etc/apt
99edf /etc/apt/apt.conf.d/
99edfproxy /etc/apt/apt.conf.d/

%post

apt-get update && apt-get -y install build-essential wget

mkdir /local00
mkdir /scratch
chmod 755 /local00
chmod 755 /scratch

sed -i 's/ main/ main contrib non-free/' /etc/apt/sources.list

cat >> /etc/apt/sources.list << EOF
deb http://dist.calibre.edf.fr/scibian9-applis-public scibian9 main
EOF

wget -e use_proxy=on -e https_proxy=https://proxypac.edf.fr:3128 -e http_proxy=http://proxypac.edf.fr:3128 https://scibian.org/repo/scibian-auto-keyring.pub -O- | apt-key add -

cat >> /etc/apt/preferences.d/00scibian << EOF
Package: *
Pin: release o=Scibian
Pin-Priority: 1001
EOF


apt-get update

apt-get -y install scibian-desktop

%post

apt-get -y install locales

%files

locale.gen /etc/

%post

locale.gen
