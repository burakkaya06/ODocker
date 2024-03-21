# Build aşaması
FROM maven:3.8.4-openjdk-11 as build

# Git kurulumu
RUN apt-get update && apt-get install -y git

# Çalışma dizini ayarlayın
WORKDIR /workspace

# Repo klonlama (repo URL'si ve branch sabit kalacak)
ARG GIT_TOKEN
RUN git clone -b master https://$GIT_TOKEN@github.com/SAGLIKDOSYAM/MyHealthFileMainProject.git ./app

# Klonlanan reponun dizinine girin
WORKDIR /workspace/app

# Bağımlılıkları indir
RUN mvn dependency:go-offline

RUN sed -i 's|spring.datasource.url=jdbc:postgresql://containers-us-west-139.railway.app:7825/railway|spring.datasource.url=jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/resources/application.properties
RUN sed -i 's|spring.datasource.password=bm7jX2FIoLlCcE01IDS4|spring.datasource.password=88qJp1zLy7JUmkPK8emrU3|g' ./src/main/resources/application.properties

RUN sed -i 's|spring.datasource.url=jdbc:postgresql://localhost:5432/my_health_file|spring.datasource.url=jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/resources/application-dev.properties
RUN sed -i 's|spring.datasource.password=99019901Ae|spring.datasource.password=88qJp1zLy7JUmkPK8emrU3|g' ./src/main/resources/application-dev.properties

RUN sed -i 's|spring.datasource.url=jdbc:postgresql://containers-us-west-139.railway.app:7825/railway|spring.datasource.url=jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/resources/application-devrail.properties
RUN sed -i 's|spring.datasource.password=y64b2wcVBceqFsp8vymc|spring.datasource.password=88qJp1zLy7JUmkPK8emrU3|g' ./src/main/resources/application-devrail.properties


#Proje içi yönlendirme
RUN sed -i 's|account-service.uri=https://saglikdosyam-account.up.railway.app/api/parents/save|account-service.uri=http://accountservice:50503/api/parents/save|g' ./src/main/resources/application-devrail.properties
RUN sed -i 's|account-service.uri.notification=https://saglikdosyam-account.up.railway.app/api/notifications/save|account-service.uri.notification=http://accountservice:50503/api/notifications/save|g' ./src/main/resources/application-devrail.properties


RUN sed -i 's|https://www.ealerji.com/verification/|http://op.kayacode.tech/main/api/auth/verify/email?verificationId=|g' ./src/main/java/org/myhealthfile/app/utils/EmailUtil.java



# Projeyi derleyin
RUN mvn clean package -DskipTests

# Çalıştırma aşaması
FROM openjdk:11-jre-slim

# Çalışma dizinini ayarlayın
WORKDIR /app

# Derleme aşamasından oluşturulan JAR dosyasını kopyalayın
COPY --from=build /workspace/app/target/*.jar /app/app.jar

# Uygulamayı çalıştırın
CMD ["java", "-jar", "/app/app.jar"]
