<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "94c80ae71fb9971e9b57b51ab0912121",
<<<<<<< HEAD
  "translation_date": "2025-08-18T23:06:16+00:00",
=======
  "translation_date": "2025-08-18T18:27:48+00:00",
>>>>>>> origin/main
  "source_file": "03-GettingStarted/02-client/README.md",
  "language_code": "uk"
}
-->
# Створення клієнта

<<<<<<< HEAD
Клієнти — це спеціальні програми або скрипти, які безпосередньо взаємодіють із сервером MCP для запиту ресурсів, інструментів і підказок. На відміну від використання інструменту інспектора, який забезпечує графічний інтерфейс для взаємодії із сервером, написання власного клієнта дозволяє програмувати та автоматизувати взаємодії. Це дає змогу розробникам інтегрувати можливості MCP у власні робочі процеси, автоматизувати завдання та створювати індивідуальні рішення, адаптовані до конкретних потреб.

## Огляд

У цьому уроці розглядається концепція клієнтів у екосистемі Model Context Protocol (MCP). Ви дізнаєтеся, як написати власного клієнта та підключити його до сервера MCP.
=======
Клієнти — це спеціальні програми або скрипти, які безпосередньо взаємодіють із сервером MCP для запиту ресурсів, інструментів і підказок. На відміну від використання інспектора, який надає графічний інтерфейс для взаємодії із сервером, написання власного клієнта дозволяє програмувати та автоматизувати взаємодії. Це дає змогу розробникам інтегрувати можливості MCP у власні робочі процеси, автоматизувати завдання та створювати індивідуальні рішення, адаптовані до конкретних потреб.

## Огляд

У цьому уроці ми розглянемо концепцію клієнтів у екосистемі Model Context Protocol (MCP). Ви дізнаєтеся, як написати власного клієнта та підключити його до сервера MCP.
>>>>>>> origin/main

## Навчальні цілі

До кінця цього уроку ви зможете:

- Зрозуміти, що може робити клієнт.
- Написати власного клієнта.
- Підключити та протестувати клієнта із сервером MCP, щоб переконатися, що він працює належним чином.

## Що потрібно для написання клієнта?

<<<<<<< HEAD
Щоб написати клієнта, необхідно виконати наступне:

- **Імпортувати потрібні бібліотеки**. Ви будете використовувати ту саму бібліотеку, що й раніше, але з іншими конструкціями.
- **Створити екземпляр клієнта**. Це передбачає створення екземпляра клієнта та підключення його до обраного методу транспортування.
- **Визначити, які ресурси перелічити**. Ваш сервер MCP має ресурси, інструменти та підказки, і вам потрібно вирішити, які з них перелічити.
- **Інтегрувати клієнта в основну програму**. Як тільки ви дізнаєтеся про можливості сервера, потрібно інтегрувати це у вашу основну програму, щоб, якщо користувач введе підказку або іншу команду, відповідна функція сервера була викликана.
=======
Щоб написати клієнта, вам потрібно виконати наступне:

- **Імпортувати необхідні бібліотеки**. Ви будете використовувати ту саму бібліотеку, що й раніше, але з іншими конструкціями.
- **Інстанціювати клієнта**. Це передбачає створення екземпляра клієнта та підключення його до обраного методу транспорту.
- **Визначити, які ресурси перерахувати**. Ваш сервер MCP має ресурси, інструменти та підказки, і вам потрібно вирішити, які з них перерахувати.
- **Інтегрувати клієнта в хост-додаток**. Після того, як ви дізнаєтеся про можливості сервера, вам потрібно інтегрувати це у ваш хост-додаток, щоб, коли користувач вводить підказку або іншу команду, викликалася відповідна функція сервера.
>>>>>>> origin/main

Тепер, коли ми розуміємо на високому рівні, що ми збираємося робити, давайте розглянемо приклад.

### Приклад клієнта

Розглянемо приклад клієнта:

### TypeScript

```typescript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";

const transport = new StdioClientTransport({
  command: "node",
  args: ["server.js"]
});

const client = new Client(
  {
    name: "example-client",
    version: "1.0.0"
  }
);

await client.connect(transport);

// List prompts
const prompts = await client.listPrompts();

// Get a prompt
const prompt = await client.getPrompt({
  name: "example-prompt",
  arguments: {
    arg1: "value"
  }
});

// List resources
const resources = await client.listResources();

// Read a resource
const resource = await client.readResource({
  uri: "file:///example.txt"
});

// Call a tool
const result = await client.callTool({
  name: "example-tool",
  arguments: {
    arg1: "value"
  }
});
```

У наведеному вище коді ми:

- Імпортуємо бібліотеки.
<<<<<<< HEAD
- Створюємо екземпляр клієнта та підключаємо його за допомогою stdio для транспортування.
- Перелічуємо підказки, ресурси та інструменти та викликаємо їх усі.
=======
- Створюємо екземпляр клієнта та підключаємо його за допомогою stdio як транспорту.
- Перераховуємо підказки, ресурси та інструменти та викликаємо їх усі.
>>>>>>> origin/main

