## Choosing Your Generative Model


By default, Alter offers a variety of models, listed alphabetically by their hosting company.

You can also use your [API key](#via-your-api-key) or use [your local model](#locally-via-ollama-or-studiolm).

### Choosing your model 

After opening Alter, just type `/` to show available models and select the model you want to use.


#### Chosing a favorite model

Select the star icon next to a model with your mouse to mark the model as your favorite.
![Favoriting a model](https://alterhq.com/assets-doc/images/models/favorite-model.webp)


When using your API key or a local model, these appear at the top under **Custom**.  
All other interactions are routed through Alter Cloud.

### Using Alter Cloud

By default, Alter is set up with `/best` , our internal model router, choosing the best model based on your query.

![Router and model example](https://alterhq.com/assets-doc/images/settings/router.png)


You can change the default model in **Settings > Defaults > Model**.  


#### List of the models via Alter Cloud

Alter provides access to **92+ models across 10 providers** through its unified router. Use the `/models` endpoint to list current models, or see the **[API Gateway Guide](../guides/api-gateway.md)** for detailed model information.

**Provider Overview (as of Beta 71):**

| Provider | Model Count | Example Models |
|----------|-------------|-----------------|
| **Alter** | 4 | `best`, `fair`, `fast`, `light` |
| **Claude** (Anthropic) | 4 | `claude-sonnet-4-6`, `claude-sonnet-4-20250514` |
| **OpenAI** | 17 | `gpt-4o`, `gpt-4o-mini`, `gpt-5`, `o3`, `o4-mini` |
| **Gemini** (Google) | 10 | `gemini-2.5-pro`, `gemini-2.5-flash`, `gemini-3-pro-preview` |
| **Mistral** | 9 | `mistral-small-latest`, `codestral-2501`, `pixtral-large-latest` |
| **Groq** | 7 | Llama, Qwen, and other optimized models |
| **Together** | 26 | DeepSeek, Llama, Qwen, and specialty variants |
| **xAI** | 8 | `grok-3-latest`, `grok-4` series |
| **Cerebras** | 5 | Llama, Qwen, and DeepSeek variants |
| **Perplexity** | 2 | `sonar`, `sonar-pro` (web search capable) |

**Key Model Characteristics:**

| Feature | Models | Context |
|---------|--------|---------|
| **Vision Capable** | GPT-4O, Gemini 2.5+, Claude, Mistral Pixtral | Analyze images/video |
| **Highest Context** | Alter models, Gemini | 1M+ tokens |
| **Fastest** | Alter `light`, GPT-4O mini, Gemini Flash | Low latency |
| **Most Capable** | GPT-4O, Gemini 2.5 Pro, Claude Sonnet | Complex reasoning |
| **Web Search** | Perplexity Sonar | Real-time info |
| **Code Specialist** | Mistral Codestral | Code generation |

**For the complete current list of all 92+ models**, check available models directly through the API:

```bash
curl https://alterhq.com/api/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

Or see the **[API Gateway Guide](../guides/api-gateway.md)** for detailed information on model selection and usage.

### Using Your API Key

![Custom Local](https://alterhq.com/assets-doc/images/models/custom-api-keys.webp)

You can use your own API key to connect directly to your provider's endpoint:  
1. Go to **Settings > API keys > Custom provider**.  
2. Enable Custom Provider
3. Pick your provider in the list

> Once connected, a tick will appear next to **Custom Endpoint**.  

Your provider's models will be listed under the **Custom** section.

> We only support OpenAI compatible endpoints meaning you can't use your Anthropic API keys.

Here's a list of the supported platforms for custom keys, based on the provided image:

1.  Azure
2.  Gemini
3.  LM Studio
4.  Mistral
5.  Ollama
6.  OpenAI
7.  Open Router
8.  Custom (Any OpenAI compatible endpoint)

#### Setting Up an Azure Endpoint in Alter

1.  **Enable Custom Provider:** In Alter's settings, enable the "Custom provider" option.
2.  **Choose Azure:** Select Azure as your provider.
3.  **Enter Complete Chat Completion Endpoint URL:** Provide the full chat completion endpoint URL, including the `api-version` parameter and the model name within the URL.  For example: `https://yourinstance.openai.azure.com/openai/deployments/your-model-name/chat/completions?api-version=2024-02-15-preview`
4.  **Enter API Key:**  Enter your Azure OpenAI API key.

Important Considerations

*   **Complete Endpoint Required:**  Make sure to use the *complete* chat completion endpoint, as Alter extracts the model name from the URL.
*   **Model Name in URL:** The model deployment name *must* be included in the URL path.
*   **API Version:** The URL *must* include the `api-version` parameter.


#### Where to find your API keys

| Provider | URL for generate an API Key | 
| -------- | -------- | 
| Google (Gemini)     | https://aistudio.google.com/app/apikey   | [Link](https://ai.google.dev/api/compatibility)
| Mistral     | https://console.mistral.ai/api-keys/  
| OpenAI     | https://platform.openai.com/api-keys |[Link]




### Locally using Ollama or LM Studio

![Custom Local](https://beehiiv-images-production.s3.amazonaws.com/uploads/asset/file/a3cb944c-7379-49a6-9349-c829bcda071b/image.png?t=1740499713)

To use Alter with local models (via Ollama or LM Studio):  
1. Go to **Settings > API keys > Custom provider**.  
2. Enable Custom Provider
3. Pick Ollama or LM Studio in the list of provider

> Once connected, a tick will appear next to **Custom Endpoint**.  

![image alt](https://beehiiv-images-production.s3.amazonaws.com/uploads/asset/file/4a22f3fb-ad9e-4f50-8184-1e5cc5238118/Alter_Settings_API_key_custom_provider_on.png?t=1740500360)

Your local models will be listed under the **Custom** section.

![Custom model](https://beehiiv-images-production.s3.amazonaws.com/uploads/asset/file/c3a9bef5-ff23-4a35-99b6-aedc7bc38972/Alter_Main_Custom_Models.png?t=1740502675)
