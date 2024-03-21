FROM maven:3.8.4-openjdk-11 as build

RUN apt-get update && apt-get install -y git

WORKDIR /workspace

ARG GIT_TOKEN
RUN git clone -b master https://$GIT_TOKEN@github.com/SAGLIKDOSYAM/AccountService.git ./app

# Maven bağımlılıklarını indirin ve projeyi derleyin
WORKDIR /workspace/app

RUN sed -i 's|spring.datasource.url=jdbc:postgresql://containers-us-west-115.railway.app:7961/railway|spring.datasource.url=jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/resources/application-dev.properties
RUN sed -i 's|spring.datasource.password=AGoTVtDt97ibNLrjLLXa|spring.datasource.password=88qJp1zLy7JUmkPK8emrU3|g' ./src/main/resources/application-dev.properties

RUN sed -i 's|spring.datasource.url=jdbc:postgresql://containers-us-west-115.railway.app:7961/railway|spring.datasource.url=jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/resources/application.properties
RUN sed -i 's|spring.datasource.password=xGEGz7rvsJPmYOvUeQ2R|spring.datasource.password=88qJp1zLy7JUmkPK8emrU3|g' ./src/main/resources/application.properties

RUN sed -i 's|jdbc:postgresql://containers-us-west-115.railway.app:7961/railway|jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/java/org/myhealthfile/config/DataSourceConfig.java
RUN sed -i 's|AGoTVtDt97ibNLrjLLXa|88qJp1zLy7JUmkPK8emrU3|g' ./src/main/java/org/myhealthfile/config/DataSourceConfig.java

#bu bir bug
RUN sed -i "/@ColumnDefault(\"'NEW'\")/d" ./src/main/java/org/myhealthfile/data/entity/notifications/BaseNotification.java


RUN mvn dependency:go-offline
RUN mvn clean package -DskipTests

# Çalıştırma aşaması için yeni bir base image kullanın
FROM openjdk:11-jre-slim

WORKDIR /app

# Hedef klasördeki .jar dosyasını kopyalayın
COPY --from=build /workspace/app/target/*.jar /app/app.jar

# Uygulamayı çalıştırın
CMD ["java", "-jar", "/app/app.jar"]