Ось і все, клієнт, який може взаємодіяти із сервером MCP.

Давайте детально розглянемо кожен фрагмент коду в наступному розділі вправ.

## Вправа: Написання клієнта

Як зазначено вище, давайте детально пояснимо код, і, якщо хочете, пишіть код разом із нами.

### -1- Імпорт бібліотек

<<<<<<< HEAD
Імпортуємо потрібні бібліотеки. Нам знадобляться посилання на клієнта та обраний транспортний протокол, stdio. stdio — це протокол для програм, які мають працювати на вашому локальному комп’ютері. SSE — це ще один транспортний протокол, який ми покажемо в майбутніх розділах, але це ваш інший варіант. Поки що продовжимо зі stdio.
=======
Імпортуємо необхідні бібліотеки. Нам знадобляться посилання на клієнта та обраний транспортний протокол, stdio. stdio — це протокол для програм, які запускаються на вашій локальній машині. SSE — це інший транспортний протокол, який ми розглянемо в майбутніх розділах, але це ваш інший варіант. Зараз же продовжимо зі stdio.
>>>>>>> origin/main

#### TypeScript

```typescript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";
```

#### Python

```python
from mcp import ClientSession, StdioServerParameters, types
from mcp.client.stdio import stdio_client
```

#### .NET

```csharp
using Microsoft.Extensions.AI;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Hosting;
using ModelContextProtocol.Client;
using ModelContextProtocol.Protocol.Transport;
```

#### Java

<<<<<<< HEAD
Для Java ви створите клієнта, який підключається до сервера MCP з попередньої вправи. Використовуючи ту саму структуру проекту Java Spring Boot із розділу [Getting Started with MCP Server](../../../../03-GettingStarted/01-first-server/solution/java), створіть новий клас Java під назвою `SDKClient` у папці `src/main/java/com/microsoft/mcp/sample/client/` і додайте наступні імпорти:
=======
Для Java вам потрібно створити клієнта, який підключається до сервера MCP із попередньої вправи. Використовуючи ту саму структуру проекту Java Spring Boot із [Початок роботи з сервером MCP](../../../../03-GettingStarted/01-first-server/solution/java), створіть новий клас Java під назвою `SDKClient` у папці `src/main/java/com/microsoft/mcp/sample/client/` і додайте наступні імпорти:
>>>>>>> origin/main

```java
import java.util.Map;
import org.springframework.web.reactive.function.client.WebClient;
import io.modelcontextprotocol.client.McpClient;
import io.modelcontextprotocol.client.transport.WebFluxSseClientTransport;
import io.modelcontextprotocol.spec.McpClientTransport;
import io.modelcontextprotocol.spec.McpSchema.CallToolRequest;
import io.modelcontextprotocol.spec.McpSchema.CallToolResult;
import io.modelcontextprotocol.spec.McpSchema.ListToolsResult;
```

#### Rust
<<<<<<< HEAD

Вам потрібно додати наступні залежності до вашого файлу `Cargo.toml`.

```toml
[package]
name = "calculator-client"
version = "0.1.0"
edition = "2024"

[dependencies]
rmcp = { version = "0.5.0", features = ["client", "transport-child-process"] }
serde_json = "1.0.141"
tokio = { version = "1.46.1", features = ["rt-multi-thread"] }
```

Після цього ви можете імпортувати необхідні бібліотеки у вашому коді клієнта.

```rust
use rmcp::{
    RmcpError,
    model::CallToolRequestParam,
    service::ServiceExt,
    transport::{ConfigureCommandExt, TokioChildProcess},
};
use tokio::process::Command;
```

Переходимо до створення екземпляра.
=======
>>>>>>> origin/main

Вам потрібно додати наступні залежності до вашого файлу `Cargo.toml`.

<<<<<<< HEAD
Нам потрібно створити екземпляр транспорту та клієнта:

=======
```toml
[package]
name = "calculator-client"
version = "0.1.0"
edition = "2024"

[dependencies]
rmcp = { version = "0.5.0", features = ["client", "transport-child-process"] }
serde_json = "1.0.141"
tokio = { version = "1.46.1", features = ["rt-multi-thread"] }
```

Після цього ви можете імпортувати необхідні бібліотеки у вашому коді клієнта.

```rust
use rmcp::{
    RmcpError,
    model::CallToolRequestParam,
    service::ServiceExt,
    transport::{ConfigureCommandExt, TokioChildProcess},
};
use tokio::process::Command;
```

Переходимо до інстанціювання.

### -2- Інстанціювання клієнта та транспорту

Нам потрібно створити екземпляр транспорту та клієнта:

>>>>>>> origin/main
#### TypeScript

```typescript
const transport = new StdioClientTransport({
  command: "node",
  args: ["server.js"]
});

const client = new Client(
  {
    name: "example-client",
    version: "1.0.0"
  }
);

await client.connect(transport);
```

