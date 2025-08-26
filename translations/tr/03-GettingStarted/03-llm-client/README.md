<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "57f7b15640bb96ef2f6f09003eec935e",
  "translation_date": "2025-08-18T17:59:34+00:00",
  "source_file": "03-GettingStarted/03-llm-client/README.md",
  "language_code": "tr"
}
-->
# Bir LLM ile istemci oluşturma

Şimdiye kadar, bir sunucu ve istemci oluşturmayı gördünüz. İstemci, sunucuyu açıkça çağırarak araçlarını, kaynaklarını ve istemlerini listeleyebiliyordu. Ancak, bu çok pratik bir yaklaşım değildir. Kullanıcınız, ajanlık çağında yaşıyor ve istemleri kullanmayı ve bir LLM ile iletişim kurmayı bekliyor. Kullanıcınız için, yeteneklerinizi MCP kullanarak saklayıp saklamadığınız önemli değil, ancak doğal dil kullanarak etkileşim kurmayı bekliyorlar. Peki, bunu nasıl çözeriz? Çözüm, istemciye bir LLM eklemekle ilgilidir.

## Genel Bakış

Bu derste, istemcinize bir LLM eklemeye odaklanıyoruz ve bunun kullanıcılarınız için nasıl çok daha iyi bir deneyim sağladığını gösteriyoruz.

## Öğrenme Hedefleri

Bu dersin sonunda şunları yapabileceksiniz:

- Bir LLM ile bir istemci oluşturmak.
- Bir LLM kullanarak bir MCP sunucusuyla sorunsuz bir şekilde etkileşim kurmak.
- İstemci tarafında daha iyi bir son kullanıcı deneyimi sağlamak.

## Yaklaşım

Hangi yaklaşımı benimsememiz gerektiğini anlamaya çalışalım. Bir LLM eklemek basit görünüyor, ancak bunu gerçekten nasıl yapacağız?

İşte istemcinin sunucuyla nasıl etkileşim kuracağı:

1. Sunucuyla bağlantı kurun.

1. Yetenekleri, istemleri, kaynakları ve araçları listeleyin ve şemalarını kaydedin.

1. Bir LLM ekleyin ve kaydedilen yetenekleri ve şemalarını LLM'nin anlayabileceği bir formatta iletin.

1. Kullanıcı istemini, istemci tarafından listelenen araçlarla birlikte LLM'ye ileterek işleyin.

Harika, şimdi bunu yüksek seviyede nasıl yapabileceğimizi anladık, aşağıdaki alıştırmada bunu deneyelim.

## Alıştırma: Bir LLM ile istemci oluşturma

Bu alıştırmada, istemcimize bir LLM eklemeyi öğreneceğiz.

### GitHub Kişisel Erişim Jetonu ile Kimlik Doğrulama

GitHub jetonu oluşturmak basit bir işlemdir. İşte nasıl yapılacağı:

- GitHub Ayarlarına gidin – Sağ üst köşedeki profil resminize tıklayın ve Ayarlar'ı seçin.
- Geliştirici Ayarlarına gidin – Aşağı kaydırın ve Geliştirici Ayarlarına tıklayın.
- Kişisel Erişim Jetonlarını seçin – Kişisel erişim jetonlarına tıklayın ve ardından Yeni jeton oluşturun.
- Jetonunuzu Yapılandırın – Referans için bir not ekleyin, bir son kullanma tarihi belirleyin ve gerekli kapsamları (izinleri) seçin.
- Jetonu Oluşturun ve Kopyalayın – Jeton oluştur'a tıklayın ve hemen kopyaladığınızdan emin olun, çünkü daha sonra tekrar göremeyeceksiniz.

### -1- Sunucuya Bağlanma

Öncelikle istemcimizi oluşturalım:

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

Yukarıdaki kodda şunları yaptık:

- Gerekli kütüphaneleri içe aktardık.
- `client` ve `openai` adında iki üyesi olan bir sınıf oluşturduk, bunlar sırasıyla bir istemciyi yönetmemize ve bir LLM ile etkileşim kurmamıza yardımcı olacak.
- LLM örneğimizi GitHub Modellerini kullanacak şekilde yapılandırdık ve `baseUrl`'i çıkarım API'sine işaret edecek şekilde ayarladık.

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

Yukarıdaki kodda şunları yaptık:

- MCP için gerekli kütüphaneleri içe aktardık.
- Bir istemci oluşturduk.

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

Öncelikle, `pom.xml` dosyanıza LangChain4j bağımlılıklarını eklemeniz gerekecek. MCP entegrasyonu ve GitHub Modelleri desteği için bu bağımlılıkları ekleyin:

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

Ardından Java istemci sınıfınızı oluşturun:

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

Yukarıdaki kodda şunları yaptık:

