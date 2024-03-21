
FROM node:latest as build

RUN apt-get update && apt-get install -y git

WORKDIR /app

ARG GIT_TOKEN
RUN git clone -b main https://$GIT_TOKEN@github.com/SAGLIKDOSYAM/EAllergy.git .


RUN npm install

# Projenin her yerinde URL'leri güncelleme
RUN find . -type f -exec sed -i 's|https://ealerji.com/api/|http://op.kayacode.tech/main/api/|g' {} +
RUN find . -type f -exec sed -i 's|https://ealerji.com|http://op.kayacode.tech|g' {} +
RUN find . -type f -exec sed -i 's|https://saglikdosyam.up.railway.app/api|http://op.kayacode.tech/main/api|g' {} +

# BASE_PAGE değerini doğrudan güncelleme
RUN find . -type f \( -name "*.js" -o -name "*.env" \) -exec sed -i 's|BASE_PAGE="https://www.ealerji.com/"|BASE_PAGE="http://op.kayacode.tech"|g' {} +




RUN npm run build

EXPOSE 80

# Uygulamayı başlatın
CMD ["npm", "start"]
