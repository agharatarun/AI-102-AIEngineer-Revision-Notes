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

-----
## Monitor Azure AI services
To create an alert rule for an Azure AI services resource, select the resource in the Azure portal and on the Alerts tab, add a new alert rule. To define the alert rule, you must specify:

* The scope of the alert rule - in other words, the resource you want to monitor.
* A condition on which the alert is triggered. The specific trigger for the alert is based on a signal type, which can be Activity Log (an entry in the activity log created by an action performed on the resource, such as regenerating its subscription keys) or Metric (a metric threshold such as the number of errors exceeding 10 in an hour).
* Optional actions, such as sending an email to an administrator notifying them of the alert, or running an Azure Logic App to address the issue automatically.
* Alert rule details, such as a name for the alert rule and the resource group in which it should be defined.

In the case of Azure AI services, Azure Monitor collects metrics relating to endpoint requests, data submitted and returned, errors, and other useful measurements.
Diagnostic logging enables you to capture rich operational data for an Azure AI services resource, which can be used to analyze service usage and troubleshoot problems. **Diagnostic settings enable you to capture data for subsequent analysis**.

To capture diagnostic logs for an AI services resource, you need a destination for the log data. You can use Azure Event Hubs as a destination in order to then forward the data on to a custom telemetry solution, and you can connect directly to some third-party solutions; but in most cases you'll use one (or both) of the following kinds of resource within your Azure subscription:

Azure Log Analytics - a service that enables you to query and visualize log data within the Azure portal.
Azure Storage - a cloud-based data store that you can use to store log archives (which can be exported for analysis in other tools as needed). create the Azure Storage account in the same region as your AI services resource.

-----
## Deploy Azure AI services in containers

Language containers, Speech containers, Vision containers
Azure AI services container images example. Complete list can be found at: https://learn.microsoft.com/en-us/training/modules/investigate-container-for-use-with-ai-services/3-use-ai-services-container

mcr.microsoft.com/azure-cognitive-services/textanalytics/keyphrase
mcr.microsoft.com/**product**/azure-cognitive-services/textanalytics/language/**about**

You can use the Docker pull command to download container images to work with them directly from your machine. Some of the containers are in a "Gated" public preview state, and you need to explicitly request access to use them. Otherwise the containers are available for anyone to use with their Azure AI services deployment.

When you deploy an Azure AI services container image to a host, you must specify three settings.
ApiKey: Key from your deployed Azure AI service; used for billing.
Billing	Endpoint: URI from your deployed Azure AI service; used for billing.
Eula: Value of accept to state you accept the license for the container.

-----
## Azure AI Content Safety

### Safeguarding text content
1. **Moderate text** scans text across four categories: **violence, hate speech, sexual content, and self-harm**. A **severity level from 0 to 6** is returned for each category. 
2. **Prompt shields** is a unified API to identify and block jailbreak attacks from inputs to LLMs.
3. **Protected material** detection checks AI-generated text for protected text such as recipes, copyrighted song lyrics, or other original material.
4. **Groundedness detection** protects against inaccurate responses in AI-generated text by LLMs. An ungrounded response is one where the model's output varies from the source information. Groundedness detection includes a reasoning option in the API response. This adds a reasoning field that explains any ungroundedness detection. **However, reasoning increases processing time and costs**.

#### Safeguarding image content
1. **Moderate images** scans for inappropriate content across four categories: violence, self-harm, sexual, and hate. **A severity level is returned: safe, low, or high**. You then set a **threshold level of low, medium, or high**. The combination of the severity and threshold level determines whether the image is allowed or blocked for each category.
2. **Moderate multimodal content** scans both images and text, including text extracted from an image using optical character recognition (OCR). Content is analyzed across four categories: violence, hate speech, sexual content, and self-harm.

### Custom safety solutions
1. **Custom categories** enables you to create your own categories by providing positive and negative examples, and training the model. Content can then be scanned according to your own category definitions.
2. **Safety system message** helps you to **write effective prompts** to guide an AI system's behavior.

### Evaluating accuracy
When evaluating how accurately Azure AI Content Safety is for your situation, compare its performance against four criteria:

True positive - correct identification of harmful content.
False positive - incorrect identification of harmful content.
True negative - correct identification of harmless content.
False negative - harmful content isn't identified.

-----
## Notes: 

* The task of a conversational language model is to predict the user's intent and identify any entities to which the intent applies. It is not the job of a conversational language model to actually perform the actions required to satisfy the intent. For example, a clock application can use a conversational language model to discern that the user wants to know the time in London; but the client application itself must then implement the logic to determine the correct time and present it to the user.

* Speech Synthesis Markup Language (SSML) enables you to customize the way your speech is synthesized using an XML-based format.

* search solution that consists of the following components:
A data source that references the documents in your Azure storage container.
A skillset that defines an enrichment pipeline of skills to extract AI-generated fields from the documents.
An index that defines a searchable set of document records.
An indexer that extracts the documents from the data source, applies the skillset, and populates the index.
