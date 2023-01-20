# EmployeeControl
 🅰 Angular + 🍃 Spring Boot  - CRUD

## Prints
<img src="https://github.com/petscaramussi/images/blob/main/CRUP-APP/1.PNG" width="32%"> <img src="https://github.com/petscaramussi/images/blob/main/CRUP-APP/2.PNG" width="32%"> <img src="https://github.com/petscaramussi/images/blob/main/CRUP-APP/3.PNG" width="32%">


## Build

### Angular

1. Go to project folder 'client' then 'angular-frontend' and install dependencies:
 ```bash
 npm install
 ```
 
2. Launch development server, and open `localhost:4200` in your browser:
 ```bash
 npm start
 ```
 
 ### Spring
 
 1. You don’t need to build from source to use Spring Data (binaries in repo.spring.io), but if you want to try out the latest and greatest, Spring Data can be easily built with the maven wrapper. You also need JDK 17 or above.
  ```bash
    ./mvnw clean install
 ```
 
 2. run the following command in a terminal window (in the complete) directory: src/main/java/net/javaguides/springbootbackend/Application.java
 ```bash
   ./mvnw spring-boot:run
 ```
 
 3. Gradle and Maven

The code samples in the book use Apache Maven as the build tool. If you prefer Gradle over Maven, here's a table mapping Maven commands to Gradle:

| Maven                            | Gradle                     |
| -------------------------------- | -------------------------- |
| `./mvnw clean`                   | `./gradlew clean`          |
| `./mvnw install`                 | `./gradlew build`          |
| `./mvnw test`                    | `./gradlew test`           |
| `./mvnw repackage`               | `./gradlew bootJar`        |
| `./mvnw spring-boot:run`         | `./gradlew bootRun`        |
| `./mvnw spring-boot:build-image` | `./gradlew bootBuildImage` |

### MySql

1. You must have MySql installed on your machine and the server running.

2. create database:
```sql
    create database employee_management_system;
```

3. configure your MySql port on Spring: springboot-backend/src/main/resources/application.properties set
```
spring.datasource.url=jdbc:mysql://localhost:{{ your port here }}/employee_management_system?useSSL=false
```
 
 ## Explanations
 
 ### Create
 
On Spring:

```java
    // create employee rest api
    
    @PostMapping("/employees")
    public Employee createEmployee(@RequestBody Employee employee){
        return employeeRepository.save(employee);
    }
```

On Angular:

Service:
```javascript
    // send post request to api
    
    private baseURL = 'http://localhost:8080/api/v1/employees';
    
    createEmployee(employee: Employee): Observable<Object>{
    return this.httpClient.post(`${this.baseURL}`, employee);
  }
```

Component TS:

```javascript
    saveEmployee() {
     this.employeeService.createEmployee(this.employee).subscribe({
       next: (v) => console.log(v),
       error: (e) => console.error(e),
       complete: () => {console.info('complete'); this.goToEmployeeList()}
    });
  }
```

### Read


 
 
 
 
