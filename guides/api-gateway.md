# API Gateway & Router Service

Alter provides an OpenAI-compatible API endpoint that allows you to use Alter as a unified router for accessing 92+ AI models from 10+ providers. Use the Alter API either as a backend for third-party applications or as a direct API service for your custom projects.

## Overview

The Alter API gateway is a centralized router that eliminates the need to manage multiple API keys and billing accounts across different AI providers. Instead of having your billing details scattered across many providers, you can use Alter as your single entry point for AI model access.

### What is Alter Router?

Alter itself is a **router service**—a unified API gateway providing access to:
- 10+ AI model providers (OpenAI, Gemini, Claude, Mistral, etc.)
- 92+ individual AI models
- Simplified authentication and billing
- Easy model switching without code changes

## Key Features

- **OpenAI-compliant endpoint** supporting chat completions and model listing
- **Centralized billing** through your Alter account
- **Access to all models** from external applications or custom code
- **Seamless integration** with existing OpenAI-compatible tools and SDKs
- **Flexible model selection** across all providers

## Getting Started

### 1. Generate API Key

1. Open Alter Settings (**⌘ ,** or Settings menu)
2. Go to **Router** tab
3. Under "Alter API Keys" section, click "Add New Key" to generate a new API key
4. Copy your key (starts with `sk-`)

**Important:** Never share your API key. Treat it like a password.

### 2. Get the Endpoint

The Alter router endpoint is:
```
https://alterhq.com/api
```

For some tools, you may need to add `/v1`:
```
https://alterhq.com/api/v1
```

### 3. List Available Models

Check what models are available:

```bash
curl https://alterhq.com/api/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

This returns all 92+ models across 10 providers with their capabilities.

## Model Naming Convention

When using the Alter API, model names follow this format:
```
<Provider>#<Model-name>
```

### Examples:
- `OpenAI#gpt-4o` - Latest GPT-4O
- `OpenAI#gpt-4o-mini` - Lightweight GPT
- `Claude#claude-sonnet-4-6` - Latest Claude
- `Gemini#gemini-2.5-pro` - Latest Gemini
- `Mistral#mistral-small-latest` - Mistral model
- `Alter#best` - Alter's best model

## Usage Methods

### For Third-Party Applications

Use Alter as a backend for tools like SillyTavern, NovelCrafter, etc.:

1. Set base URL: `https://alterhq.com/api` (or `/v1`)
2. Enter your API key
3. Use `Provider#Model-name` format when selecting models

### For Custom Development

#### Python (with OpenAI SDK)

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://alterhq.com/api/v1"
)

response = client.chat.completions.create(
    model="OpenAI#gpt-4o",
    messages=[
        {"role": "user", "content": "What is machine learning?"}
    ]
)

print(response.choices[0].message.content)
```

#### JavaScript (with OpenAI SDK)

```javascript
import OpenAI from 'openai';

const openai = new OpenAI({
    apiKey: "YOUR_API_KEY",
    baseURL: "https://alterhq.com/api/v1",
    dangerouslyAllowBrowser: true
});

const completion = await openai.chat.completions.create({
    model: "OpenAI#gpt-4o",
    messages: [
        {"role": "user", "content": "Hello!"}
    ]
});

console.log(completion.choices[0].message.content);
```

#### LangChain (Python)

```python
from langchain_openai import ChatOpenAI

chat = ChatOpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://alterhq.com/api/v1",
    model="OpenAI#gpt-4o"
)

response = chat.invoke("What is AI?")
print(response.content)
```

#### Direct cURL

```bash
curl https://alterhq.com/api/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "OpenAI#gpt-4o",
    "messages": [
      {"role": "user", "content": "What is machine learning?"}
    ]
  }'
```

## Model Selection Guide

### For Speed
- `Alter#light` - Lightweight model
- `OpenAI#gpt-4o-mini` - Lightweight GPT
- `Gemini#gemini-2.5-flash-lite` - Fast Gemini

