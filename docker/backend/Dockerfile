# build stage
FROM maven:3.9.9-amazoncorretto-17 AS build
WORKDIR /build
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# Runtime stage
FROM amazoncorretto:17
#ARG PROFILE=dev
ARG APP_VERSION=0.0.1-SNAPSHOT

#define few things
WORKDIR /app
COPY --from=build /build/target/employee-back-*.jar /app/

EXPOSE 8080



#ENV ACTIVE_PROFILE=${PROFILE}
ENV JAR_VERSION=${APP_VERSION}

#CMD java -jar -Dspring.profiles.active=${ACTIVE_PROFILE} employee-back-${JAR_VERSION}.jar
#CMD java -jar employee-back-${JAR_VERSION}.jar
CMD ["java", "-jar", "/app/employee-back-1.0.1-SNAPSHOT.jar"]