У наведеному вище коді ми:

- Створили екземпляр транспорту stdio. Зверніть увагу, як він вказує команду та аргументи для пошуку та запуску сервера, оскільки це те, що нам потрібно зробити під час створення клієнта.

    ```typescript
    const transport = new StdioClientTransport({
        command: "node",
        args: ["server.js"]
    });
    ```

<<<<<<< HEAD
- Створили екземпляр клієнта, вказавши його ім’я та версію.
=======
- Інстанціювали клієнта, вказавши його ім'я та версію.
>>>>>>> origin/main

    ```typescript
    const client = new Client(
    {
        name: "example-client",
        version: "1.0.0"
    });
    ```

- Підключили клієнта до обраного транспорту.

    ```typescript
    await client.connect(transport);
    ```

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

У наведеному вище коді ми:

<<<<<<< HEAD
- Імпортували потрібні бібліотеки.
- Створили об’єкт параметрів сервера, який ми будемо використовувати для запуску сервера, щоб підключитися до нього за допомогою клієнта.
- Визначили метод `run`, який викликає `stdio_client`, що запускає сесію клієнта.
- Створили точку входу, де ми передаємо метод `run` до `asyncio.run`.
=======
- Імпортували необхідні бібліотеки.
- Створили об'єкт параметрів сервера, який ми будемо використовувати для запуску сервера, щоб підключитися до нього нашим клієнтом.
- Визначили метод `run`, який, у свою чергу, викликає `stdio_client`, що запускає сесію клієнта.
- Створили точку входу, де ми передаємо метод `run` у `asyncio.run`.
>>>>>>> origin/main

#### .NET

```dotnet
using Microsoft.Extensions.AI;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Hosting;
using ModelContextProtocol.Client;
using ModelContextProtocol.Protocol.Transport;

var builder = Host.CreateApplicationBuilder(args);

builder.Configuration
    .AddEnvironmentVariables()
    .AddUserSecrets<Program>();



var clientTransport = new StdioClientTransport(new()
{
    Name = "Demo Server",
    Command = "dotnet",
    Arguments = ["run", "--project", "path/to/file.csproj"],
});

await using var mcpClient = await McpClientFactory.CreateAsync(clientTransport);
```

У наведеному вище коді ми:

<<<<<<< HEAD
- Імпортували потрібні бібліотеки.
- Створили транспорт stdio та клієнта `mcpClient`. Останній ми будемо використовувати для переліку та виклику функцій на сервері MCP.
=======
- Імпортували необхідні бібліотеки.
- Створили транспорт stdio та клієнт `mcpClient`. Останній ми будемо використовувати для перерахування та виклику функцій на сервері MCP.
>>>>>>> origin/main

Зверніть увагу, що в "Arguments" ви можете вказати або *.csproj*, або виконуваний файл.

#### Java

```java
public class SDKClient {
    
    public static void main(String[] args) {
        var transport = new WebFluxSseClientTransport(WebClient.builder().baseUrl("http://localhost:8080"));
        new SDKClient(transport).run();
    }
    
    private final McpClientTransport transport;

    public SDKClient(McpClientTransport transport) {
        this.transport = transport;
    }

    public void run() {
        var client = McpClient.sync(this.transport).build();
        client.initialize();
        
        // Your client logic goes here
    }
}
```

У наведеному вище коді ми:

<<<<<<< HEAD
- Створили основний метод, який налаштовує транспорт SSE, що вказує на `http://localhost:8080`, де працюватиме наш сервер MCP.
- Створили клас клієнта, який приймає транспорт як параметр конструктора.
- У методі `run` створили синхронного клієнта MCP, використовуючи транспорт, і ініціалізували з’єднання.
- Використали транспорт SSE (події, що надсилаються сервером), який підходить для HTTP-зв’язку з серверами MCP на основі Java Spring Boot.

#### Rust

Цей клієнт Rust припускає, що сервер є сусіднім проектом під назвою "calculator-server" у тому ж каталозі. Код нижче запустить сервер і підключиться до нього.

```rust
async fn main() -> Result<(), RmcpError> {
    // Assume the server is a sibling project named "calculator-server" in the same directory
    let server_dir = std::path::Path::new(env!("CARGO_MANIFEST_DIR"))
        .parent()
        .expect("failed to locate workspace root")
        .join("calculator-server");

    let client = ()
        .serve(
            TokioChildProcess::new(Command::new("cargo").configure(|cmd| {
                cmd.arg("run").current_dir(server_dir);
            }))
            .map_err(RmcpError::transport_creation::<TokioChildProcess>)?,
        )
        .await?;

    // TODO: Initialize

    // TODO: List tools

    // TODO: Call add tool with arguments = {"a": 3, "b": 2}

    client.cancel().await?;
    Ok(())
}
```
=======
- Створили основний метод, який налаштовує транспорт SSE, що вказує на `http://localhost:8080`, де буде працювати наш сервер MCP.
- Створили клас клієнта, який приймає транспорт як параметр конструктора.
- У методі `run` створили синхронного клієнта MCP, використовуючи транспорт, і ініціалізували з'єднання.
- Використали транспорт SSE (події, що надсилаються сервером), який підходить для HTTP-зв'язку з серверами MCP на основі Java Spring Boot.
>>>>>>> origin/main

