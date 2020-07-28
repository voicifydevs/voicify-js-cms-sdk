# Introduction 
This project includes the models and API methods for interacting with the Voicify CMS API for JavaScript and TypeScript.

# Getting Started

You can install the package from npm:

```
npm i -s @voicify/voicify-sdk-cms
```

If you're using TypeScript, all the types are included, so you don't need to install any additional packages.


Each service has its own API class, factory, or functional composer to use in order to make requests against it. 

## Authentication

Currently, you'll need to authenticate an API user against your Voicify organization to get an Access token to start making requests against the API.

To do this, you can create a new `AuthenticationApi` client and then send a request to authenticate your API account:

```typeScript
var authClient = new AuthenticationApi({basePath: "https://cms.voicify.com"});

var tokenInfo = await authClient.authenticate("your-organization-id", "your-organization-secret", "password", "your-api-user-name", "your-api-user-password");
var accessToken = tokenInfo.accessToken;

// you can also refresh your token
var refreshedTokenInfo = await authClient.authenticate("your-organization-id", "your-organization-secret", "refresh_token", "your-api-user-name", null, "your-refresh-token");
var newAccessToken = refreshedTokenInfo.accessToken;

// these access tokens are used on subsequent requests to the API

```

## Making Requests

Once you have an access token, you can start to make requests against your organization and the apps within it. For example, we can use the previous `accessToken` variable to authenticate and create a new welcome message.

```typeScript
var welcomeMessageClient = new WelcomeMessageApi({
    basePath = "https://cms.voicify.com",
    apiKey = `Bearer ${accessToken}` 
    }
});
const newWelcomeMessage = await welcomeMessageClient.createFullContentItem({
    title: "New welcome message",
    applicationId: "an-app-id",
    applicationFeatureId: "an-app-feature-id",
    content: "Welcome to my app! I made this from the Voicify SDK!"
});
```

Voicify Partners and Customers can also check out the extended documentation and details at https://support.voicify.com

# Contributing

The Voicify core development team owns this repo and NuGet package, but all Voicify developers are welcome to contribute changes. Before contributing, please create an issue that you can track your PRs against and be sure there is not already a PR open for it.

# Build and Test
There are some steps to autogenerate the TypeScript models from the swagger API models that Voicify outputs.

## Generate Models from Swagger

Sample:

```
java -jar swagger-codegen-cli.jar generate -i http://cms.voicify.com/swagger/v1/swagger.json -l typescript-fetch -c ../typescript-options.json -o ../../src/generated
```

## Build output

Navigate to the generated folder where the package.json is and run:

```
npm install
```

then

```
npm run build
```