- **LangChain4j bağımlılıklarını ekledik**: MCP entegrasyonu, OpenAI resmi istemcisi ve GitHub Modelleri desteği için gerekli.
- **LangChain4j kütüphanelerini içe aktardık**: MCP entegrasyonu ve OpenAI sohbet modeli işlevselliği için.
- **Bir `ChatLanguageModel` oluşturduk**: GitHub Modellerini GitHub jetonunuzla kullanacak şekilde yapılandırıldı.
- **HTTP taşımayı ayarladık**: MCP sunucusuna bağlanmak için Sunucu Tarafından Gönderilen Olaylar (SSE) kullanıldı.
- **Bir MCP istemcisi oluşturduk**: Sunucuyla iletişimi yönetecek.
- **LangChain4j'nin yerleşik MCP desteğini kullandık**: LLM'ler ve MCP sunucuları arasındaki entegrasyonu basitleştirir.

#### Rust

Bu örnek, bir Rust tabanlı MCP sunucusunun çalıştığını varsayar. Eğer bir sunucunuz yoksa, [01-first-server](../01-first-server/README.md) dersine geri dönerek sunucuyu oluşturabilirsiniz.

Rust MCP sunucunuz olduğunda, bir terminal açın ve sunucuyla aynı dizine gidin. Ardından yeni bir LLM istemci projesi oluşturmak için şu komutu çalıştırın:

```bash
mkdir calculator-llmclient
cd calculator-llmclient
cargo init
```

`Cargo.toml` dosyanıza şu bağımlılıkları ekleyin:

```toml
[dependencies]
async-openai = { version = "0.29.0", features = ["byot"] }
rmcp = { version = "0.5.0", features = ["client", "transport-child-process"] }
serde_json = "1.0.141"
tokio = { version = "1.46.1", features = ["rt-multi-thread"] }
```