#### Rust

<<<<<<< HEAD
Тепер у нас є клієнт, який може підключатися, якщо програма запущена. Однак він фактично не перелічує свої функції, тому зробимо це далі:

=======
Цей клієнт Rust передбачає, що сервер є сусіднім проектом під назвою "calculator-server" у тій самій директорії. Код нижче запустить сервер і підключиться до нього.

```rust
async fn main() -> Result<(), RmcpError> {
    // Assume the server is a sibling project named "calculator-server" in the same directory
    let server_dir = std::path::Path::new(env!("CARGO_MANIFEST_DIR"))
        .parent()
        .expect("failed to locate workspace root")
        .join("calculator-server");

    let client = ()
        .serve(
            TokioChildProcess::new(Command::new("cargo").configure(|cmd| {
                cmd.arg("run").current_dir(server_dir);
            }))
            .map_err(RmcpError::transport_creation::<TokioChildProcess>)?,
        )
        .await?;

    // TODO: Initialize

    // TODO: List tools

    // TODO: Call add tool with arguments = {"a": 3, "b": 2}

    client.cancel().await?;
    Ok(())
}
```

### -3- Перерахування функцій сервера

Тепер у нас є клієнт, який може підключатися, якщо програма запущена. Однак він ще не перераховує свої функції, тому зробимо це далі:

>>>>>>> origin/main
#### TypeScript

```typescript
// List prompts
const prompts = await client.listPrompts();

// List resources
const resources = await client.listResources();

// list tools
const tools = await client.listTools();
```

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
```

<<<<<<< HEAD
Тут ми перелічуємо доступні ресурси за допомогою `list_resources()` та інструменти за допомогою `list_tools` і виводимо їх.
=======
Тут ми перераховуємо доступні ресурси за допомогою `list_resources()` та інструменти за допомогою `list_tools` і виводимо їх.
>>>>>>> origin/main

#### .NET

```dotnet
foreach (var tool in await client.ListToolsAsync())
{
    Console.WriteLine($"{tool.Name} ({tool.Description})");
}
```

<<<<<<< HEAD
Наведений вище приклад показує, як ми можемо перелічити інструменти на сервері. Для кожного інструмента ми виводимо його ім’я.
=======
Наведено приклад, як можна перерахувати інструменти на сервері. Для кожного інструмента ми виводимо його ім'я.
>>>>>>> origin/main

#### Java

```java
// List and demonstrate tools
ListToolsResult toolsList = client.listTools();
System.out.println("Available Tools = " + toolsList);

// You can also ping the server to verify connection
client.ping();
```

У наведеному вище коді ми:

- Викликали `listTools()`, щоб отримати всі доступні інструменти із сервера MCP.
<<<<<<< HEAD
- Використали `ping()`, щоб перевірити, чи працює з’єднання із сервером.
- `ListToolsResult` містить інформацію про всі інструменти, включаючи їхні імена, описи та схеми вводу.

Чудово, тепер ми захопили всі функції. Тепер питання: коли ми їх використовуємо? Цей клієнт досить простий, у тому сенсі, що ми повинні явно викликати функції, коли вони нам потрібні. У наступному розділі ми створимо більш просунутого клієнта, який матиме доступ до власної великої мовної моделі (LLM). А поки що давайте подивимося, як ми можемо викликати функції на сервері:

#### Rust

У головній функції, після ініціалізації клієнта, ми можемо ініціалізувати сервер і перелічити деякі його функції.
=======
- Використали `ping()`, щоб перевірити, чи працює з'єднання із сервером.
- `ListToolsResult` містить інформацію про всі інструменти, включаючи їхні імена, описи та схеми вводу.

Чудово, тепер ми захопили всі функції. Тепер питання: коли ми їх використовуємо? Цей клієнт досить простий, у тому сенсі, що нам потрібно буде явно викликати функції, коли ми їх хочемо. У наступному розділі ми створимо більш просунутого клієнта, який матиме доступ до власної великої мовної моделі (LLM). А поки що давайте подивимося, як ми можемо викликати функції на сервері:

#### Rust

У головній функції, після ініціалізації клієнта, ми можемо ініціалізувати сервер і перерахувати деякі його функції.
>>>>>>> origin/main

```rust
// Initialize
let server_info = client.peer_info();
println!("Server info: {:?}", server_info);

