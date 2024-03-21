FROM maven:3.8.4-openjdk-11 as build

RUN apt-get update && apt-get install -y git

WORKDIR /workspace

ARG GIT_TOKEN
RUN git clone -b main https://$GIT_TOKEN@github.com/SAGLIKDOSYAM/ComplaintQuestions.git ./app

WORKDIR /workspace/app

RUN sed -i 's|spring.datasource.url=jdbc:postgresql://containers-us-west-150.railway.app:5446/railway|spring.datasource.url=jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/resources/application-dev3.properties
RUN sed -i 's|spring.datasource.password=cl5E9AKA7WdSAiscGAkW|spring.datasource.password=88qJp1zLy7JUmkPK8emrU3|g' ./src/main/resources/application-dev3.properties

RUN sed -i 's|spring.datasource.url=jdbc:postgresql://localhost:5432/dev|spring.datasource.url=jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/resources/application-dev2.properties
RUN sed -i 's|spring.datasource.password=99019901Ae|spring.datasource.password=88qJp1zLy7JUmkPK8emrU3|g' ./src/main/resources/application-dev2.properties

RUN sed -i 's|spring.datasource.url=jdbc:postgresql://localhost:5432/dev2|spring.datasource.url=jdbc:postgresql://161.35.229.123:32768/railway|g' ./src/main/resources/application-dev.properties
RUN sed -i 's|spring.datasource.password=99019901Ae|spring.datasource.password=88qJp1zLy7JUmkPK8emrU3|g' ./src/main/resources/application-dev.properties



RUN mvn dependency:go-offline
RUN mvn clean package -DskipTests

FROM openjdk:11-jre-slim


WORKDIR /app

COPY --from=build /workspace/app/target/*.jar /app/app.jar

# Uygulamayı çalıştırın
CMD ["java", "-jar", "/app/app.jar"]
