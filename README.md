# Servidor de Streaming com NGINX

Um servidor para streaming de arquivos estáticos, somente o essencial para você transmitir e assistir ✨

## 🔧 Tecnologias utilizadas

![NGINX](https://skillicons.dev/icons?i=nginx)

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
      root /tmp;
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

## ➕ Informações Extras

- Faça upload dos videos usando o WinSCP

## 🌐 Como assistir a transmissão

- Abra o VLC > Mídia > Abrir Transmissão de Rede > Informe a URL do video
  > **"https://IP_SERVER/hls/T1/EP1/1.m3u8"**