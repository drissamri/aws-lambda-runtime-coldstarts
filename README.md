# AWS Lambda - Coldstart comparison

- Java8 minimal: **828 ms**
- Java8 full: (Dagger+Gson+DynamoDB): **3.9 sec**
- Java8 Micronaut 1.1.0-RC2 (DynamoDB): **5.3 sec** (WIP: Improvements possible and this is the non-GraalVM example)
- nodejs8 full (DynamoDB): **540 ms**

Below you can see the X-Ray for each example.  
*Initialization (light blue)*: This is code initialization (Static blocks + Constructor)  
*After initialization (dark blue)*: This is the function handler code

### Java 8 - minimal - 1024 MB
![Java 8 - minimal ](./images/java8-minimal-xray.png)

**_CloudWatch_**
```
REPORT Duration: 155.22 ms  Billed Duration: 200 ms  Memory Size: 1024 MB  Max Memory Used: 88 MB
```

### Java 8 - full - 1024 MB

![Java 8 - minimal ](./images/java8-full-xray.png)

- Dagger
- Gson
- AWS SDK 2: DynamoDB
- AWS SDK 2: url-connection-client (faster starting HTTP client)

**_CloudWatch_**
```
REPORT Duration: 2170.02 ms  Billed Duration: 2200 ms  Memory Size: 1024 MB  Max Memory Used: 158 MB	
```

### Java 8 - Micronaut  - 1024 MB

- Micronaut 1.1.0 (RC2)
- AWS SDK 2: DynamoDB
- AWS SDK 2: url-connection-client (faster starting HTTP client)

![Java 8 - minimal ](./images/java8-micronaut-xray.png)

**_CloudWatch_**
```
REPORT Duration: 3210.99 ms  Billed Duration: 3300 ms  Memory Size: 1024 MB  Max Memory Used: 172 MB	
```

### nodejs 8 - full - 1024 MB

- TypeScript
- Webpack
- DynamoDB

**_CloudWatch_**
```
REPORT Duration: 69.36 ms  Billed Duration: 100 ms  Memory Size: 1024 MB  Max Memory Used: 106 MB	
```

![nodejs 8 - full ](./images/nodejs8-full-xray.png)
