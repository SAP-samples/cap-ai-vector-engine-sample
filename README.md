# CAP with SAP HANA Vector Engine & SAP Core AI

[![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/cap-ai-vector-engine-sample)](https://api.reuse.software/info/github.com/SAP-samples/cap-ai-vector-engine-sample)

## Description
This repository contains a code sample on how to build a Cloud Application Programming Model application exposing functionality of SAP AI Core and SAP HANA Cloud Vector Engine using the CAP LLM Plugin. The code also shows how a developer can leverage vector embeddings to train an LLM on your very own business context.

For more information about the end-to-end scenario, take a look at the [architecture documentation](/doumentation/architecture.md).

## Requirements
* A suitable IDE like Visual Studio Code or Neovim
* Install the [Cloud Foundry CLI](https://developers.sap.com/tutorials/cp-cf-download-cli.html)
* Install the [hana-cli](https://github.com/SAP-samples/hana-developer-cli-tool-example) (optional)
* Create an [SAP BTP account](https://help.sap.com/docs/btp/sap-business-technology-platform/trial-accounts-and-free-tier)
* Create an instance of [SAP HANA Cloud](https://developers.sap.com/tutorials/hana-cloud-deploying.html).
* Create an instance of [SAP AI Core](https://help.sap.com/docs/sap-ai-core/sap-ai-core-service-guide/create-service-instance)
* Create [deployments](https://help.sap.com/docs/sap-ai-core/sap-ai-core-service-guide/create-deployment-for-generative-ai-model-in-sap-ai-core) for model support ChatCompletion `gpt-35-turbo or gpt-4` and embedding model `text-embedding-ada-002`
* Create a [destination](https://help.sap.com/docs/btp/sap-business-technology-platform/create-destination) for Generative AI Hub in the SAP BTP Cockpit of your subaccount based on the Service Key of SAP AI Core:
```
Name: GENERATIVE_AI_HUB
Description: SAP AI Core deployed service (generative AI hub)
URL: <AI-API-OF-AI-CORE-SERVICE-KEY>/v2 # make sure to add /v2!
Type: HTTP
ProxyType: Internet
Authentication: OAuth2ClientCredentials
tokenServiceURL: <TOKEN-SERVICE-URL-OF-AI-CORE-SERVICE-KEY>/oauth/token
clientId: <YOUR-CLIENT-ID-OF-AI-CORE-SERVICE-KEY>
clientSecret: <YOUR-CLIENT-SECRET-OF-AI-CORE-SERVICE-KEY>
# Additional Properties:
URL.headers.AI-Resource-Group: default # adjust if necessary
URL.headers.Content-Type: application/json
HTML5.DynamicDestination: true
```
* The SAP BTP account needs the following entitlements:

| Name              | Service/Application | Plan |
| :---------------- | :------ | :---- |
| AI Core        |   `aicore`   | `extended` |
| AI Launchpad           |   `ai-launchpad`   | `standard` |
| HANA Cloud    |  `hana-cloud`   | `hana` |

## Download and Installation
1. Clone this GitHub repository to your local machine and open it in VS Code or any other suitable editor.
2. Run `npm install` in the root to install all dependencies
3. Connect to your SAP BTP subaccount:  
`cf login -a <subaccount-endpoint>`
4. Bind the following services to the application:  
    - SAP Hana Cloud  
    `cds bind --to <hana-service-instance>:default  `
    - SAP BTP, Destination Service  
    `cds bind --to <destination>  `
5. Build the database artifacts for the SAP HANA Cloud deployment:  
`cds build --for hana`
6. Deploy database artifacts to SAP HANA Cloud:  
`cds deploy --to hana:<hana-service-instance>`
7. For [hybrid testing](https://cap.cloud.sap/docs/advanced/hybrid-testing) execute:  
`cds watch --profile hybrid`

## How to use the application
To properly run through the use case there are four API endpoints you can call which can be found in the [API Documentation](documentation/api-documentation.md).

There are two services defined in this CAP application:

* The **Embedding Storage**; includes the input text chunking, creation of vector embeddings, storing and deletion of the vector embeddings in the SAP HANA Cloud vector engine.
* The **Roadshow Service**; includes calls for retrieving the RAG response and execution of a similarity search.

## Further Information
* [CAP LLM Plugin samples](https://github.com/SAP-samples/cap-llm-plugin-samples/)
* [CAP LLM Plugin npm](https://www.npmjs.com/package/cap-llm-plugin)
* [CAP Vector Embeddings](https://cap.cloud.sap/docs/guides/databases-hana#vector-embeddings)
* [Retrieval Augmented Generation with GenAI on SAP BTP](https://discovery-center.cloud.sap/refArchDetail/ref-arch-open-ai)
* [What is SAP AI Core?](https://help.sap.com/docs/sap-ai-core/sap-ai-core-service-guide/what-is-sap-ai-core)
* [Combine the Power of AI with Business Context Using SAP HANA Cloud Vector Engine](https://news.sap.com/2024/04/sap-hana-cloud-vector-engine-ai-with-business-context/)

## Known Issues
No known issues.

## How to obtain support
[Create an issue](https://github.com/SAP-samples/<repository-name>/issues) in this repository if you find a bug or have questions about the content.
 
For additional support, [ask a question in SAP Community](https://answers.sap.com/questions/ask.html).

## Contributing
If you wish to contribute code, offer fixes or improvements, please send a pull request. Due to legal reasons, contributors will be asked to accept a DCO when they create the first pull request to this project. This happens in an automated fashion during the submission process. SAP uses [the standard DCO text of the Linux Foundation](https://developercertificate.org/).

## License
Copyright (c) 2024 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSE) file.
