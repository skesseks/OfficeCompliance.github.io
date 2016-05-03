This looks very interesting because it ties Swagger and [ApiExplorer](https://github.com/OfficeCompliance/vNext-Investigations/wiki/Visual-Studio-Documentation-Features/_edit#apiexplorer) together...

[Swashbuckle 5.0](https://github.com/domaindrivendev/Swashbuckle) Seamlessly adds a Swagger to WebApi projects! Combines ApiExplorer and Swagger/swagger-ui to provide a rich discovery, documentation and playground experience to your API consumers.

In addition to its Swagger generator, Swashbuckle also contains an embedded version of swagger-ui which it will automatically serve up once Swashbuckle is installed. This means you can complement your API with a slick discovery UI to assist consumers with their integration efforts. Best of all, it requires minimal coding and maintenance, allowing you to focus on building an awesome API! Once you have a Web API that can describe itself in Swagger, you've opened the treasure chest of Swagger-based tools including a client generator that can be targeted to a wide range of popular platforms. See [swagger-codegen](https://github.com/swagger-api/swagger-codegen) for more details

**Swashbuckle Core Features:**
* Auto-generated Swagger 2.0
* Seamless integration of swagger-ui
* Reflection-based Schema generation for describing API types
* Extensibility hooks for customizing the generated Swagger doc & swagger-ui
* Out-of-the-box support for leveraging Xml comments
* Support for describing ApiKey, Basic Auth and OAuth2 schemes 
* Support for documenting **multiple versions of the API**