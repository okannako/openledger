![1500x500](https://github.com/user-attachments/assets/f0f32870-8d3c-4205-b3b6-97175338b347)

## Ön Bilgi, Kayıt ve Giriş
- Open Ledger 8M$ yatırım aldı ve ödüllü testnet başlattı. Bütün adımlardan burada ve videoda bahsettim.
- Node yüklemek için üç farklı yöntem var ve aşağıdaki tabloda uptime göre verilecek puanı görebilirsiniz. Ayrıca sosyal medya görevleriyle de ek puanlar toplanıyor.

  ![openn](https://github.com/user-attachments/assets/60e18135-c8cf-4c60-a9b4-03664ad6bde6)

- Windows vs. gb masaüstü işletim sistemleri için direkt Gmail ile **[Buradan](https://testnet.openledger.xyz/?referral_code=bqp4npvuny)** giriş yapıyoruz. Girdkten sonra aşağıdaki gibi bir ekranla karşılaşacaksınız. Ayrıntılarıdan videoda bahsettim.

![openn22](https://github.com/user-attachments/assets/a713ec14-fbdc-4235-bbde-44db2677ecca)

## Linux Vps İçin Kurulum Adımları
- Buradaki adımları yaparak vps üzerinde tarayıcı sayfası açarak chrome eklentisini kuruyoruz.
- İlk olarak Docker ile Chromium tarayıcıyı vps'e kuruyoruz.
```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Docker version check
docker --version
```

### Timezone Kontrolü
```
realpath --relative-to /usr/share/zoneinfo /etc/localtime
```

### Chromium Yükleme Adımları

1-) Klasör oluşturma
```
mkdir chromium
cd chromium
```

2-) docker-compose.yaml dosyası oluşturmak
```
nano docker-compose.yaml
```

```
---
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER=Kullanıcı
      - PASSWORD=Sifre
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CHROME_CLI=https://testnet.openledger.xyz/?referral_code=bqp4npvuny #optional
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   #Change 3010 to your favorite port if needed
      - 3011:3001   #Change 3011 to your favorite port if needed
    shm_size: "1gb"
    restart: unless-stopped
```

3-) Chromium Başlatmak
```
docker compose up -d
```

4-) Chromium Durdurma ve Silme
```
docker stop chromium
docker rm chromium
docker system prune
```

SON: Yükleme adımları bu kadardı. Mutlaka videoyu izleyerek yapın. Destek için YILDIZ ve FORK tuşlarına tıklayabilirsiniz. Teşekkürler. Kolay gelsin.