// List tools
let tools = client.list_tools(Default::default()).await?;
println!("Available tools: {:?}", tools);
```

### -4- Виклик функцій

<<<<<<< HEAD
Щоб викликати функції, потрібно переконатися, що ми вказуємо правильні аргументи, а в деяких випадках — ім’я того, що ми намагаємося викликати.
=======
Щоб викликати функції, нам потрібно переконатися, що ми вказуємо правильні аргументи, а в деяких випадках і назву того, що ми намагаємося викликати.
>>>>>>> origin/main

#### TypeScript

```typescript

// Read a resource
const resource = await client.readResource({
  uri: "file:///example.txt"
});

// Call a tool
const result = await client.callTool({
  name: "example-tool",
  arguments: {
    arg1: "value"
  }
});

// call prompt
const promptResult = await client.getPrompt({
    name: "review-code",
    arguments: {
        code: "console.log(\"Hello world\")"
    }
})
```

У наведеному вище коді ми:

- Зчитуємо ресурс, викликаючи `readResource()` із зазначенням `uri`. Ось як це, ймовірно, виглядає на стороні сервера:

    ```typescript
    server.resource(
        "readFile",
        new ResourceTemplate("file://{name}", { list: undefined }),
        async (uri, { name }) => ({
          contents: [{
            uri: uri.href,
            text: `Hello, ${name}!`
          }]
        })
    );
    ```

    Наше значення `uri` `file://example.txt` відповідає `file://{name}` на сервері. `example.txt` буде зіставлено з `name`.

<<<<<<< HEAD
- Викликаємо інструмент, вказуючи його `name` та `arguments`, наприклад:
=======
- Викликаємо інструмент, вказуючи його `name` та `arguments`, ось так:
>>>>>>> origin/main

    ```typescript
    const result = await client.callTool({
        name: "example-tool",
        arguments: {
            arg1: "value"
        }
    });
    ```

- Отримуємо підказку, викликаючи `getPrompt()` із `name` та `arguments`. Код сервера виглядає так:

    ```typescript
    server.prompt(
        "review-code",
        { code: z.string() },
        ({ code }) => ({
            messages: [{
            role: "user",
            content: {
                type: "text",
                text: `Please review this code:\n\n${code}`
            }
            }]
        })
    );
    ```

<<<<<<< HEAD
    А ваш клієнтський код виглядає так, щоб відповідати тому, що оголошено на сервері:
=======
    Відповідно, ваш клієнтський код виглядає так, щоб відповідати тому, що оголошено на сервері:
>>>>>>> origin/main

    ```typescript
    const promptResult = await client.getPrompt({
        name: "review-code",
        arguments: {
            code: "console.log(\"Hello world\")"
        }
    })
    ```

#### Python

```python
# Read a resource
print("READING RESOURCE")
content, mime_type = await session.read_resource("greeting://hello")

# Call a tool
print("CALL TOOL")
result = await session.call_tool("add", arguments={"a": 1, "b": 7})
print(result.content)
```

У наведеному вище коді ми:

- Викликали ресурс під назвою `greeting` за допомогою `read_resource`.
- Викликали інструмент під назвою `add` за допомогою `call_tool`.

#### .NET

1. Додамо код для виклику інструмента:

  ```csharp
  var result = await mcpClient.CallToolAsync(
      "Add",
      new Dictionary<string, object?>() { ["a"] = 1, ["b"] = 3  },
      cancellationToken:CancellationToken.None);
  ```

<<<<<<< HEAD
1. Щоб вивести результат, ось код для обробки:
=======
1. Щоб вивести результат, ось код для обробки цього:
>>>>>>> origin/main

  ```csharp
  Console.WriteLine(result.Content.First(c => c.Type == "text").Text);
  // Sum 4
  ```

#### Java

```java
// Call various calculator tools
CallToolResult resultAdd = client.callTool(new CallToolRequest("add", Map.of("a", 5.0, "b", 3.0)));
System.out.println("Add Result = " + resultAdd);

CallToolResult resultSubtract = client.callTool(new CallToolRequest("subtract", Map.of("a", 10.0, "b", 4.0)));
System.out.println("Subtract Result = " + resultSubtract);

CallToolResult resultMultiply = client.callTool(new CallToolRequest("multiply", Map.of("a", 6.0, "b", 7.0)));
System.out.println("Multiply Result = " + resultMultiply);

CallToolResult resultDivide = client.callTool(new CallToolRequest("divide", Map.of("a", 20.0, "b", 4.0)));
System.out.println("Divide Result = " + resultDivide);

CallToolResult resultHelp = client.callTool(new CallToolRequest("help", Map.of()));
System.out.println("Help = " + resultHelp);
```

У наведеному вище коді ми:

<<<<<<< HEAD
- Викликали кілька інструментів калькулятора за допомогою методу `callTool()` із об’єктами `CallToolRequest`.
- Кожен виклик інструмента вказує ім’я інструмента та `Map` аргументів, необхідних для цього інструмента.
- Інструменти сервера очікують конкретні імена параметрів (наприклад, "a", "b" для математичних операцій).
- Результати повертаються як об’єкти `CallToolResult`, що містять відповідь сервера.
=======
- Викликали кілька інструментів калькулятора за допомогою методу `callTool()` із об'єктами `CallToolRequest`.
- Кожен виклик інструмента вказує назву інструмента та `Map` аргументів, необхідних для цього інструмента.
- Інструменти сервера очікують конкретні назви параметрів (наприклад, "a", "b" для математичних операцій).
- Результати повертаються як об'єкти `CallToolResult`, що містять відповідь від сервера.

