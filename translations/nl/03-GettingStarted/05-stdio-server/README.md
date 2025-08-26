<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e22bdd25c14c3c213fb0ca70973f1000",
  "translation_date": "2025-08-26T19:37:46+00:00",
  "source_file": "03-GettingStarted/05-stdio-server/README.md",
  "language_code": "nl"
}
-->
# MCP Server met stdio Transport

> **⚠️ Belangrijke Update**: Vanaf MCP Specificatie 2025-06-18 is de standalone SSE (Server-Sent Events) transport **verouderd** en vervangen door "Streamable HTTP" transport. De huidige MCP specificatie definieert twee primaire transportmechanismen:
> 1. **stdio** - Standaard input/output (aanbevolen voor lokale servers)
> 2. **Streamable HTTP** - Voor externe servers die intern SSE kunnen gebruiken
>
> Deze les is bijgewerkt om te focussen op de **stdio transport**, wat de aanbevolen aanpak is voor de meeste MCP serverimplementaties.

De stdio transport stelt MCP servers in staat om te communiceren met clients via standaard input- en outputstreams. Dit is het meest gebruikte en aanbevolen transportmechanisme in de huidige MCP specificatie, en biedt een eenvoudige en efficiënte manier om MCP servers te bouwen die gemakkelijk geïntegreerd kunnen worden met verschillende clientapplicaties.

## Overzicht

Deze les behandelt hoe je MCP Servers kunt bouwen en gebruiken met behulp van de stdio transport.

## Leerdoelen

Aan het einde van deze les kun je:

- Een MCP Server bouwen met de stdio transport.
- Een MCP Server debuggen met de Inspector.
- Een MCP Server gebruiken met Visual Studio Code.
- De huidige MCP transportmechanismen begrijpen en waarom stdio wordt aanbevolen.

## stdio Transport - Hoe werkt het?

De stdio transport is een van de twee ondersteunde transporttypes in de huidige MCP specificatie (2025-06-18). Zo werkt het:

- **Eenvoudige communicatie**: De server leest JSON-RPC berichten van standaard input (`stdin`) en stuurt berichten naar standaard output (`stdout`).
- **Proces-gebaseerd**: De client start de MCP server als een subprocess.
- **Berichtformaat**: Berichten zijn individuele JSON-RPC verzoeken, notificaties of antwoorden, gescheiden door nieuwe regels.
- **Logging**: De server MAG UTF-8 strings schrijven naar standaard error (`stderr`) voor logdoeleinden.

### Belangrijke vereisten:
- Berichten MOETEN gescheiden zijn door nieuwe regels en MOGEN GEEN ingesloten nieuwe regels bevatten.
- De server MAG NIETS schrijven naar `stdout` dat geen geldig MCP bericht is.
- De client MAG NIETS schrijven naar de `stdin` van de server dat geen geldig MCP bericht is.

### TypeScript

```typescript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server(
  {
    name: "example-server",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {},
    },
  }
);
```

In de bovenstaande code:

- We importeren de `Server` klasse en `StdioServerTransport` uit de MCP SDK.
- We maken een serverinstantie met basisconfiguratie en mogelijkheden.

### Python

```python
import asyncio
import logging
from mcp.server import Server
from mcp.server.stdio import stdio_server

# Create server instance
server = Server("example-server")

@server.tool()
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b

async def main():
    async with stdio_server(server) as (read_stream, write_stream):
        await server.run(
            read_stream,
            write_stream,
            server.create_initialization_options()
        )

if __name__ == "__main__":
    asyncio.run(main())
```

In de bovenstaande code:

- We maken een serverinstantie met behulp van de MCP SDK.
- We definiëren tools met decorators.
- We gebruiken de stdio_server contextmanager om het transport te beheren.

### .NET

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using ModelContextProtocol.Server;

var builder = Host.CreateApplicationBuilder(args);

builder.Services
    .AddMcpServer()
    .WithStdioTransport()
    .WithTools<Tools>();

builder.Services.AddLogging(logging => logging.AddConsole());

