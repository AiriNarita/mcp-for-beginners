<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "57f7b15640bb96ef2f6f09003eec935e",
  "translation_date": "2025-08-18T16:48:53+00:00",
  "source_file": "03-GettingStarted/03-llm-client/README.md",
  "language_code": "pa"
}
-->
# ਕਲਾਇੰਟ ਬਣਾਉਣਾ LLM ਨਾਲ

ਅਜੇ ਤੱਕ, ਤੁਸੀਂ ਦੇਖਿਆ ਕਿ ਸਰਵਰ ਅਤੇ ਕਲਾਇੰਟ ਕਿਵੇਂ ਬਣਾਉਣਾ ਹੈ। ਕਲਾਇੰਟ ਨੇ ਸਰਵਰ ਨੂੰ ਸਪਸ਼ਟ ਤੌਰ 'ਤੇ ਕਾਲ ਕਰਕੇ ਇਸਦੇ ਟੂਲ, ਸਰੋਤ ਅਤੇ ਪ੍ਰੋੰਪਟ ਦੀ ਸੂਚੀ ਬਣਾਈ ਹੈ। ਪਰ ਇਹ ਵਿਧੀ ਬਹੁਤ ਵਿਆਵਹਾਰਿਕ ਨਹੀਂ ਹੈ। ਤੁਹਾਡਾ ਯੂਜ਼ਰ ਏਜੈਂਟਿਕ ਯੁੱਗ ਵਿੱਚ ਰਹਿੰਦਾ ਹੈ ਅਤੇ ਉਮੀਦ ਕਰਦਾ ਹੈ ਕਿ ਉਹ ਪ੍ਰੋੰਪਟ ਵਰਤ ਕੇ ਅਤੇ LLM ਨਾਲ ਸੰਚਾਰ ਕਰਕੇ ਕੰਮ ਕਰੇ। ਯੂਜ਼ਰ ਲਈ, ਇਹ ਮਹੱਤਵਪੂਰਨ ਨਹੀਂ ਹੈ ਕਿ ਤੁਸੀਂ ਆਪਣੀਆਂ ਸਮਰੱਥਾਵਾਂ ਨੂੰ ਸਟੋਰ ਕਰਨ ਲਈ MCP ਵਰਤਦੇ ਹੋ ਜਾਂ ਨਹੀਂ, ਪਰ ਉਹ ਕੁਦਰਤੀ ਭਾਸ਼ਾ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਸੰਚਾਰ ਕਰਨ ਦੀ ਉਮੀਦ ਕਰਦੇ ਹਨ। ਤਾਂ ਅਸੀਂ ਇਸ ਸਮੱਸਿਆ ਨੂੰ ਕਿਵੇਂ ਹੱਲ ਕਰਦੇ ਹਾਂ? ਹੱਲ ਇਹ ਹੈ ਕਿ ਕਲਾਇੰਟ ਵਿੱਚ LLM ਸ਼ਾਮਲ ਕੀਤਾ ਜਾਵੇ।

## ਝਲਕ

ਇਸ ਪਾਠ ਵਿੱਚ ਅਸੀਂ ਆਪਣੇ ਕਲਾਇੰਟ ਵਿੱਚ LLM ਸ਼ਾਮਲ ਕਰਨ 'ਤੇ ਧਿਆਨ ਦੇਵਾਂਗੇ ਅਤੇ ਦਿਖਾਵਾਂਗੇ ਕਿ ਇਹ ਤੁਹਾਡੇ ਯੂਜ਼ਰ ਲਈ ਕਿਵੇਂ ਬਿਹਤਰ ਅਨੁਭਵ ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ।

## ਸਿੱਖਣ ਦੇ ਉਦੇਸ਼

ਇਸ ਪਾਠ ਦੇ ਅੰਤ ਤੱਕ, ਤੁਸੀਂ ਸਮਰੱਥ ਹੋਵੋਗੇ:

- LLM ਨਾਲ ਕਲਾਇੰਟ ਬਣਾਉਣਾ।
- LLM ਦੀ ਵਰਤੋਂ ਕਰਕੇ MCP ਸਰਵਰ ਨਾਲ ਬਿਨਾਂ ਰੁਕਾਵਟ ਸੰਚਾਰ ਕਰਨਾ।
- ਕਲਾਇੰਟ ਪਾਸੇ ਬਿਹਤਰ ਅੰਤ-ਯੂਜ਼ਰ ਅਨੁਭਵ ਪ੍ਰਦਾਨ ਕਰਨਾ।

## ਵਿਧੀ

