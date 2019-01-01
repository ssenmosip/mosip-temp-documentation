# Auth Adapter usage Guidelines

This document explains how to use the Auth Adapter in a Spring Boot application in the follwing four sections.

* [Libraries Injection](#Libraries-Injection)
* [Request mapping method returns ResponseEntity](#Request-mapping-method-returns-ResponseEntity)
* [Authorize endpoints](#Authorize-endpoints)
* [Micro service to Micro service communication](#Micro-service-to-Micro-service-communication)

## Libraries Injection
Follow the below instructions to make your project ready for Authentication and Authorization.

### Add below mentioned spring security libraries in to your pom.xml
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-test</artifactId>
    <scope>test</scope>
</dependency>
```

### Add the [AuthAdapter](https://github.com/mosip/mosip/wiki/Auth-Adapter) module to your project as specified below
```
To be updated
As of now copy paste it from the Github
```

## Request mapping method returns ResponseEntity
Once the request processing is done, do not directly return the response instead use the ResponseEntity as shown below.
```
@RequestMapping(value = "/api/restaurant/{id}", method = RequestMethod.GET)
public ResponseEntity<RestaurantEntity> getRestaurantById(@PathVariable Integer id) throws Exception {
    HttpHeaders httpHeaders = new HttpHeaders();
    httpHeaders.set("Authorization", authHeadersFilter.getToken());
    ResponseEntity responseEntity = new ResponseEntity(restaurantsService.getRestaurantById(id), httpHeaders, HttpStatus.OK);
    return responseEntity;
}
```

The authHeadersFilter used above will be autowired in the RestController as shown below.
```
@Autowired
AuthHeadersFilter authHeadersFilter;
```

## Authorize endpoints
All you need to do to protect your endpoint's is add the **@PreAuthorize** annotation above your RequestMapping as shown below:
```
@PreAuthorize("hasAnyRole('DIVISION_ADMIN', 'SUPERVISOR', 'AGENT')")
@RequestMapping(value = "/api/restaurants", method = RequestMethod.GET)
```

## Micro service to Micro service communication
To make any kind of HTTP or HTTPS calls to a mosip's micro service that also injected the [AuthAdapter](https://github.com/mosip/mosip/wiki/Auth-Adapter), use the standard RestTemplate capabilities as mentioned below.

* Intially autowire the RestTemplate in the class where you are going to make an API call.
```
@Autowired
private RestTemplate restTemplate;
```
* Now make the call using the autowired restTemplate. See the sample below:
```
final String uri = "http://localhost:3001/api/location";
LocationDao response = restTemplate.getForObject(uri, LocationDao.class);
```

**Note:** Do not create a new instance of the RestTemplate instead use the autowired one.