var app = builder.Build();
await app.RunAsync();
```

Het belangrijkste verschil met SSE is dat stdio servers:

- Geen webserver setup of HTTP endpoints vereisen.
- Als subprocessen door de client worden gestart.
- Communiceren via stdin/stdout streams.
- Eenvoudiger te implementeren en te debuggen zijn.

## Oefening: Een stdio Server maken

Om onze server te maken, moeten we twee dingen in gedachten houden:

- We moeten een webserver gebruiken om endpoints voor verbinding en berichten bloot te stellen.

## Lab: Een eenvoudige MCP stdio server maken

In dit lab maken we een eenvoudige MCP server met de aanbevolen stdio transport. Deze server zal tools blootstellen die clients kunnen aanroepen met behulp van het standaard Model Context Protocol.

### Vereisten

- Python 3.8 of later
- MCP Python SDK: `pip install mcp`
- Basiskennis van asynchrone programmering

Laten we beginnen met het maken van onze eerste MCP stdio server:

```python
import asyncio
import logging
from mcp.server import Server
from mcp.server.stdio import stdio_server
from mcp import types

# Configure logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

# Create the server
server = Server("example-stdio-server")

@server.tool()
def calculate_sum(a: int, b: int) -> int:
    """Calculate the sum of two numbers"""
    return a + b

@server.tool() 
def get_greeting(name: str) -> str:
    """Generate a personalized greeting"""
    return f"Hello, {name}! Welcome to MCP stdio server."

async def main():
    # Use stdio transport
    async with stdio_server(server) as (read_stream, write_stream):
        await server.run(
            read_stream,
            write_stream,
            server.create_initialization_options()
        )

if __name__ == "__main__":
    asyncio.run(main())
```

## Belangrijke verschillen met de verouderde SSE aanpak

**Stdio Transport (Huidige Standaard):**
- Eenvoudig subprocessmodel - client start server als child process.
- Communicatie via stdin/stdout met JSON-RPC berichten.
- Geen HTTP server setup vereist.
- Betere prestaties en beveiliging.
- Eenvoudiger debuggen en ontwikkelen.

**SSE Transport (Verouderd vanaf MCP 2025-06-18):**
- Vereiste HTTP server met SSE endpoints.
- Complexere setup met webserver infrastructuur.
- Extra beveiligingsoverwegingen voor HTTP endpoints.
- Nu vervangen door Streamable HTTP voor web-gebaseerde scenario's.

### Een server maken met stdio transport

Om onze stdio server te maken, moeten we:

1. **De benodigde bibliotheken importeren** - We hebben de MCP servercomponenten en stdio transport nodig.
2. **Een serverinstantie maken** - Definieer de server met zijn mogelijkheden.
3. **Tools definiëren** - Voeg de functionaliteit toe die we willen blootstellen.
4. **Het transport instellen** - Configureer stdio communicatie.
5. **De server starten** - Start de server en verwerk berichten.

Laten we dit stap voor stap bouwen:

### Stap 1: Een basis stdio server maken

```python
import asyncio
import logging
from mcp.server import Server
from mcp.server.stdio import stdio_server

# Configure logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

# Create the server
server = Server("example-stdio-server")

@server.tool()
def get_greeting(name: str) -> str:
    """Generate a personalized greeting"""
    return f"Hello, {name}! Welcome to MCP stdio server."

async def main():
    async with stdio_server(server) as (read_stream, write_stream):
        await server.run(
            read_stream,
            write_stream,
            server.create_initialization_options()
        )

if __name__ == "__main__":
    asyncio.run(main())
```

### Stap 2: Meer tools toevoegen

```python
@server.tool()
def calculate_sum(a: int, b: int) -> int:
    """Calculate the sum of two numbers"""
    return a + b

@server.tool()
def calculate_product(a: int, b: int) -> int:
    """Calculate the product of two numbers"""
    return a * b

@server.tool()
def get_server_info() -> dict:
    """Get information about this MCP server"""
    return {
        "server_name": "example-stdio-server",
        "version": "1.0.0",
        "transport": "stdio",
        "capabilities": ["tools"]
    }
```

### Stap 3: De server starten

Sla de code op als `server.py` en voer het uit vanaf de commandoregel:

```bash
python server.py
```

De server zal starten en wachten op input van stdin. Het communiceert via JSON-RPC berichten over de stdio transport.

### Stap 4: Testen met de Inspector

Je kunt je server testen met de MCP Inspector:

1. Installeer de Inspector: `npx @modelcontextprotocol/inspector`
2. Start de Inspector en wijs deze naar je server.
3. Test de tools die je hebt gemaakt.

### .NET

```csharp
var builder = WebApplication.CreateBuilder(args);
builder.Services
    .AddMcpServer();

## Debugging your stdio server

### Using the MCP Inspector