ਆਓ ਅਸੀਂ ਸਮਝਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰੀਏ ਕਿ ਸਾਨੂੰ ਕਿਹੜੀ ਵਿਧੀ ਅਪਣਾਉਣੀ ਚਾਹੀਦੀ ਹੈ। LLM ਸ਼ਾਮਲ ਕਰਨਾ ਸਧਾਰਨ ਲੱਗਦਾ ਹੈ, ਪਰ ਕੀ ਅਸੀਂ ਇਸ ਨੂੰ ਅਸਲ ਵਿੱਚ ਕਰ ਸਕਦੇ ਹਾਂ?

ਇਹ ਹੈ ਕਿ ਕਲਾਇੰਟ ਸਰਵਰ ਨਾਲ ਕਿਵੇਂ ਸੰਚਾਰ ਕਰੇਗਾ:

1. ਸਰਵਰ ਨਾਲ ਕਨੈਕਸ਼ਨ ਸਥਾਪਿਤ ਕਰੋ।

1. ਸਮਰੱਥਾਵਾਂ, ਪ੍ਰੋੰਪਟ, ਸਰੋਤ ਅਤੇ ਟੂਲ ਦੀ ਸੂਚੀ ਬਣਾਓ ਅਤੇ ਉਨ੍ਹਾਂ ਦੀ ਸਕੀਮਾ ਸੇਵ ਕਰੋ।

1. ਇੱਕ LLM ਸ਼ਾਮਲ ਕਰੋ ਅਤੇ ਸੇਵ ਕੀਤੀਆਂ ਸਮਰੱਥਾਵਾਂ ਅਤੇ ਉਨ੍ਹਾਂ ਦੀ ਸਕੀਮਾ ਨੂੰ ਇੱਕ ਫਾਰਮੈਟ ਵਿੱਚ ਪਾਸ ਕਰੋ ਜੋ LLM ਨੂੰ ਸਮਝ ਆਵੇ।

1. ਯੂਜ਼ਰ ਪ੍ਰੋੰਪਟ ਨੂੰ ਸੰਭਾਲੋ ਅਤੇ ਇਸਨੂੰ LLM ਨੂੰ ਪਾਸ ਕਰੋ, ਨਾਲ ਹੀ ਉਹ ਟੂਲ ਜੋ ਕਲਾਇੰਟ ਦੁਆਰਾ ਸੂਚੀਬੱਧ ਕੀਤੇ ਗਏ ਹਨ।

ਵਧੀਆ, ਹੁਣ ਅਸੀਂ ਸਮਝ ਗਏ ਕਿ ਅਸੀਂ ਇਸਨੂੰ ਉੱਚ-ਸਤਹ 'ਤੇ ਕਿਵੇਂ ਕਰ ਸਕਦੇ ਹਾਂ, ਆਓ ਹੇਠਾਂ ਦਿੱਤੇ ਅਭਿਆਸ ਵਿੱਚ ਇਸਨੂੰ ਅਜ਼ਮਾਈਏ।

## ਅਭਿਆਸ: LLM ਨਾਲ ਕਲਾਇੰਟ ਬਣਾਉਣਾ

ਇਸ ਅਭਿਆਸ ਵਿੱਚ, ਅਸੀਂ ਸਿੱਖਾਂਗੇ ਕਿ ਆਪਣੇ ਕਲਾਇੰਟ ਵਿੱਚ LLM ਕਿਵੇਂ ਸ਼ਾਮਲ ਕਰਨਾ ਹੈ।

### GitHub Personal Access Token ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਪ੍ਰਮਾਣਿਕਤਾ

GitHub ਟੋਕਨ ਬਣਾਉਣਾ ਇੱਕ ਸਧਾਰਨ ਪ੍ਰਕਿਰਿਆ ਹੈ। ਇਹ ਹੈ ਕਿ ਤੁਸੀਂ ਇਸਨੂੰ ਕਿਵੇਂ ਕਰ ਸਕਦੇ ਹੋ:

- GitHub ਸੈਟਿੰਗਜ਼ 'ਤੇ ਜਾਓ – ਉੱਪਰ ਸੱਜੇ ਕੋਨੇ ਵਿੱਚ ਆਪਣੇ ਪ੍ਰੋਫਾਈਲ ਚਿੱਤਰ 'ਤੇ ਕਲਿਕ ਕਰੋ ਅਤੇ ਸੈਟਿੰਗਜ਼ ਚੁਣੋ।
- Developer Settings 'ਤੇ ਜਾਓ – ਹੇਠਾਂ ਸਕ੍ਰੋਲ ਕਰੋ ਅਤੇ Developer Settings 'ਤੇ ਕਲਿਕ ਕਰੋ।
- Personal Access Tokens ਚੁਣੋ – Personal access tokens 'ਤੇ ਕਲਿਕ ਕਰੋ ਅਤੇ ਫਿਰ ਨਵਾਂ ਟੋਕਨ ਬਣਾਓ।
- ਆਪਣੇ ਟੋਕਨ ਨੂੰ ਕਨਫਿਗਰ ਕਰੋ – ਹਵਾਲੇ ਲਈ ਇੱਕ ਨੋਟ ਸ਼ਾਮਲ ਕਰੋ, ਮਿਆਦ ਦੀ ਮਿਤੀ ਸੈਟ ਕਰੋ, ਅਤੇ ਜ਼ਰੂਰੀ ਸਕੋਪ (ਅਧਿਕਾਰ) ਚੁਣੋ।
- ਟੋਕਨ ਬਣਾਓ ਅਤੇ ਕਾਪੀ ਕਰੋ – Generate token 'ਤੇ ਕਲਿਕ ਕਰੋ, ਅਤੇ ਇਸਨੂੰ ਤੁਰੰਤ ਕਾਪੀ ਕਰਨਾ ਯਕੀਨੀ ਬਣਾਓ, ਕਿਉਂਕਿ ਤੁਸੀਂ ਇਸਨੂੰ ਫਿਰ ਨਹੀਂ ਦੇਖ ਸਕੋਗੇ।

