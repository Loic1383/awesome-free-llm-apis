# Inference Providers - Setup Guides

Third-party platforms that host open-weight models from various sources.

## Cloudflare Workers AI

**Models:** Llama 3.3 70B, Llama 4 Scout, GPT-OSS-120B, Gemma 4 26B, GLM-4.7-Flash +55 more
**Limits:** 10,000 Neurons/day, shared across all models, reset daily at 00:00 UTC. Going over fails the request, it does not bill you.

### Get your API key

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com/profile/api-tokens).
2. Sign in or create a Cloudflare account.
3. Create an API token with the "Workers AI" permission.
4. Note your Account ID from the dashboard sidebar.
5. Copy both the token and account ID.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_CLOUDFLARE_API_TOKEN",
    base_url="https://api.cloudflare.com/client/v4/accounts/YOUR_ACCOUNT_ID/ai/v1/"
)

response = client.chat.completions.create(
    model="@cf/meta/llama-3.3-70b-instruct-fp8-fast",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export CLOUDFLARE_API_TOKEN="your-token-here"
export CLOUDFLARE_ACCOUNT_ID="your-account-id"
```

---

## Gonka Broker

**Models:** MiniMax M2.7, DeepSeek V4 Flash, GLM-5.3-Flash, BGE-M3 (embeddings) — lineup rotates; live list at https://proxy.gonkabroker.com/v1/models
**Limits:** ~1M tokens/month (shared, varies by model; cheaper models stretch further), resets monthly, unused tokens don't carry over. On free-tier funds requests are capped at a lower RPM — the current cap is returned as `maxRpm` by `/test-auth`.

### Get your API key

1. Go to [gonkabroker.com](https://app.gonkabroker.com/signup) and sign up with email or Google.
2. Verify a real (non-VoIP) phone number via SMS to receive the free grant (one grant per number).
3. Open the **API Keys** tab and create a key.
4. Copy the key (starts with `gnk-prx-`, shown only once).

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_GONKA_BROKER_KEY",
    base_url="https://proxy.gonkabroker.com/v1"
)

response = client.chat.completions.create(
    model="MiniMaxAI/MiniMax-M2.7",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export GONKA_API_KEY="your-key-here"
```

---

## Groq

**Models:** GPT-OSS-120B, GPT-OSS-20B, Qwen3.8 27B (vision)
**Limits:** 30 RPM, 1,000 RPD

### Get your API key

1. Go to the [Groq Console](https://console.groq.com/keys).
2. Create an account or sign in.
3. Click "Create API Key."
4. Name it and copy the key.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_GROQ_API_KEY",
    base_url="https://api.groq.com/openai/v1/"
)

response = client.chat.completions.create(
    model="openai/gpt-oss-120b",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export GROQ_API_KEY="your-key-here"
```

---

## Kilo Code

**Models:** `kilo-auto/free` router, Nemotron 3 Ultra, Laguna S 2.1, North Mini Code +13 more (all `:free`) — the pool changes often
**Limits:** 200 requests/hour per IP
**Data note:** `kilo-auto/free` may route to providers that log prompts and outputs.

### Get access

Free models need no API key. For a key (optional), sign in at [app.kilo.ai](https://app.kilo.ai/profile).

### Usage example

```bash
curl https://api.kilo.ai/api/gateway/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model": "kilo-auto/free", "messages": [{"role": "user", "content": "Hello!"}]}'
```

With a key, use the OpenAI SDK with `base_url="https://api.kilo.ai/api/gateway"`.

---

## LLM7.io

**Models:** GPT-OSS 20B, Mistral Nemo, MiniMax M2.7, Nemotron 3 Nano, Codestral — the catalog rotates often; live list at https://api.llm7.io/v1/models
**Limits:** With a free token: 1 RPS, 60 RPM, 250 requests/hour, 100,000 tokens/24h. Anonymous access works without a token.

### Get your token (optional)

1. Go to [LLM7 Token page](https://token.llm7.io).
2. Register or sign in to get a token.
3. Copy the token.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_LLM7_TOKEN",
    base_url="https://api.llm7.io/v1/"
)

response = client.chat.completions.create(
    model="gpt-oss:20b",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

Without a token:

```bash
curl https://api.llm7.io/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model": "gpt-oss:20b", "messages": [{"role": "user", "content": "Hello!"}]}'
```

### Environment variable

```bash
export LLM7_API_KEY="your-token-here"
```

---

## ModelScope

**Models:** Qwen3.5 35B A3B, Qwen3.5 27B + other API-Inference models
**Limits:** 2,000 requests/day total, at most 500/day per model (dynamic)
**Condition:** Requires Alibaba Cloud account binding and real-name verification. Not usable from outside mainland China in practice.

### Get your API key

1. Go to [ModelScope access tokens](https://modelscope.cn/my/myaccesstoken).
2. Sign in, bind an Alibaba Cloud account and complete real-name verification.
3. Copy your access token.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_MODELSCOPE_TOKEN",
    base_url="https://api-inference.modelscope.cn/v1/"
)

response = client.chat.completions.create(
    model="Qwen/Qwen3.5-35B-A3B",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export MODELSCOPE_API_KEY="your-token-here"
```

---

## NVIDIA NIM

**Models:** Gemma 4 31B, Nemotron 3 Ultra, GPT-OSS-20B +92 more
**Limits:** 40 RPM, 10,000 RPD
**Condition:** Free with NVIDIA Developer Program membership.

### Get your API key

1. Go to [NVIDIA NIM](https://build.nvidia.com/explore/discover).
2. Create an NVIDIA account or sign in.
3. Pick any model and click "Get API Key."
4. Copy the key.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_NVIDIA_API_KEY",
    base_url="https://integrate.api.nvidia.com/v1/"
)

response = client.chat.completions.create(
    model="openai/gpt-oss-20b",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export NVIDIA_API_KEY="your-key-here"
```

---

## Ollama Cloud

**Models:** GPT-OSS 120B, GPT-OSS 20B, Nemotron 3 Ultra + other starter models
**Limits:** Monthly starter credits, reset from the sign-up date. 1 concurrent request (extra requests are queued). Models outside the Free plan answer HTTP 402.

### Get your API key

1. Go to [Ollama keys](https://ollama.com/settings/keys).
2. Create an account or sign in.
3. Create a new key and copy it.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_OLLAMA_API_KEY",
    base_url="https://ollama.com/v1/"
)

response = client.chat.completions.create(
    model="gpt-oss:120b",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export OLLAMA_API_KEY="your-key-here"
```

---

## OpenRouter

**Models:** 17 free models (`:free` suffix): Gemma 4 31B, Nemotron 3 Ultra, Laguna S 2.1, North Mini Code, Inkling +12 more
**Limits:** 20 RPM, 50 RPD across all free models (1,000 RPD after buying at least 10 credits)
**Data note:** Free providers may log prompts for training.

### Get your API key

1. Go to [OpenRouter Keys](https://openrouter.ai/keys).
2. Create an account or sign in.
3. Click "Create Key."
4. Copy the key.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_OPENROUTER_API_KEY",
    base_url="https://openrouter.ai/api/v1/"
)

response = client.chat.completions.create(
    model="google/gemma-4-31b-it:free",  # or "openrouter/free" to let OpenRouter pick
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export OPENROUTER_API_KEY="your-key-here"
```

---

## OVHcloud AI Endpoints

**Models:** Qwen3.5 397B, GPT-OSS-120B, GPT-OSS-20B, Llama 3.3 70B, Qwen3.8 27B +5 more, hosted in the EU
**Limits:** 2 requests/minute per IP and per model, anonymous

### Get access

No signup and no API key for the free tier. An API key raises the limits but is billed pay-as-you-go.

### Usage example

```bash
curl https://oai.endpoints.kepler.ai.cloud.ovh.net/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model": "gpt-oss-120b", "messages": [{"role": "user", "content": "Hello!"}]}'
```

---

## SiliconFlow

**Models:** Hunyuan-MT-7B, Xing4.0-29B (free), 100+ paid models
**Condition:** Real-name identity verification with mainland-Chinese documents. International users must contact support.

### Get your API key

1. Go to [SiliconFlow API keys](https://cloud.siliconflow.cn/account/ak).
2. Sign up and complete identity verification.
3. Create a key and copy it.

### Usage example

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_SILICONFLOW_API_KEY",
    base_url="https://api.siliconflow.cn/v1/"
)

response = client.chat.completions.create(
    model="XingChenAGI/Xing4.0-29B",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
```

### Environment variable

```bash
export SILICONFLOW_API_KEY="your-key-here"
```
