# CasaOS bugado: "Failed to load apps, please refresh later"
Esse erro geralmente acontece depois de rodar o comando sudo apt upgrade. O problema ta rolando porque o CasaOS ainda não reconhece as versões mais recentes do Docker (29.x). A solução atual é fazer o downgrade e travar a atualização do Docker.

* 1. Preparar o sistema e repositórios
Primeiro, atualize a lista de pacotes e instale as dependências necessárias:

sudo apt update
sudo apt install ca-certificates curl


* 2. Adicionar a chave GPG oficial do Docker

sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc


* 3. Adicionar o repositório ao APT

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

* 4. Parar o serviço do Docker

sudo systemctl stop docker

* 5. Instalar a versão específica (28.5.2)
Este comando força a instalação da versão compatível com o CasaOS:

sudo apt install docker-ce=5:28.5.2-1~ubuntu.24.04~noble \
                 docker-ce-cli=5:28.5.2-1~ubuntu.24.04~noble \
                 containerd.io

* 6. Impedir atualizações automáticas do Docker
Para evitar que o Ubuntu atualize o Docker sozinho novamente, use o comando:

sudo apt-mark hold docker-ce docker-ce-cli

* 7. Reiniciar o serviço

sudo systemctl start docker
sudo systemctl enable docker

* 8. Verificar a versão
Para confirmar se deu certo, digite:

docker --version


Dica: Quando o CasaOS for atualizado e passar a aceitar as versões novas, você pode liberar as atualizações do Docker com o comando: sudo apt-mark unhold docker-ce docker-ce-cli