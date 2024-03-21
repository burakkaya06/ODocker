# nginx Dockerfile
FROM nginx:alpine

# Özel Nginx yapılandırma dosyanızı kopyalayın
COPY /Docker/znginx/nginx.conf /etc/nginx/nginx.conf

# İsteğe bağlı olarak, static dosyalarınız veya SSL sertifikalarınız varsa bunları da kopyalayabilirsiniz
# COPY static /usr/share/nginx/html
# COPY certs /etc/nginx/certs