#### Rust

```rust
// Call add tool with arguments = {"a": 3, "b": 2}
let a = 3;
let b = 2;
let tool_result = client
    .call_tool(CallToolRequestParam {
        name: "add".into(),
        arguments: serde_json::json!({ "a": a, "b": b }).as_object().cloned(),
    })
    .await?;
println!("Result of {:?} + {:?}: {:?}", a, b, tool_result);
```
>>>>>>> origin/main

#### Rust

```rust
// Call add tool with arguments = {"a": 3, "b": 2}
let a = 3;
let b = 2;
let tool_result = client
    .call_tool(CallToolRequestParam {
        name: "add".into(),
        arguments: serde_json::json!({ "a": a, "b": b }).as_object().cloned(),
    })
    .await?;
println!("Result of {:?} + {:?}: {:?}", a, b, tool_result);
```

### -5- Запуск клієнта

Щоб запустити клієнта, введіть наступну команду в терміналі:

#### TypeScript

Додайте наступний запис до розділу "scripts" у *package.json*:

```json
"client": "tsc && node build/client.js"
```

```sh
npm run client
```

#### Python

Запустіть клієнта за допомогою наступної команди:

```sh
python client.py
```

#### .NET

```sh
dotnet run
```

#### Java

Спочатку переконайтеся, що ваш сервер MCP працює на `http://localhost:8080`. Потім запустіть клієнта:

```bash
# Build you project
./mvnw clean compile

# Run the client
./mvnw exec:java -Dexec.mainClass="com.microsoft.mcp.sample.client.SDKClient"
```

<<<<<<< HEAD
Або ви можете запустити повний проект клієнта, наданий у папці рішення `03-GettingStarted\02-client\solution\java`:
=======
Або ж ви можете запустити повний проект клієнта, наданий у папці рішення `03-GettingStarted\02-client\solution\java`:
>>>>>>> origin/main

```bash
# Navigate to the solution directory
cd 03-GettingStarted/02-client/solution/java

# Build and run the JAR
./mvnw clean package
java -jar target/calculator-client-0.0.1-SNAPSHOT.jar
```

#### Rust

```bash
cargo fmt
cargo run
```

## Завдання

<<<<<<< HEAD
У цьому завданні ви використаєте те, що дізналися про створення клієнта, але створите власного клієнта.
=======
У цьому завданні ви використаєте отримані знання для створення власного клієнта.
>>>>>>> origin/main

Ось сервер, який ви можете використовувати, і який потрібно викликати через ваш клієнтський код. Спробуйте додати більше функцій до сервера, щоб зробити його цікавішим.

### TypeScript

```typescript
import { McpServer, ResourceTemplate } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

// Create an MCP server
const server = new McpServer({
  name: "Demo",
  version: "1.0.0"
});

// Add an addition tool
server.tool("add",
  { a: z.number(), b: z.number() },
  async ({ a, b }) => ({
    content: [{ type: "text", text: String(a + b) }]
  })
);

// Add a dynamic greeting resource
server.resource(
  "greeting",
  new ResourceTemplate("greeting://{name}", { list: undefined }),
  async (uri, { name }) => ({
    contents: [{
      uri: uri.href,
      text: `Hello, ${name}!`
    }]
  })
);

// Start receiving messages on stdin and sending messages on stdout

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("MCPServer started on stdin/stdout");
}

main().catch((error) => {
  console.error("Fatal error: ", error);
  process.exit(1);
});
```

### Python

```python
# server.py
from mcp.server.fastmcp import FastMCP

# Create an MCP server
mcp = FastMCP("Demo")


# Add an addition tool
@mcp.tool()
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b


# Add a dynamic greeting resource
@mcp.resource("greeting://{name}")
def get_greeting(name: str) -> str:
    """Get a personalized greeting"""
    return f"Hello, {name}!"

```

### .NET

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using ModelContextProtocol.Server;
using System.ComponentModel;

var builder = Host.CreateApplicationBuilder(args);
builder.Logging.AddConsole(consoleLogOptions =>
{
    // Configure all logs to go to stderr
    consoleLogOptions.LogToStandardErrorThreshold = LogLevel.Trace;
});

builder.Services
    .AddMcpServer()
    .WithStdioServerTransport()
    .WithToolsFromAssembly();
await builder.Build().RunAsync();

