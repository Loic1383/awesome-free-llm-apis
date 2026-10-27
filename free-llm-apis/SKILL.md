---
name: free-llm-apis
description: Guide users through obtaining and configuring free API keys for LLM providers. Use when the user wants to set up a free LLM API, get a free API key, connect to a free model provider, configure an OpenAI-compatible endpoint at no cost, or asks about free tiers for AI models. Triggers on "free API key", "free LLM", "set up Gemini/Groq/Mistral/etc.", "which free provider", "how to get an API key", "free model access", "configure LLM for free".
---

# Free LLM API Setup

Help users pick a free LLM provider and configure their API key. Every provider here has a permanent free tier, no credit card needed.

The list in this skill follows `data.json` of the repository. When a limit or a model looks wrong, `data.json` and its footnotes are the source of truth.

## Provider Selection

Ask the user what matters most, then recommend accordingly:

| Priority | Best picks |
|---|---|
| Most requests per day | NVIDIA NIM (40 RPM, 10,000 RPD), Groq (30 RPM, 1,000 RPD) |
| Largest model selection | NVIDIA NIM (100+ models), Cloudflare Workers AI (60+ models), OpenRouter (17 free models) |
| Strongest proprietary models | Google Gemini (Gemini 3.8 Flash), Mistral AI (Mistral Medium 3.5), Cohere (Command A+, non-commercial only) |
| Fastest inference | Groq (LPU inference) |
| No signup, no key | OVHcloud AI Endpoints (2 RPM per model), Kilo Code (200 req/hr), LLM7.io |
| European provider | Mistral AI (FR), OVHcloud AI Endpoints (FR, hosted in the EU), LLM7.io (UK) |
| Roleplay and storytelling | Aion Labs |

### Provider categories

**Provider APIs** -- run by the companies that train the models:
- Aion Labs, Cohere, Google Gemini, Mistral AI, Z AI (Zhipu AI)
- See [references/provider-apis.md](references/provider-apis.md) for setup instructions.

**Inference providers** -- third-party platforms hosting open-weight models:
- Cloudflare Workers AI, Gonka Broker, Groq, Kilo Code, LLM7.io, ModelScope, NVIDIA NIM, Ollama Cloud, OpenRouter, OVHcloud AI Endpoints, SiliconFlow
- See [references/inference-providers.md](references/inference-providers.md) for setup instructions.

## Workflow

1. Ask what models, rate limits, or features the user cares about. If they already know which provider they want, skip to step 3.
2. Match their priorities against the table above. Suggest 1-2 options with a short reason.
3. Load the right reference file and walk through the setup steps for that provider (API key, code example, env var).
4. Offer a quick test script or curl command so they can confirm the key works.

## Quick Test Template

After setup, use this to verify any provider:

```python
from openai import OpenAI

client = OpenAI(api_key="KEY", base_url="BASE_URL")

response = client.chat.completions.create(
    model="MODEL_NAME",
    messages=[{"role": "user", "content": "Say hello in one sentence."}],
    max_tokens=50
)
print(response.choices[0].message.content)
```

Replace KEY, BASE_URL, and MODEL_NAME with values from the provider's setup guide. For the providers that need no key, use the curl example of their guide.

## Key Notes

- All endpoints work with the OpenAI SDK unless noted.
- RPM = requests per minute. RPD = requests per day. TPD = tokens per day.
- Google Gemini's free tier is available in the EU, UK, and Switzerland, but its terms require Paid Services when you make an app available to users there. Outside the EEA, Switzerland and the UK, free-tier prompts may be used to improve Google products.
- Mistral AI free mode may use prompts for training unless you opt out. OpenRouter free providers may log prompts.
- Cohere's trial key is for non-commercial use only and allows 1,000 API calls/month.
- ModelScope and SiliconFlow require real-name verification with mainland-Chinese identity documents.
- Free model lineups change often (Kilo Code, LLM7.io, OpenRouter, Gonka Broker). Check the provider's live model list before hardcoding a model ID.
- Don't hardcode API keys. Use environment variables or a secrets manager.
