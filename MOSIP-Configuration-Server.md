# MOSIP Configuration Server

We will be using MOSIP config server (Spring cloud configurration Server) to manage all the configurations of all the microservices which will be running at a central place.<br/><br/>
**NOTE:** For the documentation purpose I have mentioned the config server URL as http://localhost:8080 ,but you have to mention the URL where configuration server is running

![Configuration Server](_images/arch_diagrams/MOSIP_config_server_setup.png)

## Git Repo
1. All the configuration files will be stored inside git in<br/>
   **\git\mosip\config**<br/>
2. For every module there will be one property file (eg: for kernel)<br/>
   The nomenclature will be as follows:<br/>
   **_{module-name}-{profile-Name}.properties_**<br/>
   For example if the application name is kernel and microservice is kernel-idgenerator-vid and profile name can be 
   dev(to differentiate between different environments, eg: testing, dev, QA etc.), so the properties file name
   will be:<br/>
   **kernel-dev.properties**<br/>
3. If we are using multiple profiles, say one for dev and one for testing, we can create 2 properties files with names - **kernel-test.properties, kernel-dev.properties**, and can switch between multiple profiles through Microservice application.
4. Properties common across the modules will be stored in files named: **application-{profile-name}.properties**
5. For XML files, name them as follows:<br/>
   _**{NameOfFile}-{profileName}.xml**_
## Microservices Configuration Clients:<br/>
### Spring boot client<br/>
   All the microservices will act as clients of config server.<br/>
1. For which microservices will be needing _spring-cloud-starter-config_ dependency, which can be added through maven.

`		<dependency>`<br/>
			`<groupId>org.springframework.cloud</groupId>`<br/>
			`<artifactId>spring-cloud-starter-config</artifactId>`<br/>
		`</dependency>`<br/>

  For actuators refresh endpoint (to refresh properties at runtime) we need actuator dependency in client

`               <dependency>`<br/>
			`<groupId>org.springframework.boot</groupId>`<br/>
			`<artifactId>spring-boot-starter-actuator</artifactId>`<br/>
			`<version>${spring.boot.version}</version>`<br/>
		`</dependency>`<br/>
2. There should be one **bootstrap.properties** file in the spring boot application under resources which will contain the details for MOSIP config server running. Inside the properties file following properties have to be mentioned:
* **spring.cloud.config.uri** key with the value of URL of config server that will be provided.
* **spring.cloud.config.label** which will define the branch from which we have to get properties from.
* **spring.profiles.active** which will contain the value of profile that you have mentioned will saving the file.
*  **spring.application.name** name of the application<br/>
*  **spring.cloud.config.name** name of module to which the application belongs<br/>
*  **spring.cloud.config.username** name of the user if config-server is secured
*  **spring.cloud.config.password** password of the user if config-server is secured


Sample Bootstrap.properties file:<br/>

`#Port where the application needs to run`<br/>
`server.port = 8081`<br/>
`# Application name - the name appended at starting of file name to differentiate`<br/>
`# between different property files for different microservices`<br/>
`spring.application.name=kernal-idgenerator-vid`<br/>
 
`#Active Profile - will relate to development properties file in the server.`<br/>
`#If this property is absent then default profile will be activated which is`<br/>
`#the property file without any environment name at the end. `<br/>
`spring.profiles.active=dev`<br/>


`# defining current branch in which we are working as label`<br/>
`spring.cloud.config.label=DEV `<br/>
 

`# url where spring cloud config server is running `<br/>
`spring.cloud.config.uri=http://localhost:8080`<br/>

 
`#spring.cloud.config.name=kernel`<br/>

`#exposing refresh endpoint so that whenevr configuration changes in git,`<br/>
`#post /actuator/refresh endpoint can be called for the client microservices`<br/>
`#to update the configuration`<br/>
`management.endpoints.web.exposure.include=refresh`<br/>
3. Once the setup is done, the properties can be used in same way in application as local properties file for properties file and yaml file. Letâ€™s assume I have a key â€œmsgâ€� in my properties file, we can get the value as follows:

`/** `<br/>
 `* `<br/>
 `* RefreshScope annotation is used such that all the rest APIs can be updated by calling`<br/>
 `* POST /actuator/refresh endpoint whenever configuration files change in git repo. `<br/>
 `*`<br/>
 `*/`<br/>
`@RefreshScope`<br/>
`@RestController`<br/>
`class MessageRestController {`<br/>
	
`	protected final Log logger = LogFactory.getLog(this.getClass());`<br/>
	
 `   @Value("${msg:Hello world - Config Server is not working..pelase check}")`<br/>
  `  private String msg;`<br/>
    
   ` @RequestMapping("/msg")`<br/>
    `String getMsg() {`<br/>
     `   return this.msg;`<br/>
        
   `  } `<br/>
