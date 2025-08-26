<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1197b6dbde36773e04a5ae826557fdb9",
  "translation_date": "2025-08-26T17:34:27+00:00",
  "source_file": "03-GettingStarted/README.md",
  "language_code": "pa"
}
-->
## ਸ਼ੁਰੂਆਤ ਕਰਨਾ  

[![ਆਪਣਾ ਪਹਿਲਾ MCP ਸਰਵਰ ਬਣਾਓ](../../../translated_images/04.0ea920069efd979a0b2dad51e72c1df7ead9c57b3305796068a6cee1f0dd6674.pa.png)](https://youtu.be/sNDZO9N4m9Y)

_(ਉਪਰ ਦਿੱਤੀ ਤਸਵੀਰ 'ਤੇ ਕਲਿੱਕ ਕਰਕੇ ਇਸ ਪਾਠ ਦਾ ਵੀਡੀਓ ਵੇਖੋ)_

ਇਸ ਸੈਕਸ਼ਨ ਵਿੱਚ ਕਈ ਪਾਠ ਸ਼ਾਮਲ ਹਨ:

- **1 ਤੁਹਾਡਾ ਪਹਿਲਾ ਸਰਵਰ**, ਇਸ ਪਹਿਲੇ ਪਾਠ ਵਿੱਚ, ਤੁਸੀਂ ਆਪਣਾ ਪਹਿਲਾ ਸਰਵਰ ਬਣਾਉਣ ਅਤੇ ਇਸਨੂੰ ਇੰਸਪੈਕਟਰ ਟੂਲ ਨਾਲ ਜਾਂਚਣ ਦਾ ਤਰੀਕਾ ਸਿੱਖੋਗੇ, ਜੋ ਕਿ ਤੁਹਾਡੇ ਸਰਵਰ ਨੂੰ ਟੈਸਟ ਅਤੇ ਡੀਬੱਗ ਕਰਨ ਦਾ ਇੱਕ ਕੀਮਤੀ ਤਰੀਕਾ ਹੈ, [ਪਾਠ 'ਤੇ ਜਾਓ](01-first-server/README.md)

- **2 ਕਲਾਇੰਟ**, ਇਸ ਪਾਠ ਵਿੱਚ, ਤੁਸੀਂ ਇੱਕ ਕਲਾਇੰਟ ਲਿਖਣ ਦਾ ਤਰੀਕਾ ਸਿੱਖੋਗੇ ਜੋ ਤੁਹਾਡੇ ਸਰਵਰ ਨਾਲ ਕਨੈਕਟ ਕਰ ਸਕੇ, [ਪਾਠ 'ਤੇ ਜਾਓ](02-client/README.md)

- **3 LLM ਨਾਲ ਕਲਾਇੰਟ**, ਇੱਕ ਹੋਰ ਵਧੀਆ ਤਰੀਕਾ ਕਲਾਇੰਟ ਲਿਖਣ ਦਾ ਹੈ ਇਸ ਵਿੱਚ LLM ਸ਼ਾਮਲ ਕਰਨਾ ਤਾਂ ਜੋ ਇਹ ਤੁਹਾਡੇ ਸਰਵਰ ਨਾਲ "ਵਾਰਤਾਲਾਪ" ਕਰ ਸਕੇ ਕਿ ਕੀ ਕਰਨਾ ਹੈ, [ਪਾਠ 'ਤੇ ਜਾਓ](03-llm-client/README.md)

- **4 Visual Studio Code ਵਿੱਚ GitHub Copilot Agent ਮੋਡ ਦੇ ਨਾਲ ਸਰਵਰ ਦੀ ਵਰਤੋਂ**, ਇੱਥੇ, ਅਸੀਂ Visual Studio Code ਵਿੱਚੋਂ ਆਪਣਾ MCP ਸਰਵਰ ਚਲਾਉਣ ਦੇ ਤਰੀਕੇ ਦੇਖ ਰਹੇ ਹਾਂ, [ਪਾਠ 'ਤੇ ਜਾਓ](04-vscode/README.md)

- **5 stdio Transport Server**, stdio ਟ੍ਰਾਂਸਪੋਰਟ ਮੌਜੂਦਾ ਵਿਸ਼ੇਸ਼ਤਾ ਵਿੱਚ MCP ਸਰਵਰ-ਤੋਂ-ਕਲਾਇੰਟ ਸੰਚਾਰ ਲਈ ਸਿਫਾਰਸ਼ੀ ਮਿਆਰ ਹੈ, ਜੋ ਸੁਰੱਖਿਅਤ subprocess-ਅਧਾਰਿਤ ਸੰਚਾਰ ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ [ਪਾਠ 'ਤੇ ਜਾਓ](05-stdio-server/README.md)

- **6 MCP ਨਾਲ HTTP Streaming (Streamable HTTP)**. ਆਧੁਨਿਕ HTTP ਸਟ੍ਰੀਮਿੰਗ, ਪ੍ਰਗਤੀ ਸੂਚਨਾਵਾਂ, ਅਤੇ Streamable HTTP ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਸਕੇਲਬਲ, ਰੀਅਲ-ਟਾਈਮ MCP ਸਰਵਰ ਅਤੇ ਕਲਾਇੰਟ ਲਾਗੂ ਕਰਨ ਦਾ ਤਰੀਕਾ ਸਿੱਖੋ। [ਪਾਠ 'ਤੇ ਜਾਓ](06-http-streaming/README.md)

- **7 VSCode ਲਈ AI Toolkit ਦੀ ਵਰਤੋਂ**, ਆਪਣੇ MCP ਕਲਾਇੰਟ ਅਤੇ ਸਰਵਰ ਦੀ ਵਰਤੋਂ ਅਤੇ ਟੈਸਟ ਕਰਨ ਲਈ [ਪਾਠ 'ਤੇ ਜਾਓ](07-aitk/README.md)

- **8 ਟੈਸਟਿੰਗ**, ਇੱਥੇ ਅਸੀਂ ਖਾਸ ਤੌਰ 'ਤੇ ਇਸ ਗੱਲ 'ਤੇ ਧਿਆਨ ਦੇਵਾਂਗੇ ਕਿ ਅਸੀਂ ਆਪਣੇ ਸਰਵਰ ਅਤੇ ਕਲਾਇੰਟ ਨੂੰ ਵੱਖ-ਵੱਖ ਤਰੀਕਿਆਂ ਵਿੱਚ ਕਿਵੇਂ ਟੈਸਟ ਕਰ ਸਕਦੇ ਹਾਂ, [ਪਾਠ 'ਤੇ ਜਾਓ](08-testing/README.md)

- **9 ਡਿਪਲੌਇਮੈਂਟ**, ਇਹ ਅਧਿਆਇ ਤੁਹਾਡੇ MCP ਹੱਲਾਂ ਨੂੰ ਡਿਪਲੌਇ ਕਰਨ ਦੇ ਵੱਖ-ਵੱਖ ਤਰੀਕਿਆਂ ਨੂੰ ਦੇਖੇਗਾ, [ਪਾਠ 'ਤੇ ਜਾਓ](09-deployment/README.md)

Model Context Protocol (MCP) ਇੱਕ ਖੁੱਲਾ ਪ੍ਰੋਟੋਕੋਲ ਹੈ ਜੋ ਐਪਲੀਕੇਸ਼ਨਾਂ ਨੂੰ LLMs ਨੂੰ ਸੰਦਰਭ ਪ੍ਰਦਾਨ ਕਰਨ ਦੇ ਤਰੀਕੇ ਨੂੰ ਮਿਆਰੀ ਬਣਾਉਂਦਾ ਹੈ। MCP ਨੂੰ AI ਐਪਲੀਕੇਸ਼ਨਾਂ ਲਈ USB-C ਪੋਰਟ ਵਾਂਗ ਸੋਚੋ - ਇਹ AI ਮਾਡਲਾਂ ਨੂੰ ਵੱਖ-ਵੱਖ ਡਾਟਾ ਸਰੋਤਾਂ ਅਤੇ ਟੂਲਾਂ ਨਾਲ ਜੁੜਨ ਦਾ ਮਿਆਰੀ ਤਰੀਕਾ ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ।

## ਸਿੱਖਣ ਦੇ ਉਦੇਸ਼

ਇਸ ਪਾਠ ਦੇ ਅੰਤ ਤੱਕ, ਤੁਸੀਂ ਇਹ ਕਰਨ ਦੇ ਯੋਗ ਹੋਵੋਗੇ:

- C#, Java, Python, TypeScript, ਅਤੇ JavaScript ਵਿੱਚ MCP ਲਈ ਵਿਕਾਸ ਵਾਤਾਵਰਣ ਸੈਟਅਪ ਕਰੋ
- ਵਿਸ਼ੇਸ਼ ਫੀਚਰਾਂ (ਸਰੋਤ, ਪ੍ਰੋੰਪਟ, ਅਤੇ ਟੂਲ) ਦੇ ਨਾਲ ਬੇਸਿਕ MCP ਸਰਵਰ ਬਣਾਓ ਅਤੇ ਡਿਪਲੌਇ ਕਰੋ
- ਐਪਲੀਕੇਸ਼ਨ ਹੋਸਟ ਕਰੋ ਜੋ MCP ਸਰਵਰਾਂ ਨਾਲ ਜੁੜਦੇ ਹਨ
- MCP ਲਾਗੂ ਕਰਨ ਦੀ ਜਾਂਚ ਅਤੇ ਡੀਬੱਗ ਕਰੋ
- ਆਮ ਸੈਟਅਪ ਚੁਣੌਤੀਆਂ ਅਤੇ ਉਨ੍ਹਾਂ ਦੇ ਹੱਲ ਨੂੰ ਸਮਝੋ
- ਆਪਣੇ MCP ਲਾਗੂ ਕਰਨ ਨੂੰ ਪ੍ਰਸਿੱਧ LLM ਸੇਵਾਵਾਂ ਨਾਲ ਜੋੜੋ

## ਆਪਣਾ MCP ਵਾਤਾਵਰਣ ਸੈਟਅਪ ਕਰਨਾ

MCP 'ਤੇ ਕੰਮ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ, ਇਹ ਜ਼ਰੂਰੀ ਹੈ ਕਿ ਤੁਸੀਂ ਆਪਣਾ ਵਿਕਾਸ ਵਾਤਾਵਰਣ ਤਿਆਰ ਕਰੋ ਅਤੇ ਬੁਨਿਆਦੀ ਵਰਕਫਲੋ ਨੂੰ ਸਮਝੋ। ਇਹ ਸੈਕਸ਼ਨ ਤੁਹਾਨੂੰ MCP ਨਾਲ ਸਹੀ ਸ਼ੁਰੂਆਤ ਕਰਨ ਲਈ ਸ਼ੁਰੂਆਤੀ ਸੈਟਅਪ ਕਦਮਾਂ ਵਿੱਚ ਮਦਦ ਕਰੇਗਾ।

### ਪੂਰਵ ਸ਼ਰਤਾਂ

MCP ਵਿਕਾਸ ਵਿੱਚ ਡੁੱਬਣ ਤੋਂ ਪਹਿਲਾਂ, ਇਹ ਯਕੀਨੀ ਬਣਾਓ ਕਿ ਤੁਹਾਡੇ ਕੋਲ ਹੈ:

- **ਵਿਕਾਸ ਵਾਤਾਵਰਣ**: ਤੁਹਾਡੇ ਚੁਣੇ ਹੋਏ ਭਾਸ਼ਾ ਲਈ (C#, Java, Python, TypeScript, ਜਾਂ JavaScript)
- **IDE/Editor**: Visual Studio, Visual Studio Code, IntelliJ, Eclipse, PyCharm, ਜਾਂ ਕੋਈ ਆਧੁਨਿਕ ਕੋਡ ਐਡੀਟਰ
- **ਪੈਕੇਜ ਮੈਨੇਜਰ**: NuGet, Maven/Gradle, pip, ਜਾਂ npm/yarn
- **API Keys**: ਉਹ AI ਸੇਵਾਵਾਂ ਲਈ ਜੋ ਤੁਸੀਂ ਆਪਣੇ ਹੋਸਟ ਐਪਲੀਕੇਸ਼ਨਾਂ ਵਿੱਚ ਵਰਤਣ ਦੀ ਯੋਜਨਾ ਬਣਾਉਂਦੇ ਹੋ

### ਅਧਿਕਾਰਤ SDKs

ਆਗਾਮੀ ਅਧਿਆਇ ਵਿੱਚ ਤੁਸੀਂ Python, TypeScript, Java ਅਤੇ .NET ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਬਣਾਈਆਂ ਹੱਲਾਂ ਦੇਖੋਗੇ। ਇੱਥੇ ਸਾਰੇ ਅਧਿਕਾਰਤ SDKs ਦਿੱਤੇ ਗਏ ਹਨ।

MCP ਕਈ ਭਾਸ਼ਾਵਾਂ ਲਈ ਅਧਿਕਾਰਤ SDKs ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ:
- [C# SDK](https://github.com/modelcontextprotocol/csharp-sdk) - Microsoft ਦੇ ਸਹਿਯੋਗ ਨਾਲ ਸੰਭਾਲਿਆ ਗਿਆ
- [Java SDK](https://github.com/modelcontextprotocol/java-sdk) - Spring AI ਦੇ ਸਹਿਯੋਗ ਨਾਲ ਸੰਭਾਲਿਆ ਗਿਆ
- [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) - ਅਧਿਕਾਰਤ TypeScript ਲਾਗੂਕਰਨ
- [Python SDK](https://github.com/modelcontextprotocol/python-sdk) - ਅਧਿਕਾਰਤ Python ਲਾਗੂਕਰਨ
- [Kotlin SDK](https://github.com/modelcontextprotocol/kotlin-sdk) - ਅਧਿਕਾਰਤ Kotlin ਲਾਗੂਕਰਨ
- [Swift SDK](https://github.com/modelcontextprotocol/swift-sdk) - Loopwork AI ਦੇ ਸਹਿਯੋਗ ਨਾਲ ਸੰਭਾਲਿਆ ਗਿਆ
- [Rust SDK](https://github.com/modelcontextprotocol/rust-sdk) - ਅਧਿਕਾਰਤ Rust ਲਾਗੂਕਰਨ

## ਮੁੱਖ ਗੱਲਾਂ

- MCP ਵਿਕਾਸ ਵਾਤਾਵਰਣ ਸੈਟਅਪ ਕਰਨਾ ਭਾਸ਼ਾ-ਵਿਸ਼ੇਸ਼ SDKs ਨਾਲ ਸਿੱਧਾ ਹੈ
- MCP ਸਰਵਰ ਬਣਾਉਣ ਵਿੱਚ ਸਾਫ਼ ਸਕੀਮਾਂ ਨਾਲ ਟੂਲ ਬਣਾਉਣਾ ਅਤੇ ਰਜਿਸਟਰ ਕਰਨਾ ਸ਼ਾਮਲ ਹੈ
- MCP ਕਲਾਇੰਟ ਸਰਵਰਾਂ ਅਤੇ ਮਾਡਲਾਂ ਨਾਲ ਜੁੜਦੇ ਹਨ ਤਾਂ ਜੋ ਵਧੇਰੇ ਸਮਰੱਥਾਵਾਂ ਦਾ ਲਾਭ ਲੈ ਸਕਣ
- ਭਰੋਸੇਮੰਦ MCP ਲਾਗੂਕਰਨ ਲਈ ਟੈਸਟਿੰਗ ਅਤੇ ਡੀਬੱਗਿੰਗ ਜ਼ਰੂਰੀ ਹੈ
- ਡਿਪਲੌਇਮੈਂਟ ਵਿਕਲਪ ਸਥਾਨਕ ਵਿਕਾਸ ਤੋਂ ਕਲਾਉਡ-ਅਧਾਰਿਤ ਹੱਲਾਂ ਤੱਕ ਵੱਖ-ਵੱਖ ਹਨ

## ਅਭਿਆਸ

ਸਾਡੇ ਕੋਲ ਨਮੂਨਿਆਂ ਦਾ ਇੱਕ ਸੈੱਟ ਹੈ ਜੋ ਇਸ ਸੈਕਸ਼ਨ ਦੇ ਸਾਰੇ ਅਧਿਆਇ ਵਿੱਚ ਦਿੱਤੇ ਗਏ ਅਭਿਆਸਾਂ ਨੂੰ ਪੂਰਾ ਕਰਦਾ ਹੈ। ਇਸ ਤੋਂ ਇਲਾਵਾ, ਹਰ ਅਧਿਆਇ ਵਿੱਚ ਆਪਣੇ ਅਭਿਆਸ ਅਤੇ ਅਸਾਈਨਮੈਂਟ ਵੀ ਹਨ।

- [Java Calculator](./samples/java/calculator/README.md)
- [.Net Calculator](../../../03-GettingStarted/samples/csharp)
- [JavaScript Calculator](./samples/javascript/README.md)
- [TypeScript Calculator](./samples/typescript/README.md)
- [Python Calculator](../../../03-GettingStarted/samples/python)

## ਵਾਧੂ ਸਰੋਤ

- [Model Context Protocol ਦੀ ਵਰਤੋਂ ਕਰਕੇ Azure 'ਤੇ Agents ਬਣਾਓ](https://learn.microsoft.com/azure/developer/ai/intro-agents-mcp)
- [Azure Container Apps ਨਾਲ ਦੂਰ-ਵਰਤੋਂ MCP (Node.js/TypeScript/JavaScript)](https://learn.microsoft.com/samples/azure-samples/mcp-container-ts/mcp-container-ts/)
- [.NET OpenAI MCP Agent](https://learn.microsoft.com/samples/azure-samples/openai-mcp-agent-dotnet/openai-mcp-agent-dotnet/)

## ਅਗਲਾ ਕੀ ਹੈ

ਅਗਲਾ: [ਆਪਣਾ ਪਹਿਲਾ MCP ਸਰਵਰ ਬਣਾਉਣਾ](01-first-server/README.md)

---

**ਅਸਵੀਕਰਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੀਤਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।