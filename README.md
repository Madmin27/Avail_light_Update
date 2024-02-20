		
# Kontroller
curl "http://localhost:7000/v1/latest_block"
curl "http://localhost:7000/v1/confidence/1"
curl "http://localhost:7000/v1/appdata/1?decode=true"
curl "localhost:7000/v1/mode"
curl "localhost:7000/v1/status"

# # upgrade 
sudo systemctl daemon-reload && sudo systemctl stop availightd && sudo systemctl disable availightd
* klasörü sil

sudo apt update
sudo apt install make clang pkg-config libssl-dev build-essential

# Başlat
cd /root && mkdir -p /root/avail-light && cd /root/avail-light

wget https://github.com/availproject/avail-light/releases/download/v1.7.8/avail-light-linux-amd64.tar.gz
tar -xvzf avail-light-linux-amd64.tar.gz &&
cp avail-light-linux-amd64 avail-light
cargo build --release

sudo systemctl daemon-reload && sudo systemctl enable availightd && sudo systemctl start availightd
systemctl status availightd.service
journalctl -f -u availightd


** identy.toml  dosyasını içine at


# systemctl oluşturma availightd
sudo nano /etc/systemd/system/availightd.service

screen -S availightd
./avail-light --network goldberg


*************
[Unit]
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0

[Service]

User=root
Group=root
WorkingDirectory=/root/avail-light
ExecStart=/root/avail-light/avail-light --network goldberg
Restart=always
RestartSec=120

[Install]
WantedBy=multi-user.target

*******************
