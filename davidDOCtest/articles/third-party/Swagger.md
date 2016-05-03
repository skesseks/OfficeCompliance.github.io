Swagger is a framework for documentation and discovery of a RESTful API, used by default in API Apps. For more information, see http://swagger.io/.
### How Azure API uses Swagger
- [App Service API Apps metadata for API discovery and code generation](https://azure.microsoft.com/en-gb/documentation/articles/app-service-api-metadata/):
    - Support for Swagger 2.0 API metadata is built into App Service API Apps. You don't have to use Swagger, but if you do use it, you can take advantage of API Apps features that make discovery and consumption easier. 

    - **Swagger endpoint**: You can specify an endpoint that provides Swagger 2.0 JSON metadata for an API app in a property of the API app. The endpoint can be relative to the base URL of the API app or an absolute URL. Absolute URLs can point outside the API app. 

    - Many downstream clients (for example, Visual Studio code generation and PowerApps "Add API" flow), the ...
- [Video: Manage code changes to Web Apps using the DevOps features of Azure App Service and Visual Studio Release Management](https://azure.microsoft.com/en-gb/documentation/videos/azurecon-2015-manage-code-changes-to-web-apps-using-the-devops-features-of-azure-app-service-and-visual-studio-release-management/) - Guessing this gives a workflow of how Swagger works and how it generates code, etc.
