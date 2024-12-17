# **Azure AI Services**

Think of AI as software that exhibits one or more human-like capabilities.
1. **Visual perception** - The ability to use computer vision capabilities to accept, interpret, and process input from images, video streams, and live cameras.
2. **Text analysis and conversation** - The ability to use natural language processing (NLP) to not only "read", but also generate realistic responses and extract semantic meaning from text.
3. **Speech** - The ability to recognize speech as input and synthesize spoken output. The combination of speech capabilities together with the ability to apply NLP analysis of text enables a form of human-compute interaction that's become known as conversational AI.
4. **Decision making** - The ability to use past experience and learned correlations to assess situations and take appropriate actions. For example, recognizing anomalies in sensor readings and taking automated action to prevent failure or system damage.

**AI-related terms**
1. **Data science**: Data science is an interdisciplinary field that focuses on the processing and analysis of data; applying statistical techniques to uncover and visualize relationships and patterns in the data, and defining experimental models that help explore those patterns. Data scientist might gather samples of data about the population of an endangered species in a geographical area, and combine it with data about levels of industrialization and economic demographics in the same area.
2. **Machine learning**: Data scientists often work with machine learning models. Machine learning deals with the training and validation of predictive models. Typically, a data scientist prepares the data and then uses it to train a model based on an algorithm that exploits the relationships between the features in the data to predict values for unknown labels. **Use factors**: such as the number of nesting sites observed, the area of land designated as protected, the human population in the local area, the daily volume of traffic on local roads, and so on. **evaluate plan**: for housing, infrastructure, and industrial development in the local area and assess their likely impact on the local wildlife
3. **Artificial intelligence**: Artificial intelligence (AI) describes software that emulates one or more characteristics of human intelligence. Machine learning is a prominent approach used to create AI software. Knowledge of data science can support an understanding of artificial intelligence. **a predictive model** could be trained to analyze image data taken by motion-activated cameras in remote locations, and predict whether a photograph contains a sighting of the animal

After the model has been trained, you can submit new data that includes known feature values and have the model predict the most likely label. Using the model to make predictions is referred to as **inferencing**.
Software developers should make use of **confidence score** values to evaluate predictions and apply appropriate thresholds to optimize application reliability and mitigate the risk of predictions that may be made based on marginal probabilities.
software engineers building AI-enabled solutions should apply due consideration to **mitigate risks and ensure fairness, reliability, and adequate protection from harm or discrimination.**
Responsible AI: Fairness, Reliability and safety, Privacy and Security, Inclusiveness, Transparency, Accountability.

**Automated machine learning**: This feature enables **non-experts to quickly create an effective machine learning model** from data.
**Azure Machine Learning designer**:	A graphical interface enabling **no-code development** of machine learning solutions.
**Data and compute management**: **Cloud-based data storage and compute resources** that professional data scientists can use to run data experiment code at scale.
**Pipelines**:	Data scientists, software engineers, and IT operations professionals can define pipelines to **orchestrate model training, deployment, and management tasks**.

Software engineers may interact with Azure Machine Learning in the following ways:
1. Using Automated Machine Learning or Azure Machine Learning designer to train machine learning models and deploy them as services that can be integrated into AI-enabled applications.
2. Collaborating with data scientists to deploy models based on common frameworks such as Scikit-Learn, PyTorch, and TensorFlow as web services, and consume them in applications.
3. **Using Azure Machine Learning SDKs or command-line interface (CLI) scripts** to orchestrate DevOps processes that manage versioning, deployment, and testing of machine learning models as part of an overall application **delivery solution**.

![image](https://github.com/user-attachments/assets/1051515f-9d20-487f-9a61-2c7166480826)

Azure OpenAI Service is an Azure AI service for deploying, utilizing, and fine-tuning models developed by OpenAI. AI engineers can develop applications that use the powerful generative AI models in Azure OpenAI to further utilize this technology. Both REST and language specific SDKs are available when developing applications.

In addition to basic text-based indexing, Azure AI Search enables you to define an **enrichment pipeline** that uses AI skills to enhance the index with insights derived from the source data - for example, by using computer vision and natural language processing capabilities to generate descriptions of images, extract text from scanned documents, and determine key phrases in large documents that encapsulate their key points.

Not only does this AI enrichment produce a more useful search experience, **the insights extracted by your enrichment pipeline can be persisted in a knowledge store for further analysis or integration into a data pipeline for a business intelligence solution**.

To consume the service through the endpoint, applications require the following information:
1. **The endpoint URI**. This is the HTTP address at which the REST interface for the service can be accessed.
2. **A subscription key**. Client applications must provide a valid key to consume the service. When you provision an AI services resource, two keys are created - applications can use either key.
3. **The resource location**. When you provision a resource in Azure, you generally assign it to a location, which determines the Azure data center in which the resource is defined. While most SDKs use the endpoint URI to connect to the service, some require the location.
-----
##Secure Azure AI services
You can regenerate **subscription keys** using the Azure portal, or using the az cognitiveservices account keys regenerate Azure command-line interface (CLI) command.

**Token-based authentication**
When using the REST interface, some AI services support (or even require) token-based authentication. In these cases, the subscription key is presented in an initial request to obtain an authentication token, which has a valid period of 10 minutes. Subsequent requests must present the token to validate that the caller has been authenticated. When using an SDK, the calls to obtain and present a token are handled for you by the SDK.
**Microsoft Entra ID authentication**
Azure AI services supports Microsoft Entra ID authentication, enabling you to grant access to specific service principals or managed identities for apps and services running in Azure.
**Authenticate using service principals**
1. Create a custom subdomain
2. Assign a role to a service principal
3. Authenticate using managed identities

az ad sp create-for-rbac -n "api://ai-app-ta0011" --role owner --scopes subscriptions/9937e55a-6e56-470d-83d7-a31e3f5e27bb/resourceGroups/rg-01
{
    "appId": "abcd12345efghi67890jklmn",
    "displayName": "api://ai-app-",
    "password": "1a2b3c4d5e6f7g8h9i0j",
    "tenant": "1234abcd5678fghi90jklm"
}

az ad sp show --id <appId-use-from-above>

az keyvault set-policy -n <keyVaultName> --object-id <objectId-use-from-above> --secret-permissions get list

**Apply network access restrictions**
By default, Azure AI services are accessible from all networks. Some individual AI services resources (such as Azure AI Face service, Azure AI Vision, and others) can be configured to restrict access to specific network addresses - either public Internet addresses or addresses on virtual networks.