The MCP Inspector is a valuable tool for debugging and testing MCP servers. Here's how to use it with your stdio server:

1. **Install the Inspector**:
   ```bash
   npx @modelcontextprotocol/inspector
   ```

2. **Run the Inspector**:
   ```bash
   npx @modelcontextprotocol/inspector python server.py
   ```

3. **Test your server**: The Inspector provides a web interface where you can:
   - View server capabilities
   - Test tools with different parameters
   - Monitor JSON-RPC messages
   - Debug connection issues

### Using VS Code

You can also debug your MCP server directly in VS Code:

1. Create a launch configuration in `.vscode/launch.json`:
   ```json
   {
     "version": "0.2.0",
     "configurations": [
       {
         "name": "Debug MCP Server",
         "type": "python",
         "request": "launch",
         "program": "server.py",
         "console": "integratedTerminal"
       }
     ]
   }
   ```

2. Set breakpoints in your server code
3. Run the debugger and test with the Inspector

### Common debugging tips

- Use `stderr` for logging - never write to `stdout` as it's reserved for MCP messages
- Ensure all JSON-RPC messages are newline-delimited
- Test with simple tools first before adding complex functionality
- Use the Inspector to verify message formats

## Consuming your stdio server in VS Code

Once you've built your MCP stdio server, you can integrate it with VS Code to use it with Claude or other MCP-compatible clients.

### Configuration

1. **Create an MCP configuration file** at `%APPDATA%\Claude\claude_desktop_config.json` (Windows) or `~/Library/Application Support/Claude/claude_desktop_config.json` (Mac):

   ```json
   {
     "mcpServers": {
       "example-stdio-server": {
         "command": "python",
         "args": ["path/to/your/server.py"]
       }
     }
   }
   ```

2. **Restart Claude**: Close and reopen Claude to load the new server configuration.

3. **Test the connection**: Start a conversation with Claude and try using your server's tools:
   - "Can you greet me using the greeting tool?"
   - "Calculate the sum of 15 and 27"
   - "What's the server info?"

### TypeScript stdio server example

Here's a complete TypeScript example for reference:

```typescript
#!/usr/bin/env node
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { CallToolRequestSchema, ListToolsRequestSchema } from "@modelcontextprotocol/sdk/types.js";

const server = new Server(
  {
    name: "example-stdio-server",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {},
    },
  }
);

// Tools toevoegen
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return {
    tools: [
      {
        name: "get_greeting",
        description: "Ontvang een persoonlijke begroeting",
        inputSchema: {
          type: "object",
          properties: {
            name: {
              type: "string",
              description: "Naam van de persoon om te begroeten",
            },
          },
          required: ["name"],
        },
      },
    ],
  };
});

server.setRequestHandler(CallToolRequestSchema, async (request) => {
  if (request.params.name === "get_greeting") {
    return {
      content: [
        {
          type: "text",
          text: `Hallo, ${request.params.arguments?.name}! Welkom bij MCP stdio server.`,
        },
      ],
    };
  } else {
    throw new Error(`Onbekende tool: ${request.params.name}`);
  }
});

async function runServer() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
}

runServer().catch(console.error);
```

### .NET stdio server example

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using ModelContextProtocol.Server;
using System.ComponentModel;

var builder = Host.CreateApplicationBuilder(args);

builder.Services
    .AddMcpServer()
    .WithStdioTransport()
    .WithTools<Tools>();

var app = builder.Build();
await app.RunAsync();

public class Tools
{
    [Description("Ontvang een persoonlijke begroeting")]
    public string GetGreeting(string name)
    {
        return $"Hallo, {name}! Welkom bij MCP stdio server.";
    }

    [Description("Bereken de som van twee getallen")]
    public int CalculateSum(int a, int b)
    {
        return a + b;
    }
}
```

## Summary

In this updated lesson, you learned how to:

- Build MCP servers using the current **stdio transport** (recommended approach)
- Understand why SSE transport was deprecated in favor of stdio and Streamable HTTP
- Create tools that can be called by MCP clients
- Debug your server using the MCP Inspector
- Integrate your stdio server with VS Code and Claude

The stdio transport provides a simpler, more secure, and more performant way to build MCP servers compared to the deprecated SSE approach. It's the recommended transport for most MCP server implementations as of the 2025-06-18 specification.
```

### .NET