[McpServerToolType]
public static class CalculatorTool
{
    [McpServerTool, Description("Adds two numbers")]
    public static string Add(int a, int b) => $"Sum {a + b}";
}
```

<<<<<<< HEAD
Дивіться цей проект, щоб дізнатися, як [додати підказки та ресурси](https://github.com/modelcontextprotocol/csharp-sdk/blob/main/samples/EverythingServer/Program.cs).
=======
Перегляньте цей проект, щоб дізнатися, як [додати підказки та ресурси](https://github.com/modelcontextprotocol/csharp-sdk/blob/main/samples/EverythingServer/Program.cs).
>>>>>>> origin/main

Також перегляньте це посилання, щоб дізнатися, як викликати [підказки та ресурси](https://github.com/modelcontextprotocol/csharp-sdk/blob/main/src/ModelContextProtocol/Client/).

### Rust

У [попередньому розділі](../../../../03-GettingStarted/01-first-server) ви дізналися, як створити простий сервер MCP за допомогою Rust. Ви можете продовжити працювати над цим або переглянути це посилання для отримання додаткових прикладів серверів MCP на основі Rust: [MCP Server Examples](https://github.com/modelcontextprotocol/rust-sdk/tree/main/examples/servers)

## Рішення

<<<<<<< HEAD
**Папка рішення** містить повні, готові до запуску реалізації клієнтів, які демонструють усі концепції, розглянуті в цьому уроці. Кожне рішення включає як клієнтський, так і серверний код, організований у окремі, самодостатні проекти.
=======
**Папка рішення** містить повні, готові до запуску реалізації клієнтів, які демонструють усі концепції, розглянуті в цьому уроці. Кожне рішення включає як код клієнта, так і сервера, організовані в окремі, автономні проекти.
>>>>>>> origin/main

### 📁 Структура рішення

Каталог рішення організований за мовами програмування:

```text
solution/
├── typescript/          # TypeScript client with npm/Node.js setup
│   ├── package.json     # Dependencies and scripts
│   ├── tsconfig.json    # TypeScript configuration
│   └── src/             # Source code
├── java/                # Java Spring Boot client project
│   ├── pom.xml          # Maven configuration
│   ├── src/             # Java source files
│   └── mvnw             # Maven wrapper
├── python/              # Python client implementation
│   ├── client.py        # Main client code
│   ├── server.py        # Compatible server
│   └── README.md        # Python-specific instructions
├── dotnet/              # .NET client project
│   ├── dotnet.csproj    # Project configuration
│   ├── Program.cs       # Main client code
│   └── dotnet.sln       # Solution file
├── rust/                # Rust client implementation
|  ├── Cargo.lock        # Cargo lock file
|  ├── Cargo.toml        # Project configuration and dependencies
|  ├── src               # Source code
|  │   └── main.rs       # Main client code
└── server/              # Additional .NET server implementation
    ├── Program.cs       # Server code
    └── server.csproj    # Server project file
