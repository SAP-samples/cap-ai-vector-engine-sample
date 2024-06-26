
# Architecture Overview

## CAP LLM Plugin

![End2End Architecture of CAP & SAP AI Core](/doumentation/diagrams/CAP%20LLM%20BD.png)

Within the CAP service, the CAP LLM Plugin can be used not only to connect to the SAP AI Core or SAP HANA Cloud Vector Engine but also to execute operations like anonymization of data, creation of embeddings, executing similarity search, chat completion, and RAG responses. The plugin mainly is responsible for establishing connection using configuration information within the CAP application and creating the needed HTTP requests.
The plugin is available as [npm package](https://www.npmjs.com/package/cap-llm-plugin), the documentation and samples are available on [GitHub](https://github.com/SAP-samples/cap-llm-plugin-samples/tree/main) and the plugin is currently in beta (not suitable for production use cases yet).

## End-to-End Scenario

![End2End Architecture of CAP & SAP AI Core](/doumentation/diagrams/CAPLLM_End2End_Architecture_Simple.png)

A CAP application is connected to an SAP HANA Cloud instance on the SAP Business Technology Platform (BTP). The application is interacting with the SAP HANA Cloud Vector Engine to store and retrieve vector embeddings. The CAP LLM Plugin is responsible for creating the HTTP requests and establish connection to SAP HANA Cloud and SAP Gen AI Hub. 
To establish a connection between the CAP application and SAP Gen AI Hub, it is necessary to define the connection details in a SAP BTP destination using the Destination Service. The destination can be created on BTP account level or directly in the subaccount. Because the CAP application is being deployed in the SAP BTP, Cloud Foundry runtime (CF), a destination is being created within the CF development space of the subaccount.
Through the help of bindings, the CAP application will have the correct configurations to resolve the connections to SAP HANA Cloud as well as the destination service which respectively routes HTTP requests through to the SAP AI Core APIs. A configuration for which embedding model and for which chat completion model to use is being configured within the CAP application as well. The needed information can be found in the SAP Gen AI Hub.
If a request is being sent from the CAP application to the SAP AI Core for creating embeddings or retrieving a RAG response, the requests get routed through the destination to SAP AI Core. SAP AI Core is routing the requests through to the partner foundation models and returns the response back to the CAP application.
