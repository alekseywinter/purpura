1. Сначала обновляем список репозиториев Debian:
`sudo apt update`

2. Для полного счастья можно добавить все возможные репозитории в файл `/etc/apt/sources.list`:
#`Stable Debian`
`deb http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware`
`deb-src http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware`

`#Security Updates`
`deb http://deb.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware`
`deb-src http://deb.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware`

`#Stable Updates`
`deb http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware`
`deb-src http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware`

`#Backports`
`deb http://deb.debian.org/debian bookworm-backports main contrib non-free non-free-firmware`
`deb-src http://deb.debian.org/debian bookworm-backports main contrib non-free non-free-firmware`

3. Затем обновляем систему:
`sudo apt update`
`sudo apt upgrade`

После этого устанавливаем нужные (и не очень) пакеты и их зависимости:
`sudo apt install -y \`
`python3 python3-venv python3-pip \`
`build-essential cmake libelf-dev \`
`qemu-system-x86 qemu-kvm qemu-utils \`
`libvirt-clients libvirt-daemon-system virtinst \`
`wireshark tshark telnet \`
`tcpdump  \`
`ca-certificates mesa-utils curl git libpcap-dev \`
`ubridge dynamips`

4. Если по какой то причине `ubridge` и `dynamips` не установились из репозитория Debian придется собирать их вручную.:
`cd /tmp`
`git clone https://github.com/GNS3/dynamips.git`
`cd dynamips`
`mkdir build`
`cd build`
`cmake ..`
`make`

`cd /tmp`
`git clone https://github.com/GNS3/ubridge.git`
`cd ubridge`
`make`
`sudo make install`
`ubridge -v`

5. Дальше создаем виртуальное окружение для исполняемых фалов GNS3:
`python3 -m venv ~/gns3`
`source ~/gns3/bin/activate`

Проверяем где расположен `python`:
`which python`
ответ должен выглядеть примерно так:
`/home/ИМЯ_ПОЛЬЗОВАТЕЛЯ/gns3/bin/python`

6. Устанавливаем графический интерфейс и сервер, а так же их зависимости:
`pip install "sip<6" "PyQt5<5.15" gns3-server==3.0.5 gns3-gui==3.0.5`

Проверяем что все нужные компоненты установлены:
`python -c "import PyQt5; print('PyQt OK')"`  
`python -c "from PyQt5 import sip; print('SIP OK')"`

7. Проверяем запуск GNS3:
`~/gns3/bin/gns3`
или
`source ~/gns3/bin/activate`
`gns3`

Если программа запускается без ошибок то выполняем финальные шаги:
`sudo usermod -aG libvirt,kvm,wireshark,dialout,plugdev $USER`

Настраиваем сеть для виртуальных машин GNS3:
`sudo virsh net-start default`
`sudo virsh net-autostart default`