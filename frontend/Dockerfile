
FROM node:latest as build

RUN apt-get update && apt-get install -y git

WORKDIR /app

ARG GIT_TOKEN
RUN git clone -b main https://$GIT_TOKEN@github.com/SAGLIKDOSYAM/EAllergy.git .


RUN npm install

RUN sed -i 's|NEXT_PUBLIC_SIGNUP_API_URL_TEST1="https://saglikdosyam.up.railway.app/api/users/member/save"|NEXT_PUBLIC_SIGNUP_API_URL_TEST1="http://op.kayacode.tech/main/api/users/member/save"|' .env

RUN sed -i 's|PRIVATE_SIGNUP_API_URL_TEST3=https://saglikdosyam.up.railway.app/api/users/member/saves"|PRIVATE_SIGNUP_API_URL_TEST3=http://op.kayacode.tech/main/api/users/member/saves|' .env

RUN sed -i 's|SIGNUP_API_URL_TEST4=up.railway.app/api/users/member/save|SIGNUP_API_URL_TEST4=http://op.kayacode.tech/main/api/users/member/save|' .env

RUN sed -i 's|NEXT_PUBLIC_SIGNUP_API_URL=https://saglikdosyam.up.railway.app/api/users/member/save"|NEXT_PUBLIC_SIGNUP_API_URL=http://op.kayacode.tech/main/api/users/member/save|' .env

RUN sed -i 's|SIGNUP_API_URL_TEST5=up.rapp/api/users/member/save"|SIGNUP_API_URL_TEST5=http://op.kayacode.tech/main/api/users/member/save|' .env

RUN sed -i 's|NEXT_PUBLIC_SIGNUP_API_URL=https://saglikdosyam.up.railway.app/api/users/member/save|NEXT_PUBLIC_SIGNUP_API_URL=http://op.kayacode.tech/main/api/users/member/save|' .env

RUN sed -i 's|NEXT_PUBLIC_LOGIN_API_URL="https://ealerji.com/api/auth/login"|NEXT_PUBLIC_LOGIN_API_URL="http://op.kayacode.tech/main/api/auth/login"|' .env


RUN npm run build

EXPOSE 80

# Uygulamayı başlatın
CMD ["npm", "start"]
