# Stage 1: Build with Maven
FROM maven:3.8.4-openjdk-17 AS builder
WORKDIR /app
COPY ./pom.xml .
COPY ./src ./src
RUN mvn clean package -DskipTests && \
    find /app/target -name "*.jar" -not -name "*-original.jar" -exec cp {} /app/app.jar \;

# Stage 2: Create the final image
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
VOLUME /tmp
# Copier le JAR depuis l'étape builder
COPY --from=builder /app/app.jar /app/app.jar
ENTRYPOINT ["java","-jar","/app/app.jar"]