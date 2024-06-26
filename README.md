# Servidor de Streaming com NGINX

Um servidor para streaming de arquivos estáticos, somente o essencial para você transmitir e assistir ✨

## 🔧 Tecnologias utilizadas

![NGINX](https://skillicons.dev/icons?i=nginx)

## 👮 Segurança - Adicionando chave SSH

- Gerar chave SSH no PuTTYgen
  
```
  * Clique no botão Generate
  * Crie um senha para a chave
  * Salve chave privada (essa chave fica na sua máquina)
  * Todo o código do campo "Public Key" deve ser copiado e salvo no servidor
```

- Configuração na VPS para habilitar o acesso apenas com a chave SSH
  
```
* Crie o diretório de chave SSH:
> mkdir .ssh
* Acesse o diretorio criado:
> cd .ssh
* Criando o arquivo authorized_keys, local onde a chave pública precisa ser armazenadas(Cole nesse arquivo):
> sudo nano authorized_keys
* Abra o arquivo sshd_config para desabilitar a autenticação por senha:
> sudo nano /etc/ssh/sshd_config
* Altere os seguintes comandos:
> PasswordAuthentication no
> ChallengeResponseAuthentication no
> UsePAM no
```
- [Adicionando chave SSH - Tutorial em Video](https://www.youtube.com/watch?v=WyZWMIA4XUA)

## 🚀 Rodando o projeto

- Rodar o comando para atualizar os pacotes do linux
  > sudo apt-get update -y

- Rodar os comandos para instalar o nginx, certbot e seu plugin gerador de certificado SSL
  > sudo apt-get install nginx -y
  > sudo apt-get install certbot -y
  > sudo apt-get install python3-certbot-nginx -y

- Acesse a pasta /etc/nginx/sites-available
  > cd /etc/nginx/sites-available

- Dentro desse diretório cria um arquivos chamado site.conf
  > sudo nano site.conf

- Adicione esse trecho dentro do arquivo site.conf

```
server {
    server_name v-play.online;

    location /hls {
      types {
        application/vnd.apple.mpegurl m3u8;
        video/mp2t ts;
      }
      root /stream;
      add_header Cache-Control no-cache;
      add_header Access-Control-Allow-Origin *;
    }
}
```

- Salve e Feche o arquivo
  > CTRL + O / ENTER / CTRL + X

- Habilitando o domínio informado no arquivo site.config e criando link simbolico que vai ficar dentro da pasta sites-enabled
  > sudo ln -s /etc/nginx/sites-available/site.conf /etc/nginx/sites-enabled/

- Retorne para o diretiorio /etc/nginx
  > cd /etc/nginx

- Removendo configuração default do Nginx
  > sudo rm sites-enabled/default

- Verificando se as configurações do Nginx estão corretas
  > sudo nginx -t

- Reniciando o Nginx
  > sudo systemctl reload nginx

- Gerando e instalando o certifiado SSL através do plugin instalado no início
  > sudo certbot --nginx

## 🚨 Monitoramento do Hardware

- Instale o gerenciador de versões do nodejs
  > sudo npm install -g n

- Instale a versão desejada do nodejs
  > sudo n XX.XX.XX

- Instale o forever
  > sudo npm install forever -g

- Clone o repositório
  > git clone https://github.com/V-Carvalho/Bot_Hardware_Manager.git

- Rode dentro da pasta do projeto
  > npm install

- Inicie aplicação de monitoramento
  > forever start app.js

## ➕ Informações Extras

- Faça upload dos videos usando o CyberDuck

```
  Tipo de Protocolo / Conexão: SFTP (SSH File Transfer Protocol)
  Server: IP do server
  Username: root
  Senha: Deixar em branco
  SSH Private Key: Escolha o diretorio da chave
```

## 📺 Instalação do SSL - Tutorial em Video

- [Clique Aqui!](https://www.youtube.com/watch?v=EugUN6yz4Jk&t=503s)

## 🌐 Como assistir a transmissão

- Abra o VLC > Mídia > Abrir Transmissão de Rede > Informe a URL do video
  > **"https://IP_SERVER/hls/FOLDER_NAME/T1/E1/E1.m3u8"**
