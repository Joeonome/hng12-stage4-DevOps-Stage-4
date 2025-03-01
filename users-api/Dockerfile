# Use Maven to build the Spring Boot app
FROM maven:3.8.7 AS builder

# Set the working directory
WORKDIR /app

# Copy the Maven project files and build dependencies
COPY pom.xml ./
RUN mvn dependency:go-offline

# Copy the application source code
COPY src ./src

# Build the Spring Boot application
RUN mvn clean package -DskipTests

# Debugging step: Check if the JAR file exists
RUN ls -la /app/target

# Use OpenJDK for running the application
FROM openjdk:8-jdk-alpine

# Set the working directory
WORKDIR /app

# Copy the built JAR file from the builder stage
COPY --from=builder /app/target/users-api-0.0.1-SNAPSHOT.jar app.jar

# Expose the application port
EXPOSE 6379

# Run the application
CMD ["java", "-jar", "app.jar"]
