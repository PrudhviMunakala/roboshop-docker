# FROM maven:3.9.14
# WORKDIR /app
# COPY src ./src
# COPY pom.xml . 
# RUN mvn clean package
# RUN mv target/shipping-1.0.jar shipping.jar 
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD [ "java", "-jar", "shipping.jar" ]

# ================================
# Stage 1: Build
# ================================
FROM maven:3.9.14 AS builder
WORKDIR /app

# Copy pom.xml first — caches dependencies as a separate layer
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Now copy source and build
COPY src ./src  
RUN mvn clean package -DskipTests

# ================================
# Stage 2: Runtime
# ================================
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app

# Pull only the JAR from the build stage
COPY --from=builder /app/target/shipping-1.0.jar shipping.jar
USER roboshop 

CMD ["java", "-jar", "shipping.jar"]