```

### 🚀 Що включає кожне рішення

Кожне рішення для конкретної мови надає:

- **Повну реалізацію клієнта** з усіма функціями, описаними в уроці.
<<<<<<< HEAD
- **Робочу структуру проекту** з належними залежностями та конфігурацією.
=======
- **Робочу структуру проекту** з правильними залежностями та конфігурацією.
>>>>>>> origin/main
- **Скрипти для збірки та запуску** для легкого налаштування та виконання.
- **Детальний README** з інструкціями для конкретної мови.
- **Приклади обробки помилок** та обробки результатів.

### 📖 Використання рішень

1. **Перейдіть до папки з вашою мовою програмування**:

   ```bash
   cd solution/typescript/    # For TypeScript
   cd solution/java/          # For Java
   cd solution/python/        # For Python
   cd solution/dotnet/        # For .NET
   ```

2. **Дотримуйтесь інструкцій README** у кожній папці для:
   - Встановлення залежностей.
   - Збірки проекту.
   - Запуску клієнта.

3. **Приклад виводу**, який ви повинні побачити:

   ```text
   Prompt: Please review this code: console.log("hello");
   Resource template: file
   Tool result: { content: [ { type: 'text', text: '9' } ] }
   ```

Для повної документації та покрокових інструкцій дивіться: **[📖 Документація рішення](./solution/README.md)**

## 🎯 Повні приклади

<<<<<<< HEAD
Ми надали повні, робочі реалізації клієнтів для всіх мов програмування, розглянутих у цьому уроці. Ці приклади демонструють повну функціональність, описану вище, і можуть бути використані як еталонні реалізації або відправні точки для ваших власних проектів.
=======
Ми надали повні, робочі реалізації клієнтів для всіх мов програмування, розглянутих у цьому уроці. Ці приклади демонструють повний функціонал, описаний вище, і можуть бути використані як еталонні реалізації або стартові точки для ваших власних проектів.
>>>>>>> origin/main

### Доступні повні приклади

| Мова | Файл | Опис |
|------|------|------|
<<<<<<< HEAD
| **Java** | [`client_example_java.java`](../../../../03-GettingStarted/02-client/client_example_java.java) | Повний клієнт Java з використанням транспорту SSE та розширеною обробкою помилок |
| **C#** | [`client_example_csharp.cs`](../../../../03-GettingStarted/02-client/client_example_csharp.cs) | Повний клієнт C# з використанням транспорту stdio та автоматичним запуском сервера |
| **TypeScript** | [`client_example_typescript.ts`](../../../../03-GettingStarted/02-client/client_example_typescript.ts) | Повний клієнт TypeScript із повною підтримкою протоколу MCP |
| **Python** | [`client_example_python.py`](../../../../03-GettingStarted/02-client/client_example_python.py) | Повний клієнт Python із використанням асинхронних шаблонів |
=======
| **Java** | [`client_example_java.java`](../../../../03-GettingStarted/02-client/client_example_java.java) | Повний клієнт Java із використанням транспорту SSE та розширеною обробкою помилок |
| **C#** | [`client_example_csharp.cs`](../../../../03-GettingStarted/02-client/client_example_csharp.cs) | Повний клієнт C# із використанням транспорту stdio та автоматичним запуском сервера |
| **TypeScript** | [`client_example_typescript.ts`](../../../../03-GettingStarted/02-client/client_example_typescript.ts) | Повний клієнт TypeScript із повною підтримкою протоколу MCP |
| **Python** | [`client_example_python.py`](../../../../03-GettingStarted/02-client/client_example_python.py) | Повний клієнт Python із використанням async/await |
>>>>>>> origin/main
| **Rust** | [`client_example_rust.rs`](../../../../03-GettingStarted/02-client/client_example_rust.rs) | Повний клієнт Rust із використанням Tokio для асинхронних операцій |
Кожен повний приклад включає:

- ✅ **Встановлення з'єднання** та обробку помилок
- ✅ **Виявлення сервера** (інструменти, ресурси, підказки, де це доречно)
- ✅ **Операції калькулятора** (додавання, віднімання, множення, ділення, допомога)
- ✅ **Обробку результатів** та форматований вивід
- ✅ **Комплексну обробку помилок**
- ✅ **Чистий, задокументований код** із покроковими коментарями

### Початок роботи з повними прикладами

1. **Оберіть бажану мову** з таблиці вище
2. **Ознайомтеся з файлом повного прикладу**, щоб зрозуміти повну реалізацію
3. **Запустіть приклад**, дотримуючись інструкцій у [`complete_examples.md`](./complete_examples.md)
4. **Модифікуйте та розширюйте** приклад для вашого конкретного випадку використання

Для детальної документації щодо запуску та налаштування цих прикладів дивіться: **[📖 Документація до повних прикладів](./complete_examples.md)**

### 💡 Рішення проти повних прикладів

| **Папка з рішенням** | **Повні приклади** |
|--------------------|--------------------- |
| Повна структура проєкту з файлами збірки | Реалізації в одному файлі |
<<<<<<< HEAD
| Готові до запуску з залежностями | Зосереджені приклади коду |
=======
| Готові до запуску з залежностями | Сфокусовані приклади коду |
>>>>>>> origin/main
| Налаштування, схоже на продакшн | Освітній довідник |
| Інструменти, специфічні для мови | Порівняння між мовами |

Обидва підходи є цінними - використовуйте **папку з рішенням** для повних проєктів і **повні приклади** для навчання та довідки.

## Основні висновки

Основні висновки цього розділу щодо клієнтів:

- Можуть використовуватися як для виявлення, так і для виклику функцій на сервері.
<<<<<<< HEAD
- Можуть запускати сервер одночасно із власним запуском (як у цьому розділі), але клієнти також можуть підключатися до вже працюючих серверів.
=======
- Можуть запускати сервер під час свого запуску (як у цьому розділі), але клієнти також можуть підключатися до вже працюючих серверів.
>>>>>>> origin/main
- Є чудовим способом тестування можливостей сервера поряд з альтернативами, такими як Інспектор, описаний у попередньому розділі.

## Додаткові ресурси

- [Створення клієнтів у MCP](https://modelcontextprotocol.io/quickstart/client)

## Приклади

- [Java Калькулятор](../samples/java/calculator/README.md)
- [.Net Калькулятор](../../../../03-GettingStarted/samples/csharp)
- [JavaScript Калькулятор](../samples/javascript/README.md)
- [TypeScript Калькулятор](../samples/typescript/README.md)
- [Python Калькулятор](../../../../03-GettingStarted/samples/python)
- [Rust Калькулятор](../../../../03-GettingStarted/samples/rust)

## Що далі

- Далі: [Створення клієнта з LLM](../03-llm-client/README.md)

**Відмова від відповідальності**:  
<<<<<<< HEAD
Цей документ був перекладений за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ на його рідній мові слід вважати авторитетним джерелом. Для критичної інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникають внаслідок використання цього перекладу.
=======
Цей документ було перекладено за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, зверніть увагу, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ мовою оригіналу слід вважати авторитетним джерелом. Для критично важливої інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникли внаслідок використання цього перекладу.
>>>>>>> origin/main
