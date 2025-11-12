# Complete Tutorial for Using ERNIE Models in CAMEL AI

This tutorial will teach you how to use Baidu Qianfan Platform's ERNIE models within the CAMEL AI framework, including basic configuration, single agent usage, and multi-agent role-playing functionality.

## Prerequisites

### 1. Install Dependencies
Ensure you have installed CAMEL AI and related dependencies:

```bash
pip install camel-ai
```

### 2. Obtain Qianfan Platform API Keys
1. Visit [Baidu Intelligent Cloud Qianfan Large Model Platform](https://console.bce.baidu.com/qianfan/overview)
2. Register an account and create an application
3. Obtain your `API Key` and `Secret Key`

### 3. Environment Variable Configuration
Set the following environment variable:

```bash
export QIANFAN_API_KEY="bce-v3/ALTAK-kSLlvFK3grkPJkfw7kuq7/ea9129f801d0639d6f9dabbb4c39ae875022be95"
```

Alternatively, configure directly in code (not recommended for production environments).

## Basic Usage: Single Agent

### 1. Import Required Modules

```python
from camel.agents import ChatAgent
from camel.configs import QianfanConfig
from camel.models import ModelFactory
from camel.types import ModelPlatformType, ModelType
```

### 2. Create ERNIE Model Instance

```python
# Create ERNIE 4.5 model configuration
model = ModelFactory.create(
    model_platform=ModelPlatformType.QIANFAN,  # Specify Qianfan platform
    model_type=ModelType.ERNIE_4_5_TURBO_128K,  # Select ERNIE 4.5 Turbo 128K model
    model_config_dict=QianfanConfig(temperature=0.2).as_dict(),  # Configure temperature parameter
)
```

### 3. Create Agent and Conduct Conversation

```python
# Define system message
sys_msg = "You are a helpful assistant."

# Set up agent
camel_agent = ChatAgent(system_message=sys_msg, model=model)

# User message
user_msg = """Say hi to CAMEL-AI, one open-source community believe that
scaling up multi-agent systems is a pathway toward AGI. It's mission is:
Finding the Scaling Laws of Agents. Intelligence emerges from diversity, not a
single perfect principle. Multi-agent systems naturally follow "divide and
conquer" approaches, breaking down complex problems across multiple
specialized agents. Since 2023, they have been building the first multi-agent
framework CAMEL"""

# Get response
response = camel_agent.step(user_msg)
print(response.msgs[0].content)
```

### 4. Complete Single Agent Example

```python
from camel.agents import ChatAgent
from camel.configs import QianfanConfig
from camel.models import ModelFactory
from camel.types import ModelPlatformType, ModelType

def single_agent_example():
    # Create model
    model = ModelFactory.create(
        model_platform=ModelPlatformType.QIANFAN,
        model_type=ModelType.ERNIE_4_5_TURBO_128K,
        model_config_dict=QianfanConfig(temperature=0.2).as_dict(),
    )

    # Create agent
    camel_agent = ChatAgent(
        system_message="You are a helpful assistant.",
        model=model
    )

    # Conduct conversation
    user_message = "Please introduce the development history of artificial intelligence"
    response = camel_agent.step(user_message)

    print("AI Response:", response.msgs[0].content)

if __name__ == "__main__":
    single_agent_example()
```