> [!NOTE]
> OpenAI için resmi bir Rust kütüphanesi yoktur, ancak `async-openai` paketi [topluluk tarafından sürdürülen bir kütüphanedir](https://platform.openai.com/docs/libraries/rust#rust) ve yaygın olarak kullanılır.

`src/main.rs` dosyasını açın ve içeriğini şu kodla değiştirin:

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

Bu kod, bir MCP sunucusuna ve GitHub Modellerine bağlanacak temel bir Rust uygulaması oluşturur.

> [!IMPORTANT]
> Uygulamayı çalıştırmadan önce `OPENAI_API_KEY` ortam değişkenini GitHub jetonunuzla ayarladığınızdan emin olun.

Harika, bir sonraki adımımızda sunucudaki yetenekleri listeleyeceğiz.

### -2- Sunucu Yeteneklerini Listeleme

Şimdi sunucuya bağlanıp yeteneklerini soracağız:

#### TypeScript

Aynı sınıfa şu yöntemleri ekleyin:

```typescript
async connectToServer(transport: Transport) {
     await this.client.connect(transport);
     this.run();
     console.error("MCPClient started on stdin/stdout");
}

async run() {
    console.log("Asking server for available tools");

    // listing tools
    const toolsResult = await this.client.listTools();
}
```

Yukarıdaki kodda şunları yaptık:

- Sunucuya bağlanmak için `connectToServer` kodunu ekledik.
- Uygulama akışımızı yöneten bir `run` yöntemi oluşturduk. Şu ana kadar sadece araçları listeliyor, ancak yakında daha fazlasını ekleyeceğiz.

#### Python

```python
# List available resources
resources = await session.list_resources()
print("LISTING RESOURCES")
for resource in resources:
    print("Resource: ", resource)

# List available tools
tools = await session.list_tools()
print("LISTING TOOLS")
for tool in tools.tools:
    print("Tool: ", tool.name)
    print("Tool", tool.inputSchema["properties"])
```

Eklediğimiz şeyler:

- Kaynakları ve araçları listeledik ve yazdırdık. Araçlar için ayrıca daha sonra kullanacağımız `inputSchema`yı listeledik.

#### .NET

```csharp
async Task<List<ChatCompletionsToolDefinition>> GetMcpTools()
{
    Console.WriteLine("Listing tools");
    var tools = await mcpClient.ListToolsAsync();

    List<ChatCompletionsToolDefinition> toolDefinitions = new List<ChatCompletionsToolDefinition>();

    foreach (var tool in tools)
    {
        Console.WriteLine($"Connected to server with tools: {tool.Name}");
        Console.WriteLine($"Tool description: {tool.Description}");
        Console.WriteLine($"Tool parameters: {tool.JsonSchema}");

        // TODO: convert tool definition from MCP tool to LLm tool     
    }

    return toolDefinitions;
}
```

Yukarıdaki kodda şunları yaptık:

- MCP Sunucusunda mevcut araçları listeledik.
- Her araç için ad, açıklama ve şemasını listeledik. Şema, araçları çağırmak için kısa süre sonra kullanacağımız bir şeydir.

#### Java

```java
// Create a tool provider that automatically discovers MCP tools
ToolProvider toolProvider = McpToolProvider.builder()
        .mcpClients(List.of(mcpClient))
        .build();

// The MCP tool provider automatically handles:
// - Listing available tools from the MCP server
// - Converting MCP tool schemas to LangChain4j format
// - Managing tool execution and responses
```

Yukarıdaki kodda şunları yaptık:

- MCP sunucusundaki tüm araçları otomatik olarak keşfeden ve kaydeden bir `McpToolProvider` oluşturduk.
- Araç sağlayıcı, MCP araç şemaları ile LangChain4j'nin araç formatı arasındaki dönüşümü dahili olarak yönetir.
- Bu yaklaşım, manuel araç listeleme ve dönüştürme sürecini soyutlar.

#### Rust

MCP sunucusundan araçları almak `list_tools` yöntemi kullanılarak yapılır. MCP istemcisini ayarladıktan sonra, `main` fonksiyonunuza şu kodu ekleyin:

```rust
// Get MCP tool listing 
let tools = mcp_client.list_tools(Default::default()).await?;
```

### -3- Sunucu Yeteneklerini LLM Araçlarına Dönüştürme

Sunucu yeteneklerini listeledikten sonraki adım, bunları LLM'nin anlayabileceği bir formata dönüştürmektir. Bunu yaptıktan sonra, bu yetenekleri LLM'ye araç olarak sağlayabiliriz.

#### TypeScript

1. MCP Sunucusundan gelen yanıtı LLM'nin kullanabileceği bir araç formatına dönüştürmek için şu kodu ekleyin:

    ```typescript
    openAiToolAdapter(tool: {
        name: string;
        description?: string;
        input_schema: any;
        }) {
        // Create a zod schema based on the input_schema
        const schema = z.object(tool.input_schema);
    
        return {
            type: "function" as const, // Explicitly set type to "function"
            function: {
            name: tool.name,
            description: tool.description,
            parameters: {
            type: "object",
            properties: tool.input_schema.properties,
            required: tool.input_schema.required,
            },
            },
        };
    }

    ```

    Yukarıdaki kod, MCP Sunucusundan gelen bir yanıtı alır ve bunu LLM'nin anlayabileceği bir araç tanımı formatına dönüştürür.

1. Ardından, `run` yöntemini sunucu yeteneklerini listeleyecek şekilde güncelleyelim:

    ```typescript
    async run() {
        console.log("Asking server for available tools");
        const toolsResult = await this.client.listTools();
        const tools = toolsResult.tools.map((tool) => {
            return this.openAiToolAdapter({
            name: tool.name,
            description: tool.description,
            input_schema: tool.inputSchema,
            });
        });
    }
    ```

    Yukarıdaki kodda, sonucu haritalamak ve her giriş için `openAiToolAdapter` çağırmak üzere `run` yöntemini güncelledik.

#### Python

1. Öncelikle şu dönüştürücü fonksiyonu oluşturalım:

    ```python
    def convert_to_llm_tool(tool):
        tool_schema = {
            "type": "function",
            "function": {
                "name": tool.name,
                "description": tool.description,
                "type": "function",
                "parameters": {
                    "type": "object",
                    "properties": tool.inputSchema["properties"]
                }
            }
        }

        return tool_schema
    ```

    Yukarıdaki `convert_to_llm_tools` fonksiyonunda, bir MCP araç yanıtını alır ve bunu LLM'nin anlayabileceği bir formata dönüştürürüz.

1. Ardından, istemci kodumuzu bu fonksiyondan yararlanacak şekilde güncelleyelim:

    ```python
    for tool in tools.tools:
        print("Tool: ", tool.name)
        print("Tool", tool.inputSchema["properties"])
        functions.append(convert_to_llm_tool(tool))
    ```

    Burada, MCP araç yanıtını daha sonra LLM'ye besleyebileceğimiz bir şeye dönüştürmek için `convert_to_llm_tool` çağrısı ekliyoruz.

#### .NET

1. MCP araç yanıtını LLM'nin anlayabileceği bir şeye dönüştürmek için kod ekleyelim:

```csharp
ChatCompletionsToolDefinition ConvertFrom(string name, string description, JsonElement jsonElement)
{ 
    // convert the tool to a function definition
    FunctionDefinition functionDefinition = new FunctionDefinition(name)
    {
        Description = description,
        Parameters = BinaryData.FromObjectAsJson(new
        {
            Type = "object",
            Properties = jsonElement
        },
        new JsonSerializerOptions() { PropertyNamingPolicy = JsonNamingPolicy.CamelCase })
    };

    // create a tool definition
    ChatCompletionsToolDefinition toolDefinition = new ChatCompletionsToolDefinition(functionDefinition);
    return toolDefinition;
}
```

Yukarıdaki kodda şunları yaptık:

- `ConvertFrom` adında bir fonksiyon oluşturduk, bu fonksiyon ad, açıklama ve giriş şemasını alır.
- Bir ChatCompletionsDefinition'a geçirilen bir FunctionDefinition oluşturan işlevselliği tanımladık. Bu, LLM'nin anlayabileceği bir şeydir.

1. Mevcut kodu bu fonksiyondan yararlanacak şekilde nasıl güncelleyebileceğimizi görelim:

    ```csharp
    async Task<List<ChatCompletionsToolDefinition>> GetMcpTools()
    {
        Console.WriteLine("Listing tools");
        var tools = await mcpClient.ListToolsAsync();

        List<ChatCompletionsToolDefinition> toolDefinitions = new List<ChatCompletionsToolDefinition>();

        foreach (var tool in tools)
        {
            Console.WriteLine($"Connected to server with tools: {tool.Name}");
            Console.WriteLine($"Tool description: {tool.Description}");
            Console.WriteLine($"Tool parameters: {tool.JsonSchema}");

            JsonElement propertiesElement;
            tool.JsonSchema.TryGetProperty("properties", out propertiesElement);

            var def = ConvertFrom(tool.Name, tool.Description, propertiesElement);
            Console.WriteLine($"Tool definition: {def}");
            toolDefinitions.Add(def);

            Console.WriteLine($"Properties: {propertiesElement}");        
        }

        return toolDefinitions;
    }
    ```

    Yukarıdaki kodda şunları yaptık:

    - MCP araç yanıtını bir LLM aracına dönüştürmek için fonksiyonu güncelledik. Eklediğimiz kodu vurgulayalım:

        ```csharp
        JsonElement propertiesElement;
        tool.JsonSchema.TryGetProperty("properties", out propertiesElement);

        var def = ConvertFrom(tool.Name, tool.Description, propertiesElement);
        Console.WriteLine($"Tool definition: {def}");
        toolDefinitions.Add(def);
        ```

        Giriş şeması araç yanıtının bir parçasıdır, ancak "properties" özniteliğinde bulunur, bu nedenle çıkarmamız gerekir. Ayrıca, araç ayrıntılarıyla `ConvertFrom` çağrısı yapıyoruz. Şimdi ağır işleri tamamladık, bir kullanıcı istemini işlerken her şeyin nasıl bir araya geldiğini görelim.

#### Java

```java
// Create a Bot interface for natural language interaction
public interface Bot {
    String chat(String prompt);
}

// Configure the AI service with LLM and MCP tools
Bot bot = AiServices.builder(Bot.class)
        .chatLanguageModel(model)
        .toolProvider(toolProvider)
        .build();
```

Yukarıdaki kodda şunları yaptık:

- Doğal dil etkileşimleri için basit bir `Bot` arayüzü tanımladık.
- LangChain4j'nin `AiServices`'ini kullanarak LLM'yi MCP araç sağlayıcısıyla otomatik olarak bağladık.
- Çerçeve, araç şeması dönüştürme ve işlev çağrısını sahne arkasında otomatik olarak yönetir.
- Bu yaklaşım, MCP araçlarını LLM uyumlu bir formata dönüştürme sürecini ortadan kaldırır - LangChain4j, MCP araçlarını LLM uyumlu bir formata dönüştürmenin tüm karmaşıklığını yönetir.

#### Rust

MCP araç yanıtını LLM'nin anlayabileceği bir formata dönüştürmek için, araç listesini biçimlendiren bir yardımcı fonksiyon ekleyeceğiz. Bu, LLM'ye istek yaparken çağrılacaktır:

```rust
async fn format_tools(tools: &ListToolsResult) -> Result<Vec<Value>, Box<dyn Error>> {
    let tools_json = serde_json::to_value(tools)?;
    let Some(tools_array) = tools_json.get("tools").and_then(|t| t.as_array()) else {
        return Ok(vec![]);
    };

    let formatted_tools = tools_array
        .iter()
        .filter_map(|tool| {
            let name = tool.get("name")?.as_str()?;
            let description = tool.get("description")?.as_str()?;
            let schema = tool.get("inputSchema")?;

            Some(json!({
                "type": "function",
                "function": {
                    "name": name,
                    "description": description,
                    "parameters": {
                        "type": "object",
                        "properties": schema.get("properties").unwrap_or(&json!({})),
                        "required": schema.get("required").unwrap_or(&json!([]))
                    }
                }
            }))
        })
        .collect();

    Ok(formatted_tools)
}
```

Harika, artık kullanıcı isteklerini işlemek için hazırız, o zaman bir sonraki adımı ele alalım.

### -4- Kullanıcı İstemini İşleme

Bu kod bölümünde, kullanıcı isteklerini işleyeceğiz.

#### TypeScript

1. LLM'yi çağırmak için kullanılacak bir yöntem ekleyin:

    ```typescript
    async callTools(
        tool_calls: OpenAI.Chat.Completions.ChatCompletionMessageToolCall[],
        toolResults: any[]
    ) {
        for (const tool_call of tool_calls) {
        const toolName = tool_call.function.name;
        const args = tool_call.function.arguments;

        console.log(`Calling tool ${toolName} with args ${JSON.stringify(args)}`);


        // 2. Call the server's tool 
        const toolResult = await this.client.callTool({
            name: toolName,
            arguments: JSON.parse(args),
        });

        console.log("Tool result: ", toolResult);

        // 3. Do something with the result
        // TODO  

        }
    }
    ```

    Yukarıdaki kodda şunları yaptık:

    - `callTools` adında bir yöntem ekledik.
    - Yöntem, bir LLM yanıtını alır ve herhangi bir araç çağrılıp çağrılmadığını kontrol eder:

        ```typescript
        for (const tool_call of tool_calls) {
        const toolName = tool_call.function.name;
        const args = tool_call.function.arguments;

        console.log(`Calling tool ${toolName} with args ${JSON.stringify(args)}`);

        // call tool
        }
        ```

    - LLM'nin çağrılması gerektiğini belirttiği bir aracı çağırır:

        ```typescript
        // 2. Call the server's tool 
        const toolResult = await this.client.callTool({
            name: toolName,
            arguments: JSON.parse(args),
        });

        console.log("Tool result: ", toolResult);

        // 3. Do something with the result
        // TODO  
        ```

1. `run` yöntemini LLM çağrılarını ve `callTools` çağrılarını içerecek şekilde güncelleyin:

    ```typescript

    // 1. Create messages that's input for the LLM
    const prompt = "What is the sum of 2 and 3?"

    const messages: OpenAI.Chat.Completions.ChatCompletionMessageParam[] = [
            {
                role: "user",
                content: prompt,
            },
        ];

    console.log("Querying LLM: ", messages[0].content);

    // 2. Calling the LLM
    let response = this.openai.chat.completions.create({
        model: "gpt-4o-mini",
        max_tokens: 1000,
        messages,
        tools: tools,
    });    

    let results: any[] = [];

    // 3. Go through the LLM response,for each choice, check if it has tool calls 
    (await response).choices.map(async (choice: { message: any; }) => {
        const message = choice.message;
        if (message.tool_calls) {
            console.log("Making tool call")
            await this.callTools(message.tool_calls, results);
        }
    });
    ```

Harika, kodu tam olarak listeleyelim:

```typescript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";
import { Transport } from "@modelcontextprotocol/sdk/shared/transport.js";
import OpenAI from "openai";
import { z } from "zod"; // Import zod for schema validation

class MyClient {
    private openai: OpenAI;
    private client: Client;
    constructor(){
        this.openai = new OpenAI({
            baseURL: "https://models.inference.ai.azure.com", // might need to change to this url in the future: https://models.github.ai/inference
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

    async connectToServer(transport: Transport) {
        await this.client.connect(transport);
        this.run();
        console.error("MCPClient started on stdin/stdout");
    }

    openAiToolAdapter(tool: {
        name: string;
        description?: string;
        input_schema: any;
          }) {
          // Create a zod schema based on the input_schema
          const schema = z.object(tool.input_schema);
      
          return {
            type: "function" as const, // Explicitly set type to "function"
            function: {
              name: tool.name,
              description: tool.description,
              parameters: {
              type: "object",
              properties: tool.input_schema.properties,
              required: tool.input_schema.required,
              },
            },
          };
    }
    
    async callTools(
        tool_calls: OpenAI.Chat.Completions.ChatCompletionMessageToolCall[],
        toolResults: any[]
      ) {
        for (const tool_call of tool_calls) {
          const toolName = tool_call.function.name;
          const args = tool_call.function.arguments;
    
          console.log(`Calling tool ${toolName} with args ${JSON.stringify(args)}`);
    
    
          // 2. Call the server's tool 
          const toolResult = await this.client.callTool({
            name: toolName,
            arguments: JSON.parse(args),
          });
    
          console.log("Tool result: ", toolResult);
    
          // 3. Do something with the result
          // TODO  
    
         }
    }

    async run() {
        console.log("Asking server for available tools");
        const toolsResult = await this.client.listTools();
        const tools = toolsResult.tools.map((tool) => {
            return this.openAiToolAdapter({
              name: tool.name,
              description: tool.description,
              input_schema: tool.inputSchema,
            });
        });

        const prompt = "What is the sum of 2 and 3?";
    
        const messages: OpenAI.Chat.Completions.ChatCompletionMessageParam[] = [
            {
                role: "user",
                content: prompt,
            },
        ];

        console.log("Querying LLM: ", messages[0].content);
        let response = this.openai.chat.completions.create({
            model: "gpt-4o-mini",
            max_tokens: 1000,
            messages,
            tools: tools,
        });    

        let results: any[] = [];
    
        // 1. Go through the LLM response,for each choice, check if it has tool calls 
        (await response).choices.map(async (choice: { message: any; }) => {
          const message = choice.message;
          if (message.tool_calls) {
              console.log("Making tool call")
              await this.callTools(message.tool_calls, results);
          }
        });
    }
    
}

let client = new MyClient();
 const transport = new StdioClientTransport({
            command: "node",
            args: ["./build/index.js"]
        });

client.connectToServer(transport);
```

#### Python

1. LLM'yi çağırmak için gereken bazı içe aktarmaları ekleyelim:

    ```python
    # llm
    import os
    from azure.ai.inference import ChatCompletionsClient
    from azure.ai.inference.models import SystemMessage, UserMessage
    from azure.core.credentials import AzureKeyCredential
    import json
    ```

1. Ardından, LLM'yi çağıracak fonksiyonu ekleyelim:

    ```python
    # llm

    def call_llm(prompt, functions):
        token = os.environ["GITHUB_TOKEN"]
        endpoint = "https://models.inference.ai.azure.com"

        model_name = "gpt-4o"

        client = ChatCompletionsClient(
            endpoint=endpoint,
            credential=AzureKeyCredential(token),
        )

        print("CALLING LLM")
        response = client.complete(
            messages=[
                {
                "role": "system",
                "content": "You are a helpful assistant.",
                },
                {
                "role": "user",
                "content": prompt,
                },
            ],
            model=model_name,
            tools = functions,
            # Optional parameters
            temperature=1.,
            max_tokens=1000,
            top_p=1.    
        )

        response_message = response.choices[0].message
        
        functions_to_call = []

        if response_message.tool_calls:
            for tool_call in response_message.tool_calls:
                print("TOOL: ", tool_call)
                name = tool_call.function.name
                args = json.loads(tool_call.function.arguments)
                functions_to_call.append({ "name": name, "args": args })

        return functions_to_call
    ```

    Yukarıdaki kodda şunları yaptık:

    - MCP sunucusundan bulduğumuz ve dönüştürdüğümüz işlevleri LLM'ye ilettik.
    - Ardından, bu işlevlerle LLM'yi çağırdık.
    - Daha sonra, sonucu inceleyerek çağrılması gereken işlevleri kontrol ettik.
    - Son olarak, çağrılacak işlevlerin bir dizisini ilettik.

1. Son adım, ana kodumuzu güncelleyelim:

    ```python
    prompt = "Add 2 to 20"

    # ask LLM what tools to all, if any
    functions_to_call = call_llm(prompt, functions)

    # call suggested functions
    for f in functions_to_call:
        result = await session.call_tool(f["name"], arguments=f["args"])
        print("TOOLS result: ", result.content)
    ```

    İşte bu, son adımdı. Yukarıdaki kodda şunları yapıyoruz:

    - LLM'nin çağrılması gerektiğini düşündüğü bir işlevi kullanarak `call_tool` aracılığıyla bir MCP aracını çağırıyoruz.
    - MCP Sunucusuna yapılan araç çağrısının sonucunu yazdırıyoruz.

#### .NET

1. Bir LLM istemi isteği yapmak için bazı kodlar gösterelim:

    ```csharp
    var tools = await GetMcpTools();

    for (int i = 0; i < tools.Count; i++)
    {
        var tool = tools[i];
        Console.WriteLine($"MCP Tools def: {i}: {tool}");
    }

    // 0. Define the chat history and the user message
    var userMessage = "add 2 and 4";

    chatHistory.Add(new ChatRequestUserMessage(userMessage));

    // 1. Define tools
    ChatCompletionsToolDefinition def = CreateToolDefinition();


    // 2. Define options, including the tools
    var options = new ChatCompletionsOptions(chatHistory)
    {
        Model = "gpt-4o-mini",
        Tools = { tools[0] }
    };

    // 3. Call the model  

    ChatCompletions? response = await client.CompleteAsync(options);
    var content = response.Content;

    ```

    Yukarıdaki kodda şunları yaptık:

    - MCP sunucusundan araçları aldık, `var tools = await GetMcpTools()`.
    - Bir kullanıcı istemi `userMessage` tanımladık.
    - Model ve araçları belirten bir seçenekler nesnesi oluşturduk.
    - LLM'ye bir istek yaptık.

1. Son bir adım, LLM'nin bir işlev çağrısı yapmamız gerektiğini düşünüp düşünmediğini görelim:

    ```csharp
    // 4. Check if the response contains a function call
    ChatCompletionsToolCall? calls = response.ToolCalls.FirstOrDefault();
    for (int i = 0; i < response.ToolCalls.Count; i++)
    {
        var call = response.ToolCalls[i];
        Console.WriteLine($"Tool call {i}: {call.Name} with arguments {call.Arguments}");
        //Tool call 0: add with arguments {"a":2,"b":4}

        var dict = JsonSerializer.Deserialize<Dictionary<string, object>>(call.Arguments);
        var result = await mcpClient.CallToolAsync(
            call.Name,
            dict!,
            cancellationToken: CancellationToken.None
        );

        Console.WriteLine(result.Content.First(c => c.Type == "text").Text);

    }
    ```

    Yukarıdaki kodda şunları yaptık:

    - Bir işlev çağrıları listesi arasında döngü yaptık.
    - Her araç çağrısı için, adı ve argümanları ayrıştırdık ve MCP istemcisini kullanarak MCP sunucusundaki aracı çağırdık. Son olarak sonuçları yazdırdık.

İşte tam kod:

```csharp
using Azure;
using Azure.AI.Inference;
using Azure.Identity;
using System.Text.Json;
using ModelContextProtocol.Client;
using ModelContextProtocol.Protocol.Transport;
using System.Text.Json;

var endpoint = "https://models.inference.ai.azure.com";
var token = Environment.GetEnvironmentVariable("GITHUB_TOKEN"); // Your GitHub Access Token
var client = new ChatCompletionsClient(new Uri(endpoint), new AzureKeyCredential(token));
var chatHistory = new List<ChatRequestMessage>
{
    new ChatRequestSystemMessage("You are a helpful assistant that knows about AI")
};

var clientTransport = new StdioClientTransport(new()
{
    Name = "Demo Server",
    Command = "/workspaces/mcp-for-beginners/03-GettingStarted/02-client/solution/server/bin/Debug/net8.0/server",
    Arguments = [],
});

Console.WriteLine("Setting up stdio transport");

await using var mcpClient = await McpClientFactory.CreateAsync(clientTransport);

ChatCompletionsToolDefinition ConvertFrom(string name, string description, JsonElement jsonElement)
{ 
    // convert the tool to a function definition
    FunctionDefinition functionDefinition = new FunctionDefinition(name)
    {
        Description = description,
        Parameters = BinaryData.FromObjectAsJson(new
        {
            Type = "object",
            Properties = jsonElement
        },
        new JsonSerializerOptions() { PropertyNamingPolicy = JsonNamingPolicy.CamelCase })
    };

    // create a tool definition
    ChatCompletionsToolDefinition toolDefinition = new ChatCompletionsToolDefinition(functionDefinition);
    return toolDefinition;
}



async Task<List<ChatCompletionsToolDefinition>> GetMcpTools()
{
    Console.WriteLine("Listing tools");
    var tools = await mcpClient.ListToolsAsync();

    List<ChatCompletionsToolDefinition> toolDefinitions = new List<ChatCompletionsToolDefinition>();

    foreach (var tool in tools)
    {
        Console.WriteLine($"Connected to server with tools: {tool.Name}");
        Console.WriteLine($"Tool description: {tool.Description}");
        Console.WriteLine($"Tool parameters: {tool.JsonSchema}");

        JsonElement propertiesElement;
        tool.JsonSchema.TryGetProperty("properties", out propertiesElement);

        var def = ConvertFrom(tool.Name, tool.Description, propertiesElement);
        Console.WriteLine($"Tool definition: {def}");
        toolDefinitions.Add(def);

        Console.WriteLine($"Properties: {propertiesElement}");        
    }

    return toolDefinitions;
}

// 1. List tools on mcp server

var tools = await GetMcpTools();
for (int i = 0; i < tools.Count; i++)
{
    var tool = tools[i];
    Console.WriteLine($"MCP Tools def: {i}: {tool}");
}

// 2. Define the chat history and the user message
var userMessage = "add 2 and 4";

chatHistory.Add(new ChatRequestUserMessage(userMessage));


// 3. Define options, including the tools
var options = new ChatCompletionsOptions(chatHistory)
{
    Model = "gpt-4o-mini",
    Tools = { tools[0] }
};

// 4. Call the model  

ChatCompletions? response = await client.CompleteAsync(options);
var content = response.Content;

// 5. Check if the response contains a function call
ChatCompletionsToolCall? calls = response.ToolCalls.FirstOrDefault();
for (int i = 0; i < response.ToolCalls.Count; i++)
{
    var call = response.ToolCalls[i];
    Console.WriteLine($"Tool call {i}: {call.Name} with arguments {call.Arguments}");
    //Tool call 0: add with arguments {"a":2,"b":4}

    var dict = JsonSerializer.Deserialize<Dictionary<string, object>>(call.Arguments);
    var result = await mcpClient.CallToolAsync(
        call.Name,
        dict!,
        cancellationToken: CancellationToken.None
    );

    Console.WriteLine(result.Content.First(c => c.Type == "text").Text);

}

// 5. Print the generic response
Console.WriteLine($"Assistant response: {content}");
```

#### Java

```java
try {
    // Execute natural language requests that automatically use MCP tools
    String response = bot.chat("Calculate the sum of 24.5 and 17.3 using the calculator service");
    System.out.println(response);

    response = bot.chat("What's the square root of 144?");
    System.out.println(response);

    response = bot.chat("Show me the help for the calculator service");
    System.out.println(response);
} finally {
    mcpClient.close();
}
```

Yukarıdaki kodda şunları yaptık:

- MCP sunucusu araçlarıyla etkileşim kurmak için basit doğal dil istemlerini kullandık.
- LangChain4j çerçevesi otomatik olarak şunları yönetir:
  - Kullanıcı istemlerini gerektiğinde araç çağrılarına dönüştürme.
  - LLM'nin kararına göre uygun MCP araçlarını çağırma.
  - LLM ve MCP sunucusu arasındaki konuşma akışını yönetme.
- `bot.chat()` yöntemi, MCP araç yürütmelerinden gelen sonuçları içerebilecek doğal dil yanıtları döndürür.
- Bu yaklaşım, kullanıcıların temel MCP uygulamasını bilmesine gerek kalmadan sorunsuz bir kullanıcı deneyimi sağlar.

Tam kod örneği:

```java
public class LangChain4jClient {
    
    public static void main(String[] args) throws Exception {        ChatLanguageModel model = OpenAiOfficialChatModel.builder()
                .isGitHubModels(true)
                .apiKey(System.getenv("GITHUB_TOKEN"))
                .timeout(Duration.ofSeconds(60))
                .modelName("gpt-4.1-nano")
                .timeout(Duration.ofSeconds(60))
                .build();

        McpTransport transport = new HttpMcpTransport.Builder()
                .sseUrl("http://localhost:8080/sse")
                .timeout(Duration.ofSeconds(60))
                .logRequests(true)
                .logResponses(true)
                .build();

        McpClient mcpClient = new DefaultMcpClient.Builder()
                .transport(transport)
                .build();

        ToolProvider toolProvider = McpToolProvider.builder()
                .mcpClients(List.of(mcpClient))
                .build();

        Bot bot = AiServices.builder(Bot.class)
                .chatLanguageModel(model)
                .toolProvider(toolProvider)
                .build();

        try {
            String response = bot.chat("Calculate the sum of 24.5 and 17.3 using the calculator service");
            System.out.println(response);

            response = bot.chat("What's the square root of 144?");
            System.out.println(response);

            response = bot.chat("Show me the help for the calculator service");
            System.out.println(response);
        } finally {
            mcpClient.close();
        }
    }
}
```

#### Rust

Burada işin çoğu gerçekleşir. Başlangıçtaki kullanıcı istemiyle LLM'yi çağıracağız, ardından yanıtı işleyerek herhangi bir aracın çağrılması gerekip gerekmediğini kontrol edeceğiz. Eğer gerekiyorsa, bu araçları çağıracağız ve LLM ile nihai bir yanıt alana kadar konuşmaya devam edeceğiz.
Ana dosyanıza aşağıdaki işlevi ekleyerek LLM çağrısını gerçekleştirecek bir işlev tanımlayalım:

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

Bu işlev, LLM istemcisini, kullanıcı istemi dahil olmak üzere bir mesaj listesini, MCP sunucusundan araçları alır ve LLM'e bir istek göndererek yanıtı döndürür.

LLM'den gelen yanıt, `choices` adlı bir dizi içerecektir. Sonuçları işleyerek herhangi bir `tool_calls` olup olmadığını kontrol etmemiz gerekecek. Bu, LLM'in belirli bir aracın argümanlarla çağrılmasını istediğini gösterir. LLM yanıtını işlemek için ana dosyanızın sonuna aşağıdaki kodu ekleyerek bir işlev tanımlayın:

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

Eğer `tool_calls` mevcutsa, araç bilgilerini çıkarır, MCP sunucusuna araç isteğiyle çağrı yapar ve sonuçları konuşma mesajlarına ekler. Daha sonra LLM ile konuşmaya devam eder ve mesajlar, asistanın yanıtı ve araç çağrısı sonuçları ile güncellenir.

LLM'in MCP çağrıları için döndürdüğü araç çağrısı bilgilerini çıkarmak için, çağrı yapmak için gereken her şeyi çıkaran bir yardımcı işlev ekleyeceğiz. Ana dosyanızın sonuna aşağıdaki kodu ekleyin:

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

Tüm parçalar hazır olduğunda, artık ilk kullanıcı istemini işleyebilir ve LLM'i çağırabiliriz. `main` işlevinizi aşağıdaki kodu ekleyerek güncelleyin:

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

Bu, iki sayının toplamını sormak için ilk kullanıcı istemiyle LLM'i sorgular ve yanıtı işleyerek araç çağrılarını dinamik olarak yönetir.

Harika, başardınız!

## Görev

Egzersizdeki kodu alarak sunucuyu daha fazla araçla geliştirin. Ardından, egzersizde olduğu gibi bir LLM içeren bir istemci oluşturun ve sunucu araçlarınızın dinamik olarak çağrıldığından emin olmak için farklı istemlerle test edin. Bu tür bir istemci oluşturmak, son kullanıcıya harika bir kullanıcı deneyimi sağlar çünkü istemleri kullanabilirler ve herhangi bir MCP sunucusunun çağrıldığından habersiz olurlar.

## Çözüm

[Çözüm](/03-GettingStarted/03-llm-client/solution/README.md)

## Önemli Noktalar

- İstemcinize bir LLM eklemek, kullanıcıların MCP Sunucuları ile etkileşim kurması için daha iyi bir yol sağlar.
- MCP Sunucusu yanıtını LLM'in anlayabileceği bir forma dönüştürmeniz gerekir.

## Örnekler

- [Java Hesap Makinesi](../samples/java/calculator/README.md)
- [.Net Hesap Makinesi](../../../../03-GettingStarted/samples/csharp)
- [JavaScript Hesap Makinesi](../samples/javascript/README.md)
- [TypeScript Hesap Makinesi](../samples/typescript/README.md)
- [Python Hesap Makinesi](../../../../03-GettingStarted/samples/python)
- [Rust Hesap Makinesi](../../../../03-GettingStarted/samples/rust)

## Ek Kaynaklar

## Sırada Ne Var

- Sıradaki: [Visual Studio Code kullanarak bir sunucu tüketmek](../04-vscode/README.md)

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hata veya yanlışlıklar içerebileceğini lütfen unutmayın. Belgenin orijinal dili, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalardan sorumlu değiliz.