### -1- ਸਰਵਰ ਨਾਲ ਕਨੈਕਟ ਕਰੋ

ਆਓ ਪਹਿਲਾਂ ਆਪਣਾ ਕਲਾਇੰਟ ਬਣਾਈਏ:

#### TypeScript

```typescript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";
import { Transport } from "@modelcontextprotocol/sdk/shared/transport.js";
import OpenAI from "openai";
import { z } from "zod"; // Import zod for schema validation

class MCPClient {
    private openai: OpenAI;
    private client: Client;
    constructor(){
        this.openai = new OpenAI({
            baseURL: "https://models.inference.ai.azure.com", 
            apiKey: process.env.GITHUB_TOKEN,
        });

        this.client = new Client(
            {
                name: "example-client",
                version: "1.0.0"
            },
            {
                capabilities: {
                prompts: {},
                resources: {},
                tools: {}
                }
            }
            );    
    }
}
```

ਉਪਰੋਕਤ ਕੋਡ ਵਿੱਚ ਅਸੀਂ:

- ਲੋੜੀਂਦੇ ਲਾਇਬ੍ਰੇਰੀਜ਼ ਇੰਪੋਰਟ ਕੀਤੇ ਹਨ।
- ਦੋ ਮੈਂਬਰਾਂ `client` ਅਤੇ `openai` ਨਾਲ ਇੱਕ ਕਲਾਸ ਬਣਾਈ ਹੈ ਜੋ ਸਾਨੂੰ ਕਲਾਇੰਟ ਨੂੰ ਮੈਨੇਜ ਕਰਨ ਅਤੇ LLM ਨਾਲ ਸੰਚਾਰ ਕਰਨ ਵਿੱਚ ਮਦਦ ਕਰੇਗੀ।
- GitHub ਮਾਡਲ ਦੀ ਵਰਤੋਂ ਕਰਨ ਲਈ `baseUrl` ਸੈਟ ਕਰਕੇ ਆਪਣੇ LLM ਇੰਸਟੈਂਸ ਨੂੰ ਕਨਫਿਗਰ ਕੀਤਾ ਹੈ।

#### Python

```python
from mcp import ClientSession, StdioServerParameters, types
from mcp.client.stdio import stdio_client

# Create server parameters for stdio connection
server_params = StdioServerParameters(
    command="mcp",  # Executable
    args=["run", "server.py"],  # Optional command line arguments
    env=None,  # Optional environment variables
)


async def run():
    async with stdio_client(server_params) as (read, write):
        async with ClientSession(
            read, write
        ) as session:
            # Initialize the connection
            await session.initialize()


if __name__ == "__main__":
    import asyncio

    asyncio.run(run())

```

ਉਪਰੋਕਤ ਕੋਡ ਵਿੱਚ ਅਸੀਂ:

- MCP ਲਈ ਲੋੜੀਂਦੇ ਲਾਇਬ੍ਰੇਰੀਜ਼ ਇੰਪੋਰਟ ਕੀਤੇ ਹਨ।
- ਇੱਕ ਕਲਾਇੰਟ ਬਣਾਇਆ ਹੈ।

#### .NET

```csharp
using Azure;
using Azure.AI.Inference;
using Azure.Identity;
using System.Text.Json;
using ModelContextProtocol.Client;
using ModelContextProtocol.Protocol.Transport;
using System.Text.Json;

var clientTransport = new StdioClientTransport(new()
{
    Name = "Demo Server",
    Command = "/workspaces/mcp-for-beginners/03-GettingStarted/02-client/solution/server/bin/Debug/net8.0/server",
    Arguments = [],
});

await using var mcpClient = await McpClientFactory.CreateAsync(clientTransport);
```

#### Java

