Выключи VM полностью

Очень важно! Не делаем это на работающей системе.

2️⃣ Увеличиваем файл диска на хосте

qemu-img resize debian-12.6.qcow2 +2G
Файл теперь больше (~4 GB), VM ещё не знает об этом.

3️⃣ Не трогаем старый раздел!

Сейчас у тебя есть /dev/sda1 с root, который занимает 1.9 GB.

Мы не удаляем его, просто расширим файловую систему.

Расширяем раздел безопасно
Устанавливаем пакет cloud-guest-utils, который содержит growpart:
sudo apt update
sudo apt install -y cloud-guest-utils

Расширяем основной раздел /dev/sda1 до конца диска:
sudo growpart /dev/sda 1

Проверяем с помощью:
lsblk
Теперь /dev/sda1 будет занимать весь диск (~4 GB)

Расширяем файловую систему
sudo resize2fs /dev/sda1
После этого df -h покажет весь увеличенный размер /



sudo apt update
sudo apt install -y python3 python3-pip python3-scapy


python3 -c "from scapy.all import *; show_interfaces()"