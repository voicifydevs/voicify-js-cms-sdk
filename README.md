# Introduction 

TODO

# Getting Started

TODO

# Build and Test
This project contains core models for all Voicify integrations including API models and other custom models.
There are some steps to autogenerate the TypeScript models from the swagger API models that Voicify outputs.

## Generate Models from Swagger

Sample:

```
java -jar swagger-codegen-cli.jar generate -i http://cms.voicify.com/swagger/v1/swagger.json -l typescript-node -c ../typescript-options.json -o ../../src/generated
```
