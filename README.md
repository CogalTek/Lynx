# Lynx

### Setup RTMP server with nginx 2024 version

sudo apt update

sudo apt upgrade -y

mkdir Lynx

cd Lynx/

sudo apt install wget tar libpcre3-dev zlib1g-dev build-essential libssl-dev libpcre3

wget https://nginx.org/download/nginx-1.25.5.tar.gz

git clone https://github.com/arut/nginx-rtmp-module.git

tar -zxvf nginx-1.25.5.tar.gz 

rm nginx-1.25.5.tar.gz 

cd nginx-1.25.5/

./configure --add-module=../nginx-rtmp-module

make

sudo make install

sudo wget https://raw.github.com/JasonGiedymin/nginx-init-ubuntu/master/nginx -O /etc/init.d/nginx

sudo chmod +x /etc/init.d/nginx

sudo update-rc.d nginx defaults

cd /usr/local/nginx/conf

> Ajouter ça tout en bas 

```C
rtmp {
    server {
		listen 1935;
		chunk_size 4096;
	
		application live {
			live on;
			record off;
		}
    }
}
```

sudo cp nginx.conf nginx.conf_old

sudo emacs nginx.conf

sudo /usr/local/nginx/sbin/nginx -t

sudo emacs nginx.conf

sudo /usr/local/nginx/sbin/nginx -t

sudo systemctl start nginx

sudo /usr/local/nginx/sbin/nginx -t

sudo shutdown -r now

sudo systemctl status nginx

> URL de connexion a votre serveur (123 = clé)
rtmp://IP_ADRESSE/live/123
