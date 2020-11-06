# fix-my-trouble
# Ошибка при обновлении Deepin v20 (1002)
echo "deb https://uos-packages.deepin.com/printer eagle non-free" | sudo tee /etc/apt/sources.list.d/printer.list

# Установка недостающих пакетов Deepin 15.11
sudo apt install kbd mc links htop curl cmus mpv

# Решение проблем индикатором раскладки Deepin 15.11
pkill dde-dock

# Сервис
sudo nano /etc/systemd/system/fix-my-trouble.service

# >> fix-my-trouble.service
[Unit]
Description=Fix My Trouble
After=multi-user.target

[Service]
Type=idle
ExecStart=/etc/systemd/system/fix-my-trouble.sh

[Install]
WantedBy=multi-user.target

# Скрипт
sudo nano /etc/systemd/system/fix-my-trouble.sh

# >> fix-my-trouble.sh
#!/bin/sh -e
sudo setkeycodes 3a 42
sudo iptables -t mangle -A POSTROUTING -j TTL --ttl-set 65

# Права
sudo chmod u+x /etc/systemd/system/fix-my-trouble.sh
sudo chmod 644 /etc/systemd/system/fix-my-trouble.service

# Запуск
sudo systemctl daemon-reload
sudo systemctl enable /etc/systemd/system/fix-my-trouble.service

# Импорт конфигурационных файлов ovpn (пример)
nmcli c import type openvpn file ~/.ProtonVPN/jp-free-01.protonvpn.com.udp.ovpn