ਸਭ ਤੋਂ ਪਹਿਲਾਂ, ਤੁਹਾਨੂੰ ਆਪਣੇ `pom.xml` ਫਾਈਲ ਵਿੱਚ LangChain4j dependencies ਸ਼ਾਮਲ ਕਰਨ ਦੀ ਲੋੜ ਹੋਵੇਗੀ। MCP ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਅਤੇ GitHub ਮਾਡਲ ਸਪੋਰਟ ਨੂੰ ਯਕੀਨੀ ਬਣਾਉਣ ਲਈ ਇਹ dependencies ਸ਼ਾਮਲ ਕਰੋ:

```xml
<properties>
    <langchain4j.version>1.0.0-beta3</langchain4j.version>
</properties>

<dependencies>
    <!-- LangChain4j MCP Integration -->
    <dependency>
        <groupId>dev.langchain4j</groupId>
        <artifactId>langchain4j-mcp</artifactId>
        <version>${langchain4j.version}</version>
    </dependency>
    
    <!-- OpenAI Official API Client -->
    <dependency>
        <groupId>dev.langchain4j</groupId>
        <artifactId>langchain4j-open-ai-official</artifactId>
        <version>${langchain4j.version}</version>
    </dependency>
    
    <!-- GitHub Models Support -->
    <dependency>
        <groupId>dev.langchain4j</groupId>
        <artifactId>langchain4j-github-models</artifactId>
        <version>${langchain4j.version}</version>
    </dependency>
    
    <!-- Spring Boot Starter (optional, for production apps) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
</dependencies>
```

ਫਿਰ ਆਪਣਾ Java ਕਲਾਇੰਟ ਕਲਾਸ ਬਣਾਓ:

```java
import dev.langchain4j.mcp.McpToolProvider;
import dev.langchain4j.mcp.client.DefaultMcpClient;
import dev.langchain4j.mcp.client.McpClient;
import dev.langchain4j.mcp.client.transport.McpTransport;
import dev.langchain4j.mcp.client.transport.http.HttpMcpTransport;
import dev.langchain4j.model.chat.ChatLanguageModel;
import dev.langchain4j.model.openaiofficial.OpenAiOfficialChatModel;
import dev.langchain4j.service.AiServices;
import dev.langchain4j.service.tool.ToolProvider;

import java.time.Duration;
import java.util.List;

public class LangChain4jClient {
    
    public static void main(String[] args) throws Exception {        // Configure the LLM to use GitHub Models
        ChatLanguageModel model = OpenAiOfficialChatModel.builder()
                .isGitHubModels(true)
                .apiKey(System.getenv("GITHUB_TOKEN"))
                .timeout(Duration.ofSeconds(60))
                .modelName("gpt-4.1-nano")
                .build();

        // Create MCP transport for connecting to server
        McpTransport transport = new HttpMcpTransport.Builder()
                .sseUrl("http://localhost:8080/sse")
                .timeout(Duration.ofSeconds(60))
                .logRequests(true)
                .logResponses(true)
                .build();

        // Create MCP client
        McpClient mcpClient = new DefaultMcpClient.Builder()
                .transport(transport)
                .build();
    }
}
```

ਉਪਰੋਕਤ ਕੋਡ ਵਿੱਚ ਅਸੀਂ:

- **LangChain4j dependencies ਸ਼ਾਮਲ ਕੀਤੇ**: MCP ਇੰਟੀਗ੍ਰੇਸ਼ਨ, OpenAI ਅਧਿਕਾਰਤ ਕਲਾਇੰਟ, ਅਤੇ GitHub ਮਾਡਲ ਸਪੋਰਟ ਲਈ ਲੋੜੀਂਦੇ।
- **LangChain4j ਲਾਇਬ੍ਰੇਰੀਜ਼ ਇੰਪੋਰਟ ਕੀਤੀਆਂ**: MCP ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਅਤੇ OpenAI ਚੈਟ ਮਾਡਲ ਫੰਕਸ਼ਨਲਿਟੀ ਲਈ।
- **`ChatLanguageModel` ਬਣਾਇਆ**: GitHub ਮਾਡਲ ਦੇ ਨਾਲ ਆਪਣੇ GitHub ਟੋਕਨ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਕਨਫਿਗਰ ਕੀਤਾ।
- **HTTP ਟ੍ਰਾਂਸਪੋਰਟ ਸੈਟ ਕੀਤਾ**: Server-Sent Events (SSE) ਦੀ ਵਰਤੋਂ ਕਰਕੇ MCP ਸਰਵਰ ਨਾਲ ਕਨੈਕਟ ਕਰਨ ਲਈ।
- **MCP ਕਲਾਇੰਟ ਬਣਾਇਆ**: ਜੋ ਸਰਵਰ ਨਾਲ ਸੰਚਾਰ ਨੂੰ ਸੰਭਾਲੇਗਾ।
- **LangChain4j ਦੀ ਬਣਾਈ MCP ਸਪੋਰਟ ਦੀ ਵਰਤੋਂ ਕੀਤੀ**: ਜੋ LLMs ਅਤੇ MCP ਸਰਵਰਾਂ ਦੇ ਵਿਚਕਾਰ ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਨੂੰ ਸਧਾਰਨ ਬਣਾਉਂਦਾ ਹੈ।

