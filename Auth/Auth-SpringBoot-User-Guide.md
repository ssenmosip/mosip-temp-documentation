This document lists out the instructions on how to use the [AuthAdapter](https://github.com/mosip/mosip/wiki/Auth-Adapter) in a Spring Boot application.

* Step 1: [Inject required libraries](#Inject-required-libraries)
* Step 2: [Attach annotations to authorize endpoints](#Attach-annotations-to-authorize-endpoints)
* Step 3: [Attach auth token to the response servlet](#Attach-auth-token-to-the-response-servlet)
* Step 4: [Use restTemplate for Http calls](#Use-restTemplate-for-Http-calls)

## Inject required libraries
Add the [AuthAdapter](https://github.com/mosip/mosip/wiki/Auth-Adapter) module to your project as a maven dependency
```java
<dependency>
	<groupId>io.mosip.kernel</groupId>
	<artifactId>kernel-auth-adapter</artifactId>
	<version>1.0.0-SNAPSHOT</version>
</dependency>
```
Then add _**/api**_ as your base path in your properties file
```properties
server.servlet.path=/api/.......
```
## Attach annotations to authorize endpoints
To restrict access to your endpoints, you need to add the **@PreAuthorize** annotation.
Look at the below example for reference.
```java
@PreAuthorize("hasAnyRole('DIVISION_ADMIN', 'SUPERVISOR', 'AGENT')")
@RequestMapping(value = "/api/restaurants", method = RequestMethod.GET)
```
There are few more methods available apart from hasAnyRole like hasRole. Look in to the [@PreAuthorize](https://docs.spring.io/spring-security/site/docs/3.0.x/reference/el-access.html) documentation for more details.

**Note:** Now we support ony hasRole and hasAnyRole methods.

## Attach auth token to the response servlet
To attach auth token we first need to autowire AuthHeadersFilter into your RestController as shown below.

```java
@Autowired
AuthHeadersFilter authHeadersFilter;
```

Now in your Controller method use ResponseEntity to attach headers and return a response as shown below.

```java
@RequestMapping(value = "/api/restaurant/{id}", method = RequestMethod.GET)
public ResponseEntity<RestaurantEntity> getRestaurantById(@PathVariable Integer id) throws Exception {
    HttpHeaders httpHeaders = new HttpHeaders();
    httpHeaders.set("Authorization", authHeadersFilter.getToken());
    ResponseEntity responseEntity = new ResponseEntity(restaurantsService.getRestaurantById(id), httpHeaders, HttpStatus.OK);
    return responseEntity;
}
```

## Use restTemplate for Http calls
To make any kind of HTTP or HTTPS calls to a mosip's micro service that also injected the [AuthAdapter](https://github.com/mosip/mosip/wiki/Auth-Adapter), use the standard RestTemplate capabilities as shown below.

* Intially autowire the RestTemplate in the class where you are going to make an API call.

```java
@Autowired
private RestTemplate restTemplate;
```

* Now make the call using the autowired restTemplate as shown in the sample below:

```java
final String uri = "http://localhost:3001/api/location";
LocationDao response = restTemplate.getForObject(uri, LocationDao.class);
```

**Note:** Do not create a new instance of the RestTemplate instead use the autowired one.