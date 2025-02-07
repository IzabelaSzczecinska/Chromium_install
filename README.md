# Chromium_install
# Aktualizacja serwera:
  sudo apt update && sudo apt upgrade

# Instalacja dockera:
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
  
  # Docker version check
  docker --version

# Timezone check 
  realpath --relative-to /usr/share/zoneinfo /etc/localtime

# Instalacja Chromium 
  mkdir chromium
  cd chromium
  nano docker-compose.yaml ---> wklejamy tam poniższy kod, uzupełniając go naszą wymyśloną nazwą użytkownika i hasłem, oraz uzupełniamy "TZ" wynikiem komendy # Timezone check

  ---
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER=     #Replace username
      - PASSWORD=    #Replace password
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London #Replace with your timezone
      - CHROME_CLI= #optional
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   #Change 3010 to your favorite port if needed
      - 3011:3001   #Change 3011 to your favorite port if needed
    shm_size: "1gb"
    restart: unless-stopped

zapisujemy poprzez wciśniecię CTRL+x, następnie y i Enter

# Uruchomienie Chromium
  cd $HOME && cd chromium
  
  docker compose up -d

Łączymy sie z chromium poprzez wpisanie w przeglądarce IP:3010, logujemy się wpisanym przez siebie powyżej loginem i hasłem
  
  