In the above snippet we are using RefreshScope annotation so that the client should be able to call the refresh API /actuator/refresh, and get latest configuration if there are any changes in configuration in GIT repo and â€œconfig Server not running please checkâ€� is the default value which will be should as value for key â€œmsgâ€� if there is any problem in fetching value from MOSIP config server.<br/>
4. For any other configuration file such as xml/json etc. you can directly get the entire file through the following url:<br/>
**http://{mosip-config-server URL}/{application-name}-{microservice-name} /{label} /{branch}/{filename}.(xml/json).** 
<br/>
<br/>
### Vert.x client:
1. For Vert.x application we need the following dependencies to be added to our Maven project:
        `<dependency>`<br/>
		  `<groupId>io.vertx</groupId>`<br/>
		  `<artifactId>vertx-config-spring-config-server</artifactId>`<br/>
		  `<version>3.5.4</version>`<br/>
	`</dependency>`<br/>
	`<dependency>`<br/>
	`	  <groupId>io.vertx</groupId>`<br/>
	`	  <artifactId>vertx-config</artifactId>`<br/>
	`	  <version>3.5.4</version>`<br/>
	`</dependency>`<br/>
2. We will be using **ConfigRetrieverOptions **in Vert.x and set the store type to "spring-config-server" and we will provide configuration for this type, by giving URL in the following format:<br/>
**_{config-server-url}/{applicationname}-{microservicename}/{profile-name}/{branchname}_**<br/>
   ` protected Future<Void> readConfig(String hoconConfigPath) {`<br/>
         `Future<Void> future = Future.future();`<br/>
         `/ **`<br/>
          `* Adding config options for vert.x application`<br/>
          `*/`<br/>
         `ConfigRetrieverOptions options = new ConfigRetrieverOptions();`<br/>
         `options.addStore(new ConfigStoreOptions()`<br/>
         `		/**`<br/>
         `		 *  Vert.x provides different stores to choose from, right now we are selecting`<br/>
         `		 *  spring-config-server to connect to our server`<br/>
         `		 */`<br/>
           `      .setType("spring-config-server")`<br/>
             `    /**`<br/>
               `   * We are providing URL in the following format - `<br/>
                 ` * <config-server-url>/<application-name-microservicename>/<profile-name>/<branch-name>`<br/>
                 ` * /`<br/>
                 `.setConfig(new JsonObject().put("url", "http://localhost:8080/kernal-kernel-idgenerator-vid/uin/DEV")`<br/>
                 `		.put("timeout", 10000)));`<br/>


3. Once the setup is done we can use the ConfigRetriever class object to fetch the configuration as follows:<br/>
        `/**`<br/>
         `* ConfigRetriever object to retrieve the configuration stored`<br/>
         `*/`<br/>
        `ConfigRetriever retriever = ConfigRetriever.create(vertx, options);`<br/>
        `retriever.getConfig(ar -> {`<br/>
         `   if (ar.succeeded()) {`<br/>
          `  	/**`<br/>
           ` 	 * All the configuration is stored in this configuration object, we can use it anywhere`<br/>
            `	 * to fetch the values by providing the keys`<br/>
            `	 */`<br/>
             `   this.configuration = ar.result();`<br/>
              `  future.complete();`<br/>
            `} else {`<br/>
             `   LOG.error("Failed to read configuration", ar.cause());`<br/>
              `  future.fail(ar.cause());`<br/>
            `}`<br/>
        `});`<br/>
         `return future;`<br/>
    ` }`<br/>
4. Letâ€™s assume I put port number in which the application will be running in the properties file, and I need to get that port value while initiating the application, I can get it as follows:<br/>
       ` Integer port = Integer.parseInt(configuration.getString("port"));`<br/>
        `server = vertx.createHttpServer()`<br/>
        		`.requestHandler(req -> `<br/>
        			`	req.response().end("I am running on the port fetched from the configuration "`<br/>
        						`+ "stored in Spring config server")).listen(port);`<br/>



**NOTE:** <br/>**Whenever there is a change in the configuration in GIT Repo, every microservice/application which  is using that particular configuration has to call the refresh endpoint in order to get that latest configuration without restarting. If the client doesnt call the refresh API, it will keep on getting the old configuration.** <br/>
The refresh end point is following:<br/>
**POST  {Microservice-URL} /actuator/refresh**

**To Encrypt any property:** <br/>
Run the following command : <br/>
`curl http://<spring_security_username_env>:<spring_security_password_env>@<your-config-server-hostname>:<your-config-server-port>/encrypt -d <value-to-encrypt>`

And place the encrypted value in client application properties file with the format: <br/>
`password={cipher}<encrypted-value>`

**To Decrypt any property manually:** <br/>

`curl http://<spring_security_username_env>:<spring_security_password_env>@<your-config-server-hostname>:<your-config-server-port>/decrypt -d <encrypted-value-to-decrypt>`

**NOTE** There is no need to write decryption mechanism in client applications for encrypted values. They will be automatically decrypted.




