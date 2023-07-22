# azure-open-ai-batch-demo
A demo on how to run Azure OpenAI generation batch jobs on ACA

## Prerequisites

- Python 3.6 or later

- Azure CLI

- Azure Service Bus namespace (Will be created by the `setup.sh` script if it doesn't already exist)

## Setup

1\. Clone the repository:

   ```
   git clone https://github.com/Azure-Samples/azure-open-ai-batch-demo.git
   ```

2\. Create a Service Bus namespace and two queues:

   `./setup.sh`

   This script creates a new resource group, Service Bus namespace, and two queues (`pendingPrompts` and `generatedPrompts`) if they don't already exist. It also outputs the connection string for the Service Bus namespace.

3\. Set the `SERVICE_BUS_CONN_STR` environment variable:

   `export SERVICE_BUS_CONN_STR=<your-connection-string>`

   Replace `<your-connection-string>` with the connection string output by the `setup.sh` script.

4\. Install the Python dependencies:

   `pip install -r requirements.txt`

## Usage

1\. Send prompts to the `pendingPrompts` queue:

   `python send_prompts.py`

   This script reads a list of services from `azure-services.txt` and sends a prompt for each service to the `pendingPrompts` queue.

2\. Generate responses using Azure OpenAI:

   `python generate_responses.py`

   This script reads prompts from the `pendingPrompts` queue, generates responses using Azure OpenAI, and writes the responses to `generated-responses.txt`.