#### Rust

ਇਹ ਉਦਾਹਰਨ ਮੰਨਦਾ ਹੈ ਕਿ ਤੁਹਾਡੇ ਕੋਲ ਇੱਕ Rust ਆਧਾਰਿਤ MCP ਸਰਵਰ ਚੱਲ ਰਿਹਾ ਹੈ। ਜੇਕਰ ਤੁਹਾਡੇ ਕੋਲ ਨਹੀਂ ਹੈ, ਤਾਂ [01-first-server](../01-first-server/README.md) ਪਾਠ ਵਿੱਚ ਵਾਪਸ ਜਾਓ ਅਤੇ ਸਰਵਰ ਬਣਾਓ।

ਜਦੋਂ ਤੁਹਾਡੇ ਕੋਲ Rust MCP ਸਰਵਰ ਹੋਵੇ, ਟਰਮੀਨਲ ਖੋਲ੍ਹੋ ਅਤੇ ਸਰਵਰ ਵਾਲੇ ਹੀ ਡਾਇਰੈਕਟਰੀ ਵਿੱਚ ਜਾਓ। ਫਿਰ ਨਵਾਂ LLM ਕਲਾਇੰਟ ਪ੍ਰੋਜੈਕਟ ਬਣਾਉਣ ਲਈ ਹੇਠਾਂ ਦਿੱਤੇ ਕਮਾਂਡ ਚਲਾਓ:

```bash
mkdir calculator-llmclient
cd calculator-llmclient
cargo init
```

ਆਪਣੇ `Cargo.toml` ਫਾਈਲ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤੀਆਂ dependencies ਸ਼ਾਮਲ ਕਰੋ:

```toml
[dependencies]
async-openai = { version = "0.29.0", features = ["byot"] }
rmcp = { version = "0.5.0", features = ["client", "transport-child-process"] }
serde_json = "1.0.141"
tokio = { version = "1.46.1", features = ["rt-multi-thread"] }
```

