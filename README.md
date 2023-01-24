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

On Spring:

```java
    // create employee rest api
    
    @GetMapping("/employees/{id}")
    public ResponseEntity<Employee> getEmployeeById(@PathVariable Long id){
        Employee employee =  employeeRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Employee not exist with id: " + id));
        return ResponseEntity.ok(employee);
    }
    
```
On Angular:

Service:
```javascript
    getEmployeeById(id: Number): Observable<Employee>{
    return this.httpClient.get<Employee>(`${this.baseURL}/${id}`);
  }
  }
```

Component TS:

```javascript
    ngOnInit(): void {
    this.id = this.route.snapshot.params['id'];
    this.emplouyeeService.getEmployeeById(this.id).subscribe(data => {
      this.employee = data;
    });
  }
```

### Update

On Spring:

```java
    // update employee rest api
    
    @PutMapping("/employees/{id}")
    public ResponseEntity<Employee> updateEmployee(@PathVariable Long id, @RequestBody Employee employeeDetails){
        Employee employee =  employeeRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Employee not exist with id: " + id));

        employee.setFirstName(employeeDetails.getFirstName());
        employee.setLastName(employeeDetails.getLastName());
        employee.setEmailId(employeeDetails.getEmailId());

        Employee updateEmployee = employeeRepository.save(employee);

        return ResponseEntity.ok(updateEmployee);
    }
    
```
On Angular:

Service:
```javascript
    updateEmployee(id: number, employee: Employee): Observable<Object>{
    return this.httpClient.put(`${this.baseURL}/${id}`, employee);
  }
```

Component TS:

```javascript
    onSubmit(){
    this.employeeService.updateEmployee(this.id, this.employee).subscribe(data => {
      this.goToEmployeeList();
    }, error => console.log(error));
  }
```

### Delete

On Spring:

```java
    //delete employee rest api
    
    @DeleteMapping("/employees/{id}")
    public ResponseEntity<Map<String, Boolean>> deleteEmployee(@PathVariable Long id){
        Employee employee =  employeeRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Employee not exist with id: " + id));

        employeeRepository.delete(employee);
        Map<String, Boolean> response = new HashMap<>();
        response.put("deleted", Boolean.TRUE);
        return  ResponseEntity.ok(response);
    }
    
```
On Angular:

Service:
```javascript
   deleteEmployee(id: number): Observable<Object>{
     return this.httpClient.delete(`${this.baseURL}/${id}`);
  }
```

Component TS:

```javascript
    deleteEmployee(id: number){
     this.employeeService.deleteEmployee(id).subscribe(data => {
       console.log(data);
       this.getEmployees();
    });
  }
```


## Coding guides

- [Angular](docs/coding-guides/angular.md)
- [TypeScript](docs/coding-guides/typescript.md)
- [Bootstrap](docs/https://getbootstrap.com)
- [Java](https://dev.java/learn/getting-started-with-java/)
- [Spring](https://spring.io/guides/gs/spring-boot/)












 
 
 
 