### For Quality
- `Alter#best` - Best available
- `OpenAI#gpt-4o` - Most capable GPT
- `Gemini#gemini-2.5-pro` - Powerful Gemini
- `Claude#claude-sonnet-4-6` - Latest Claude

### For Vision/Images
- `OpenAI#gpt-4o` - Advanced multimodal
- `Gemini#gemini-2.5-pro` - Strong vision
- `Mistral#pixtral-large-latest` - Vision capable

### For Coding
- `OpenAI#gpt-4o` - Excellent code
- `Mistral#codestral-2501` - Code specialist
- `Claude#claude-sonnet-4-6` - Strong coding

### For Cost
- `Alter#fair` - Cost-effective
- `Alter#light` - Cheapest
- `OpenAI#gpt-4o-mini` - Budget GPT

### For Web Search
- `Perplexity#sonar` - Web-aware
- `Perplexity#sonar-pro` - Advanced search

## Supported Parameters

Standard OpenAI API parameters work with Alter:

- `model` - Model ID (required)
- `messages` - Chat messages (required)
- `temperature` - 0.0-2.0 (default: 1.0)
- `max_tokens` - Maximum response length
- `top_p` - Nucleus sampling
- `frequency_penalty` - Penalize repetition
- `presence_penalty` - Encourage new topics

## Popular Use Cases

### Third-Party App Integration
- **[SillyTavern](https://sillytavern.app/)** - Roleplaying chat
- **[NovelCrafter](https://www.novelcrafter.com/)** - Creative writing
- Other OpenAI-compatible tools

### Custom Application Backend
- Internal tools needing AI
- Customer support automation
- Content generation systems
- Data analysis workflows

### Model Comparison & A/B Testing
```python
for model_id in ["OpenAI#gpt-4o", "Claude#claude-sonnet-4-6", "Gemini#gemini-2.5-pro"]:
    # Run same prompt on different models
    # Compare outputs
```

### Cost Optimization
Use cheaper models for high-volume tasks, powerful models for complex queries.

## Configuration

### API Key Management
- Generate and manage API keys through **Settings > Router**
- Keep API keys secure—never share them publicly
- Rotate keys regularly for security
- Use different keys for different environments (dev/prod)

### Usage Limits

The API gateway has fair use limitations:

- **Daily Limit**: 200 requests per day under fair use
- **Throttling**: After exceeding daily limit, requests throttle to 1 per 10 minutes
- **Budget Top-up**: "Top up" your budget for consistent access beyond fair use limits

## Troubleshooting

### Models Not Listed
If your application doesn't list available models:
- Manually specify the model using `Provider#Model-name` format
- Verify your API key is correct
- Check that the application supports model listing endpoint

### Authentication Errors
- Verify your API key is correctly entered
- Ensure you're using correct endpoint: `https://alterhq.com/api` or `https://alterhq.com/api/v1`
- Check that your Alter account is active and in good standing

### Connection Issues
- Verify the application supports OpenAI-compatible endpoints
- Ensure you're using the latest version of Alter
- Check network connectivity to `alterhq.com`

### High Latency
- Try a faster model (e.g., `OpenAI#gpt-4o-mini`)
- Check your network connection
- Use streaming for long responses

## Best Practices

1. **Secure your API key** - Use environment variables, never hardcode
2. **Monitor usage** - Track API calls and set alerts
3. **Choose appropriate models** - Match model capability to task complexity
4. **Handle errors gracefully** - Implement retry logic with backoff
5. **Optimize costs** - Use faster/cheaper models for routine tasks

## Related Docs

- [Choosing Your Model](../guides/choosing-generative-model.md)
- [Settings - Router Configuration](../guides/settings.md#8-router-settings)
- [Settings - API Keys](../guides/settings.md#7-api-keys-settings)
- https://alterhq.com/docs
- https://platform.openai.com/docs/guides/chat-completions (OpenAI API reference)