> [!NOTE]
> Rust ਲਈ OpenAI ਦੀ ਅਧਿਕਾਰਤ ਲਾਇਬ੍ਰੇਰੀ ਨਹੀਂ ਹੈ, ਪਰ `async-openai` crate ਇੱਕ [community maintained library](https://platform.openai.com/docs/libraries/rust#rust) ਹੈ ਜੋ ਆਮ ਤੌਰ 'ਤੇ ਵਰਤੀ ਜਾਂਦੀ ਹੈ।

`src/main.rs` ਫਾਈਲ ਖੋਲ੍ਹੋ ਅਤੇ ਇਸਦੀ ਸਮੱਗਰੀ ਨੂੰ ਹੇਠਾਂ ਦਿੱਤੇ ਕੋਡ ਨਾਲ ਬਦਲੋ:

```rust
use async_openai::{Client, config::OpenAIConfig};
use rmcp::{
    RmcpError,
    model::{CallToolRequestParam, ListToolsResult},
    service::{RoleClient, RunningService, ServiceExt},
    transport::{ConfigureCommandExt, TokioChildProcess},
};
use serde_json::{Value, json};
use std::error::Error;
use tokio::process::Command;

#[tokio::main]
async fn main() -> Result<(), Box<dyn Error>> {
    // Initial message
    let mut messages = vec![json!({"role": "user", "content": "What is the sum of 3 and 2?"})];

    // Setup OpenAI client
    let api_key = std::env::var("OPENAI_API_KEY")?;
    let openai_client = Client::with_config(
        OpenAIConfig::new()
            .with_api_base("https://models.github.ai/inference/chat")
            .with_api_key(api_key),
    );

    // Setup MCP client
    let server_dir = std::path::Path::new(env!("CARGO_MANIFEST_DIR"))
        .parent()
        .unwrap()
        .join("calculator-server");

    let mcp_client = ()
        .serve(
            TokioChildProcess::new(Command::new("cargo").configure(|cmd| {
                cmd.arg("run").current_dir(server_dir);
            }))
            .map_err(RmcpError::transport_creation::<TokioChildProcess>)?,
        )
        .await?;

    // TODO: Get MCP tool listing 

    // TODO: LLM conversation with tool calls

    Ok(())
}
```

ਇਹ ਕੋਡ ਇੱਕ ਬੁਨਿਆਦੀ Rust ਐਪਲੀਕੇਸ਼ਨ ਸੈਟ ਕਰਦਾ ਹੈ ਜੋ MCP ਸਰਵਰ ਅਤੇ GitHub ਮਾਡਲ ਨਾਲ LLM ਇੰਟਰੈਕਸ਼ਨ ਲਈ ਕਨੈਕਟ ਕਰੇਗਾ।

> [!IMPORTANT]
> ਐਪਲੀਕੇਸ਼ਨ ਚਲਾਉਣ ਤੋਂ ਪਹਿਲਾਂ `OPENAI_API_KEY` ਵਾਤਾਵਰਣ ਵੈਰੀਏਬਲ ਨੂੰ ਆਪਣੇ GitHub ਟੋਕਨ ਨਾਲ ਸੈਟ ਕਰਨਾ ਯਕੀਨੀ ਬਣਾਓ।

ਵਧੀਆ, ਅਗਲੇ ਕਦਮ ਵਿੱਚ, ਆਓ ਸਰਵਰ ਦੀ ਸਮਰੱਥਾਵਾਂ ਦੀ ਸੂਚੀ ਬਣਾਈਏ।
ਅਸੀਂ LLM ਨੂੰ ਕਈ ਵਾਰ ਕਾਲ ਕਰਨ ਵਾਲੇ ਹਾਂ, ਇਸ ਲਈ ਆਓ ਇੱਕ ਫੰਕਸ਼ਨ ਨੂੰ ਪਰਿਭਾਸ਼ਿਤ ਕਰੀਏ ਜੋ LLM ਕਾਲ ਨੂੰ ਸੰਭਾਲੇਗਾ। ਆਪਣੇ `main.rs` ਫਾਇਲ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤਾ ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰੋ:

```rust
async fn call_llm(
    client: &Client<OpenAIConfig>,
    messages: &[Value],
    tools: &ListToolsResult,
) -> Result<Value, Box<dyn Error>> {
    let response = client
        .completions()
        .create_byot(json!({
            "messages": messages,
            "model": "openai/gpt-4.1",
            "tools": format_tools(tools).await?,
        }))
        .await?;
    Ok(response)
}
```

ਇਹ ਫੰਕਸ਼ਨ LLM ਕਲਾਇੰਟ, ਸੁਨੇਹਿਆਂ ਦੀ ਸੂਚੀ (ਜਿਸ ਵਿੱਚ ਯੂਜ਼ਰ ਪ੍ਰੋੰਪਟ ਸ਼ਾਮਲ ਹੈ), MCP ਸਰਵਰ ਤੋਂ ਟੂਲ, ਅਤੇ LLM ਨੂੰ ਇੱਕ ਬੇਨਤੀ ਭੇਜਦਾ ਹੈ, ਅਤੇ ਜਵਾਬ ਵਾਪਸ ਕਰਦਾ ਹੈ।

LLM ਤੋਂ ਪ੍ਰਾਪਤ ਜਵਾਬ ਵਿੱਚ `choices` ਦੀ ਇੱਕ ਐਰੇ ਸ਼ਾਮਲ ਹੋਵੇਗੀ। ਸਾਨੂੰ ਨਤੀਜੇ ਨੂੰ ਪ੍ਰੋਸੈਸ ਕਰਨ ਦੀ ਲੋੜ ਹੋਵੇਗੀ ਤਾਂ ਕਿ ਪਤਾ ਲਗਾਇਆ ਜਾ ਸਕੇ ਕਿ ਕੋਈ `tool_calls` ਮੌਜੂਦ ਹਨ ਜਾਂ ਨਹੀਂ। ਇਹ ਸਾਨੂੰ ਦੱਸਦਾ ਹੈ ਕਿ LLM ਕਿਸੇ ਵਿਸ਼ੇਸ਼ ਟੂਲ ਨੂੰ ਦਲੀਲਾਂ ਨਾਲ ਕਾਲ ਕਰਨ ਦੀ ਬੇਨਤੀ ਕਰ ਰਿਹਾ ਹੈ। ਆਪਣੇ `main.rs` ਫਾਇਲ ਦੇ ਤਲ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤਾ ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ ਤਾਂ ਕਿ LLM ਜਵਾਬ ਨੂੰ ਸੰਭਾਲਣ ਲਈ ਇੱਕ ਫੰਕਸ਼ਨ ਪਰਿਭਾਸ਼ਿਤ ਕੀਤਾ ਜਾ ਸਕੇ:

```rust
async fn process_llm_response(
    llm_response: &Value,
    mcp_client: &RunningService<RoleClient, ()>,
    openai_client: &Client<OpenAIConfig>,
    mcp_tools: &ListToolsResult,
    messages: &mut Vec<Value>,
) -> Result<(), Box<dyn Error>> {
    let Some(message) = llm_response
        .get("choices")
        .and_then(|c| c.as_array())
        .and_then(|choices| choices.first())
        .and_then(|choice| choice.get("message"))
    else {
        return Ok(());
    };

    // Print content if available
    if let Some(content) = message.get("content").and_then(|c| c.as_str()) {
        println!("🤖 {}", content);
    }

    // Handle tool calls
    if let Some(tool_calls) = message.get("tool_calls").and_then(|tc| tc.as_array()) {
        messages.push(message.clone()); // Add assistant message

        // Execute each tool call
        for tool_call in tool_calls {
            let (tool_id, name, args) = extract_tool_call_info(tool_call)?;
            println!("⚡ Calling tool: {}", name);

            let result = mcp_client
                .call_tool(CallToolRequestParam {
                    name: name.into(),
                    arguments: serde_json::from_str::<Value>(&args)?.as_object().cloned(),
                })
                .await?;

            // Add tool result to messages
            messages.push(json!({
                "role": "tool",
                "tool_call_id": tool_id,
                "content": serde_json::to_string_pretty(&result)?
            }));
        }

        // Continue conversation with tool results
        let response = call_llm(openai_client, messages, mcp_tools).await?;
        Box::pin(process_llm_response(
            &response,
            mcp_client,
            openai_client,
            mcp_tools,
            messages,
        ))
        .await?;
    }
    Ok(())
}
```

ਜੇ `tool_calls` ਮੌਜੂਦ ਹਨ, ਇਹ ਟੂਲ ਜਾਣਕਾਰੀ ਨੂੰ ਕੱਢਦਾ ਹੈ, MCP ਸਰਵਰ ਨੂੰ ਟੂਲ ਬੇਨਤੀ ਨਾਲ ਕਾਲ ਕਰਦਾ ਹੈ, ਅਤੇ ਨਤੀਜਿਆਂ ਨੂੰ ਗੱਲਬਾਤ ਦੇ ਸੁਨੇਹਿਆਂ ਵਿੱਚ ਸ਼ਾਮਲ ਕਰਦਾ ਹੈ। ਫਿਰ ਇਹ LLM ਨਾਲ ਗੱਲਬਾਤ ਜਾਰੀ ਰੱਖਦਾ ਹੈ ਅਤੇ ਸੁਨੇਹਿਆਂ ਨੂੰ ਸਹਾਇਕ ਦੇ ਜਵਾਬ ਅਤੇ ਟੂਲ ਕਾਲ ਨਤੀਜਿਆਂ ਨਾਲ ਅਪਡੇਟ ਕਰਦਾ ਹੈ।

ਟੂਲ ਕਾਲ ਜਾਣਕਾਰੀ ਨੂੰ ਕੱਢਣ ਲਈ ਜੋ LLM MCP ਕਾਲਾਂ ਲਈ ਵਾਪਸ ਕਰਦਾ ਹੈ, ਅਸੀਂ ਇੱਕ ਹੋਰ ਸਹਾਇਕ ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰਾਂਗੇ ਜੋ ਕਾਲ ਕਰਨ ਲਈ ਸਾਰਾ ਕੁਝ ਕੱਢੇਗਾ। ਆਪਣੇ `main.rs` ਫਾਇਲ ਦੇ ਤਲ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤਾ ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ:

```rust
fn extract_tool_call_info(tool_call: &Value) -> Result<(String, String, String), Box<dyn Error>> {
    let tool_id = tool_call
        .get("id")
        .and_then(|id| id.as_str())
        .unwrap_or("")
        .to_string();
    let function = tool_call.get("function").ok_or("Missing function")?;
    let name = function
        .get("name")
        .and_then(|n| n.as_str())
        .unwrap_or("")
        .to_string();
    let args = function
        .get("arguments")
        .and_then(|a| a.as_str())
        .unwrap_or("{}")
        .to_string();
    Ok((tool_id, name, args))
}
```

ਸਾਰੇ ਹਿੱਸੇ ਸਥਾਪਿਤ ਹੋਣ ਦੇ ਨਾਲ, ਅਸੀਂ ਹੁਣ ਸ਼ੁਰੂਆਤੀ ਯੂਜ਼ਰ ਪ੍ਰੋੰਪਟ ਨੂੰ ਸੰਭਾਲ ਸਕਦੇ ਹਾਂ ਅਤੇ LLM ਨੂੰ ਕਾਲ ਕਰ ਸਕਦੇ ਹਾਂ। ਆਪਣੇ `main` ਫੰਕਸ਼ਨ ਨੂੰ ਹੇਠਾਂ ਦਿੱਤੇ ਕੋਡ ਨਾਲ ਅਪਡੇਟ ਕਰੋ:

```rust
// LLM conversation with tool calls
let response = call_llm(&openai_client, &messages, &tools).await?;
process_llm_response(
    &response,
    &mcp_client,
    &openai_client,
    &tools,
    &mut messages,
)
.await?;
```

ਇਹ LLM ਨੂੰ ਸ਼ੁਰੂਆਤੀ ਯੂਜ਼ਰ ਪ੍ਰੋੰਪਟ ਦੇ ਨਾਲ ਪੁੱਛੇਗਾ ਕਿ ਦੋ ਨੰਬਰਾਂ ਦਾ ਜੋੜ ਕੀ ਹੈ, ਅਤੇ ਜਵਾਬ ਨੂੰ ਪ੍ਰੋਸੈਸ ਕਰੇਗਾ ਤਾਂ ਕਿ ਟੂਲ ਕਾਲਾਂ ਨੂੰ ਗਤੀਸ਼ੀਲ ਤਰੀਕੇ ਨਾਲ ਸੰਭਾਲਿਆ ਜਾ ਸਕੇ।

ਵਧੀਆ, ਤੁਸੀਂ ਕਰ ਦਿੱਤਾ!

## ਅਸਾਈਨਮੈਂਟ

ਅਭਿਆਸ ਤੋਂ ਕੋਡ ਲਓ ਅਤੇ ਸਰਵਰ ਨੂੰ ਹੋਰ ਟੂਲਾਂ ਨਾਲ ਬਣਾਓ। ਫਿਰ ਇੱਕ LLM ਦੇ ਨਾਲ ਇੱਕ ਕਲਾਇੰਟ ਬਣਾਓ, ਜਿਵੇਂ ਕਿ ਅਭਿਆਸ ਵਿੱਚ, ਅਤੇ ਵੱਖ-ਵੱਖ ਪ੍ਰੋੰਪਟਾਂ ਨਾਲ ਇਸਨੂੰ ਟੈਸਟ ਕਰੋ ਤਾਂ ਕਿ ਤੁਹਾਡੇ ਸਰਵਰ ਟੂਲਾਂ ਨੂੰ ਗਤੀਸ਼ੀਲ ਤਰੀਕੇ ਨਾਲ ਕਾਲ ਕੀਤਾ ਜਾ ਸਕੇ। ਇਸ ਤਰੀਕੇ ਨਾਲ ਕਲਾਇੰਟ ਬਣਾਉਣ ਦਾ ਮਤਲਬ ਹੈ ਕਿ ਅੰਤਮ ਯੂਜ਼ਰ ਨੂੰ ਵਧੀਆ ਯੂਜ਼ਰ ਅਨੁਭਵ ਪ੍ਰਾਪਤ ਹੋਵੇਗਾ ਕਿਉਂਕਿ ਉਹ ਪ੍ਰੋੰਪਟਾਂ ਦੀ ਵਰਤੋਂ ਕਰਨ ਦੇ ਯੋਗ ਹੋਣਗੇ, ਸਥਿਰ ਕਲਾਇੰਟ ਕਮਾਂਡਾਂ ਦੀ ਬਜਾਏ, ਅਤੇ ਕਿਸੇ ਵੀ MCP ਸਰਵਰ ਨੂੰ ਕਾਲ ਕਰਨ ਤੋਂ ਬੇਖ਼ਬਰ ਰਹਿਣਗੇ।

## ਹੱਲ

[Solution](/03-GettingStarted/03-llm-client/solution/README.md)

## ਮੁੱਖ ਸਿੱਖਿਆ

- ਆਪਣੇ ਕਲਾਇੰਟ ਵਿੱਚ LLM ਸ਼ਾਮਲ ਕਰਨਾ ਯੂਜ਼ਰਾਂ ਨੂੰ MCP ਸਰਵਰਾਂ ਨਾਲ ਸੰਚਾਰ ਕਰਨ ਦਾ ਇੱਕ ਵਧੀਆ ਤਰੀਕਾ ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ।
- ਤੁਹਾਨੂੰ MCP ਸਰਵਰ ਜਵਾਬ ਨੂੰ ਕੁਝ ਇਸ ਤਰ੍ਹਾਂ ਰੂਪਾਂਤਰਿਤ ਕਰਨ ਦੀ ਲੋੜ ਹੈ ਜੋ LLM ਨੂੰ ਸਮਝ ਆ ਸਕੇ।

## ਨਮੂਨੇ

- [Java Calculator](../samples/java/calculator/README.md)
- [.Net Calculator](../../../../03-GettingStarted/samples/csharp)
- [JavaScript Calculator](../samples/javascript/README.md)
- [TypeScript Calculator](../samples/typescript/README.md)
- [Python Calculator](../../../../03-GettingStarted/samples/python)
- [Rust Calculator](../../../../03-GettingStarted/samples/rust)

## ਵਾਧੂ ਸਰੋਤ

## ਅਗਲਾ ਕੀ ਹੈ

- ਅਗਲਾ: [Visual Studio Code ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਸਰਵਰ ਨੂੰ ਕਨਜ਼ਿਊਮ ਕਰਨਾ](../04-vscode/README.md)

**ਅਸਵੀਕਾਰਨ:**  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੀਤਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤ ਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।