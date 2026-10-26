# Provider APIs - Setup Guides

APIs run by the companies that train or fine-tune the models themselves.

## Aion Labs

**Models:** Aion 3.0, Aion 3.0 Mini, Aion 2.0, Aion-RP Llama 3.1 8B
**Limits:** 15 RPM, 20K tokens/day
**Specialty:** Roleplay and storytelling.

### Get your API key

1. Go to [Aion Labs API keys](https://www.aionlabs.ai/app/api-keys/).
2. Create an account or sign in.
3. Create a new key.
4. Copy the key.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_AION_API_KEY",
    base_url="https://api.aionlabs.ai/v1"
)

response = client.chat.completions.create(
    model="aion-labs/aion-3.0",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export AION_API_KEY="your-key-here"
```

---

## Cohere

**Models:** Command A+, Command A, Command A Reasoning, Command A Vision, Command R+, Aya Expanse 32B +5 more
**Limits:** 20 RPM, 1,000 API calls/month
**Condition:** Trial key, non-commercial use only.

### Get your API key

1. Go to the [Cohere Dashboard](https://dashboard.cohere.com/api-keys).
2. Create an account or sign in.
3. Go to API Keys and generate a trial key.
4. Copy the key.

### Usage example

Cohere's native API lives at `https://api.cohere.com/v2`. Use the Cohere SDK (`pip install cohere`):

```python
import cohere

co = cohere.ClientV2(api_key="YOUR_COHERE_API_KEY")

response = co.chat(
    model="command-a-03-2025",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.message.content[0].text)
```

### Environment variable

```bash
export CO_API_KEY="your-key-here"
```

---

## Google Gemini

**Models:** Gemini 3.8 Flash, Gemini 3.6 Flash, Gemini 3.5 Flash-Lite, Gemini 2.5 Flash, Gemma 4 31B +3 more
**Limits:** Not published per model. Check your quotas in [AI Studio](https://aistudio.google.com/).
**Region note:** The free tier is available in the EU, UK and Switzerland, but the terms require Paid Services when you make an app available to users there.

### Get your API key

1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey).
2. Sign in with a Google account.
3. Click "Create API Key" and select or create a Google Cloud project.
4. Copy the generated key.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_GEMINI_API_KEY",
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/"
)

response = client.chat.completions.create(
    model="gemini-3.8-flash",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export GEMINI_API_KEY="your-key-here"
# Or for OpenAI-compatible usage:
export OPENAI_API_KEY="your-key-here"
export OPENAI_BASE_URL="https://generativelanguage.googleapis.com/v1beta/openai/"
```

---

## Mistral AI

**Models:** Mistral Medium 3.5, Mistral Small 4, Mistral Large 3, Codestral, Ministral 3 (3B, 8B, 14B)
**Limits:** No published numbers. Check the Limits page of the Mistral admin panel (last published: ~1 request/second, 500K tokens/minute).
**Data note:** Free-mode prompts may be used to train Mistral models unless you opt out.

### Get your API key

1. Go to the [Mistral Console](https://console.mistral.ai/api-keys).
2. Create an account or sign in. Free mode is enabled by default, no credit card required.
3. Go to API Keys and create a new key.
4. Copy the key.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_MISTRAL_API_KEY",
    base_url="https://api.mistral.ai/v1/"
)

response = client.chat.completions.create(
    model="mistral-small-2603",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export MISTRAL_API_KEY="your-key-here"
```

---

## Z AI (Zhipu AI)

**Models:** GLM-4.7-Flash, GLM-4.6V-Flash (vision), GLM-4.5-Flash (retirement announced)
**Limits:** 1 concurrent request

### Get your API key

1. Go to [Zhipu AI](https://open.bigmodel.cn/usercenter/apikeys), or to the international platform [z.ai](https://z.ai).
2. Sign up. Overseas phone numbers are accepted, and the chat API does not require real-name verification.
3. Go to API Keys and create a new key.
4. Copy the key.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_ZHIPU_API_KEY",
    base_url="https://open.bigmodel.cn/api/paas/v4/"  # or https://api.z.ai/api/paas/v4/
)

response = client.chat.completions.create(
    model="glm-4.7-flash",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export ZHIPU_API_KEY="your-key-here"
```