1. Laten we eerst enkele tools maken. Hiervoor maken we een bestand *Tools.cs* met de volgende inhoud:

  ```csharp
  using System.ComponentModel;
  using System.Text.Json;
  using ModelContextProtocol.Server;

## Exercise: Testing your stdio server

Now that you've built your stdio server, let's test it to make sure it works correctly.

### Prerequisites

1. Ensure you have the MCP Inspector installed:
   ```bash
   npm install -g @modelcontextprotocol/inspector
   ```

2. Your server code should be saved (e.g., as `server.py`)

### Testing with the Inspector

1. **Start the Inspector with your server**:
   ```bash
   npx @modelcontextprotocol/inspector python server.py
   ```

2. **Open de webinterface**: De Inspector opent een browservenster waarin de mogelijkheden van je server worden weergegeven.

3. **Test de tools**: 
   - Probeer de `get_greeting` tool met verschillende namen.
   - Test de `calculate_sum` tool met verschillende getallen.
   - Roep de `get_server_info` tool aan om servermetadata te bekijken.

4. **Monitor de communicatie**: De Inspector toont de JSON-RPC berichten die worden uitgewisseld tussen client en server.

### Wat je zou moeten zien

Wanneer je server correct start, zou je het volgende moeten zien:
- Servermogelijkheden weergegeven in de Inspector.
- Tools beschikbaar voor testen.
- Succesvolle JSON-RPC berichtuitwisselingen.
- Toolreacties weergegeven in de interface.

### Veelvoorkomende problemen en oplossingen

**Server start niet:**
- Controleer of alle afhankelijkheden zijn geïnstalleerd: `pip install mcp`.
- Verifieer Python-syntaxis en inspringing.
- Zoek naar foutmeldingen in de console.

**Tools verschijnen niet:**
- Zorg ervoor dat `@server.tool()` decorators aanwezig zijn.
- Controleer of toolfuncties zijn gedefinieerd vóór `main()`.
- Verifieer dat de server correct is geconfigureerd.

**Verbindingsproblemen:**
- Zorg ervoor dat de server stdio transport correct gebruikt.
- Controleer of er geen andere processen interfereren.
- Verifieer de Inspector commandosyntaxis.

## Opdracht

Probeer je server uit te breiden met meer mogelijkheden. Bekijk [deze pagina](https://api.chucknorris.io/) om bijvoorbeeld een tool toe te voegen die een API aanroept. Jij bepaalt hoe de server eruit moet zien. Veel plezier :)

## Oplossing

[Oplossing](./solution/README.md) Hier is een mogelijke oplossing met werkende code.

## Belangrijke inzichten

De belangrijkste inzichten uit dit hoofdstuk zijn:

- De stdio transport is het aanbevolen mechanisme voor lokale MCP servers.
- Stdio transport maakt naadloze communicatie mogelijk tussen MCP servers en clients via standaard input- en outputstreams.
- Je kunt zowel Inspector als Visual Studio Code gebruiken om stdio servers direct te gebruiken, wat debuggen en integratie eenvoudig maakt.

## Voorbeelden 

- [Java Calculator](../samples/java/calculator/README.md)
- [.Net Calculator](../../../../03-GettingStarted/samples/csharp)
- [JavaScript Calculator](../samples/javascript/README.md)
- [TypeScript Calculator](../samples/typescript/README.md)
- [Python Calculator](../../../../03-GettingStarted/samples/python) 

## Aanvullende bronnen

- [SSE](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events)

## Wat komt hierna?

## Volgende stappen

Nu je hebt geleerd hoe je MCP servers kunt bouwen met de stdio transport, kun je meer geavanceerde onderwerpen verkennen:

- **Volgende**: [HTTP Streaming met MCP (Streamable HTTP)](../06-http-streaming/README.md) - Leer over het andere ondersteunde transportmechanisme voor externe servers.
- **Geavanceerd**: [MCP Beveiligingsbest Practices](../../02-Security/README.md) - Implementeer beveiliging in je MCP servers.
- **Productie**: [Implementatiestrategieën](../09-deployment/README.md) - Implementeer je servers voor productiegebruik.

## Aanvullende bronnen

- [MCP Specificatie 2025-06-18](https://spec.modelcontextprotocol.io/specification/) - Officiële specificatie.
- [MCP SDK Documentatie](https://github.com/modelcontextprotocol/sdk) - SDK-referenties voor alle talen.
- [Community Voorbeelden](../../06-CommunityContributions/README.md) - Meer servervoorbeelden van de community.

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in zijn oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor cruciale informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor eventuele misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.