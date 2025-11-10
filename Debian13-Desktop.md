# ติดตั้งและใช้งาน Debian 13 (Desktop)
บันทึกเพื่อตัวฉันเอง

## ติดตั้ง Debian 13
- Partition: LUKs Encrypted

## จัดการ Desktop
```bash
sudo apt install gnome-tweaks
```

### ติดตั้ง extension สำหรับตั้งค่า Dask Dock
https://extensions.gnome.org/extension/307/dash-to-dock/


## ติดตั้งโปรแกรมสำหรับ Development
### ติดตั้ง git
```bash
apt install git
```

Github login
```bash
git config --global user.name "userName"
git config --global user.email "user@email.com"
git config --global user.password "Password"
```

### ติดตั้ง VSCode
```bash
sudo apt install code
```
* ติดตั้ง Gemini Code Assist (ทำงานใน VSCode)

### ติดตั้ง Gemini-CLI (ผ่าน brew)
ติดตั้ง brew ที่ https://brew.sh/
หลังจากนั้น
```bash
brew install gemini-cli
```

### ติดตั้ง Docker
ลบ docker เวอร์ชั่นอื่นๆออก
```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

#### ติดตั้ง docker
Add Docker's official GPG key:
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Add the repository to Apt sources:
```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF
sudo apt-get update
```

ติดตั้ง docker engine
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Networking
### ติดตั้ง L2TP client
ติดตั้งแพ็คเกจที่จำเป็น
```bash
sudo apt-get update
sudo apt-get install strongswan xl2tpd net-tools network-manager-l2tp-gnome
```

### ติดตั้ง OpenVPN client
```bash
apt install apt-transport-https curl
mkdir -p /etc/apt/keyrings    ### This might not exist in all distributions
curl -sSfL https://packages.openvpn.net/packages-repo.gpg >/etc/apt/keyrings/openvpn.asc
echo "deb [signed-by=/etc/apt/keyrings/openvpn.asc] https://packages.openvpn.net/openvpn3/debian trixie main" >>/etc/apt/sources.list.d/openvpn3.listh
apt update
apt install openvpn3
```

นำเข้า config
```bash
openvpn3 config-import --config file.ovpn --name NAME
```

เชื่อมต่อ
```bash
openvpn3 session-start --config NAME`
```

การจัดการ Session
```bash
openvpn3 sessions-list`
```

ตัดการเชื่อมต่อ
```bash
openvpn3 session-manage --disconnect --config NAME
```

ลบ Config ที่นำเข้าแล้ว: หากไม่ต้องการใช้งานแล้ว:
```bash
openvpn3 config-remove --config WCDT
```

## ติดตั้ง Bottles สำหรับรัน Windows programs
```bash
sudo apt install flatpak && sudo apt install gnome-software-plugin-flatpak && flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak install flathub com.usebottles.bottles
```

## อื่นๆ 
### ติดตั้ง Google Chrome
```bash
sudo apt install google-chrome-stable
```
### ติดตั้ง Winbox

### ติดตั้ง VNC Viewer
จาก https://www.realvnc.com/en/connect/download/viewer/linux/

### ถอนการติดตั้ง LibreOffice
```bash
apt-get purge libreoffice*
```

### ติดตั้ง Network/Secutiry Tools
```bash
apt install nmap tcpdump traceroute bind9-dnsutils
```
