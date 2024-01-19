# Specify the base image with Maven for building
FROM maven:3.8-openjdk-17 AS builder

# Set the working directory in the container
WORKDIR /app

# Copy the source code and pom.xml to the container
COPY ./src ./src
COPY ./pom.xml .

# Build the Maven project
RUN mvn clean package
# Specify the base image for the final image
FROM openjdk:17-jdk-alpine

# Create a volume for temporary files
VOLUME /tmp

# Define an argument for the JAR file
ARG JAR_FILE=target/*.jar

# Copy the compiled JAR file from the builder stage to the final image
COPY --from=builder /app/${JAR_FILE} app.jar

# Set the entry point for the container
ENTRYPOINT ["java", "-jar", "/app.jar"]