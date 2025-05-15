# Bring Your Own LLM Guide

This page provides recommendations for configuring your LLM and outlines the cost calculation methodology for the AskAI feature. For general information on AskAI, please refer to [the dedicated documentation](../../introduction/vectice-overview/askai.md).

## Bring your own LLM

Vectice supports integration with any LLM of your choice as long as they meet minimum performance requirements (see requirements below). Whether you use commercial APIs or host models privately, Vectice can connect seamlessly. Our team is available to assist with advanced customization needs.

**Note:** Vectice does not require a **multimodal** LLM. All current features operate using **text-only** models.

### Benefits of Using Your Own LLM

Bringing your own LLM allows to:

* **Preserve data confidentiality** by processing prompts in a secure, private environment
* **Control costs** by selecting the model and infrastructure that fit your usage profile
* **Meet compliance and IT policies** with regional hosting or on-premise setups
* **Fine-tune behavior** using domain-specific data and enterprise instructions
* **Ensure long-term flexibility** across proprietary and open-source model providers

### Best Practices for Your LLM Deployment

To ensure a **smooth experience** and prevent service interruptions in Vectice, especially under concurrent usage, we recommend:

**Token Throughput**

* Support a **throughput of 450,000 tokens per minute**
* This baseline ensures stable usage for \~5 to 10 active users
* Applies to both input and output tokens

**Recommended Model Capabilities**

* Your LLM should match or exceed the performance of **GPT-4o-mini** on reasoning, summarization, and code analysis tasks.&#x20;
* Minimum equivalent model size: **7B–8B parameters** trained on high-quality data (e.g., LLaMA 3.2+ 8B+, Mixtral 8x22B)

### Azure OpenAI Configuration for GPT-4o (Recommended)

If using **GPT-4o or GPT-4o-mini** on **Azure**, configure content filtering to avoid macro execution errors:

1. Go to **Safety + Security → Content Filters**
2. Create a dedicated filter for Vectice usage
3. **Disable the following input filters**:
   * Prompt shields for jailbreak attacks
   * Prompt shields for indirect attacks
4. Associate the filter with your GPT-4o or 4o-mini deployment

### Cost Calculation per User

Standard usage for a user actively documenting model development or validation is about 1.3 Millions tokens per month. For reference, this is the current pricing for LLMs (April 2025).

<table><thead><tr><th width="183.8148193359375"></th><th width="80.59259033203125">GPT 4o</th><th width="121.333251953125">GPT 4o-mini</th><th width="122.0740966796875">Claude 3.7 Sonnet</th><th width="119.851806640625">LLaMA 70B</th><th>Mixtral 8x22B+</th><th></th></tr></thead><tbody><tr><td>Cost per Million token</td><td>$ 5 </td><td>$ 0.6</td><td>$ 3</td><td>$ 0.72</td><td>$ 2</td><td></td></tr><tr><td>Monthly Estimated Cost per User</td><td>&#x3C; $ 7 </td><td> &#x3C; $ 1</td><td> &#x3C; $ 4</td><td>&#x3C; $ 1</td><td>&#x3C; $ 3</td><td></td></tr></tbody></table>

For the latest pricing, refer to [OpenAI’s API pricing page](https://openai.com/api/pricing/) and [Amazon's Bedrock princing page](https://aws.amazon.com/bedrock/pricing/).

### Common LLMs Used with Vectice

Enterprises typically integrate the following models based on their deployment strategy and governance needs:

<table><thead><tr><th>Model</th><th width="175.48150634765625">Provider</th><th width="163.2962646484375">Parameters</th><th>Deployment Mode</th></tr></thead><tbody><tr><td>GPT-4o / GPT 4o-mini+</td><td>OpenAI (Azure)</td><td>N/A</td><td>Cloud (Azure-hosted) / Self-hosted</td></tr><tr><td>Claude 3.7+ Sonnet</td><td>Anthropic</td><td>N/A</td><td>Cloud (Amazon Bedrock) / Self-hosted</td></tr><tr><td>LLaMA 3.3+ 70B</td><td>Meta</td><td>70B</td><td>Cloud (Amazon Bedrock) / Self-hosted </td></tr><tr><td>Mixtral 8x22B+</td><td>Mistral AI</td><td>8x22B</td><td>Cloud (Amazon Bedrock) / Self-hosted</td></tr></tbody></table>

Need help evaluating which LLM works best for your use case? Reach out to our team at **support@vectice.com**.
