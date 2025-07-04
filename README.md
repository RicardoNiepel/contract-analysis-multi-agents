# Contract Analysis Multi-Agent Sample Using Azure AI Agent Service And Semantic Kernel

C# and multi-agent version of the original https://github.com/azure-ai-foundry/foundry-samples/tree/main/samples/agent-catalog/msft-agent-samples/semantic-kernel-sdk/contract-analysis-agent

## Overview 

This code sample enables created of a contract analysis agent, implemented with Azure AI Agent Service and Semantic Kernel, which reviews multiple versions of a contract and generates a detailed and structured report that highlights the differences. The markdown report mirrors the structure of the contracts to ensure readability and makes it easy for the reviewer to understand the differences.

The agent's capabilities include: 

* **Contract Comparison**: Compares two versions of a contract to identify changes in key fields and clauses. Uses specialized tools and techniques to extract relevant information from them. 
* **Report Generation**: Generates a detailed report on the differences between the two versions of a contract. Formats reports using Markdown to ensure clarity and readability. Organizes content with headings, subheadings, bullet points, and numbered lists. 
* **Communication**: Communicates findings to the reviewer in a clear and concise manner.

This Azure AI Agent Service agent uses the Azure AI Content Understanding for transcription of PDF contacts to markdown, contract analysis, and content extraction.

**WARNING:** An agent created using this code sample is only intended to help with identifying differences between two documents.  It in no way replaces the need for obtaining legal advice from an accredited attorney with respect to any contract.

## Sample Data

Example of the Standard Operating Procedure generated by the agent is located in the [assets folder](assets/output/sample_output.md). This response was generated from sample contracts located in [the input folder](assets/input).

## Getting Started

### Prerequisites

* [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) or later

### Instructions

#### Step 0: Deploy Azure services

**Prerequisites**
1. To deploy the template, you must have the following roles:
    * **Azure AI Account Owner** or **Contributor** 
1. To create your first agent you must have the permissions:
    * **Azure AI User**

For more information, [see the getting started guide.](https://learn.microsoft.com/en-us/azure/ai-services/agents/environment-setup)
 
**Steps**

* Create new (or use existing) resource group:

```bash
    az group create --name <new-rg-name> --location eastus
```

* Deploy the template

```bash
    az deployment group create --resource-group <new-rg-name> --template-file infra/basic-setup.bicep
```

#### Step 1: Create Azure AI Content Understanding Resource

[Follow the official documentation](https://learn.microsoft.com/azure/ai-services/content-understanding/how-to/create-multi-service-resource) to create an Azure AI Services resource that supports Content Understanding.

#### Step 2: Create Deployment Model

[Follow the official documentation](https://learn.microsoft.com/azure/ai-foundry/quickstarts/get-started-playground#deploy-a-chat-model) to create an Azure AI Foundry model deployment.

#### (Optional) Step 3: Create Azure AI Agent Service Agent

*This step is optional. If you don't create an Azure AI Agent, the program will create one for you automatically.*

1. Follow the official [Azure AI Agent Service documentation](https://learn.microsoft.com/azure/ai-services/agents/quickstart?pivots=ai-foundry-portal) to create the claims analysis agent (a chat completion agent). 
2. In the **Instructions** box, paste the contents of [AgentInstructions.md file](assets/input/AgentInstructions.md).

#### Step 4: Configure Application Settings

Configure the application settings in `src/appsettings.json` and `src/appsettings.Development.json` with your Azure resource information.

```json
{
    "Settings": {
        "ContractPolicyAgentInstructionsPath": "../assets/input/ContractPolicyAgentInstructions.md",
        "ContractPolicyAgentId": "",
        "ContractAnalysisAgentInstructionsPath": "../assets/input/ContractAnalysisAgentInstructions.md",
        "ContractAnalysisAgentId": "",
        "AzureAiAgentEndpoint": "https://demo.services.ai.azure.com/api/projects/project",
        "AzureAiAgentModelDeploymentName": "gpt-4o",
        "AzureAiCuSchemaFilePath": "../assets/input/ContractSchema.json",
        "AzureAiCuEndpoint": "https://demo.services.ai.azure.com/",
        "AzureAiCuApiVersion": "2024-12-01-preview",
        "AzureAiCuSubscription": ".."
    }
}
```

#### Step 5: Build and Run the Application

Navigate to the src directory and run the application:

```sh
cd src
dotnet build
dotnet run
```

## Resources

* Semantic Kernel [documentation](https://learn.microsoft.com/semantic-kernel/overview/) and [GitHub repo with source code](https://github.com/microsoft/semantic-kernel)
* [Azure AI Agent Service documentation](https://learn.microsoft.com/azure/ai-services/agents/)
* [Azure AI Content Understanding documentation](https://learn.microsoft.com/azure/ai-services/content-understanding/)
* [Azure AI Foundry documentation](https://learn.microsoft.com/azure/ai-foundry/)
