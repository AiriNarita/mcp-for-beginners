<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "41f16dac486d2086a53bc644a01cbe42",
  "translation_date": "2025-08-18T16:49:34+00:00",
  "source_file": "07-LessonsfromEarlyAdoption/README.md",
  "language_code": "sr"
}
-->
# 🌟 Лекције од раних усвојилаца

[![Лекције од MCP раних усвојилаца](../../../translated_images/08.980bb2babbaadd8a97739effc9b31e5f1abd8f4c4a3fbc90fb9f931a866674d0.sr.png)](https://youtu.be/jds7dSmNptE)

_(Кликните на слику изнад да бисте погледали видео ове лекције)_

## 🎯 Шта покрива овај модул

Овај модул истражује како стварне организације и програмери користе Model Context Protocol (MCP) за решавање стварних изазова и подстицање иновација. Кроз детаљне студије случаја и практичне примере, открићете како MCP омогућава сигурну и скалабилну интеграцију AI-а која повезује језичке моделе, алате и корпоративне податке.

### 📚 Погледајте MCP у акцији

Желите да видите како се ови принципи примењују на алате спремне за производњу? Погледајте наш [**10 Microsoft MCP сервера који трансформишу продуктивност програмера**](microsoft-mcp-servers.md), који приказује стварне Microsoft MCP сервере које можете користити већ данас.

## Преглед

Ова лекција истражује како су рани усвојиоци искористили Model Context Protocol (MCP) за решавање стварних изазова и подстицање иновација у различитим индустријама. Кроз детаљне студије случаја и практичне пројекте, видећете како MCP омогућава стандардизовану, сигурну и скалабилну AI интеграцију—повезујући велике језичке моделе, алате и корпоративне податке у јединственом оквиру. Стећи ћете практично искуство у дизајнирању и изградњи решења заснованих на MCP-у, учити из доказаних образаца имплементације и открити најбоље праксе за примену MCP-а у производним окружењима. Лекција такође истиче нове трендове, будуће правце и ресурсе отвореног кода како бисте остали на челу MCP технологије и њеног развојног екосистема.

## Циљеви учења

- Анализирајте стварне имплементације MCP-а у различитим индустријама
- Дизајнирајте и изградите комплетне апликације засноване на MCP-у
- Истражите нове трендове и будуће правце у MCP технологији
- Примените најбоље праксе у стварним сценаријима развоја

## Стварне имплементације MCP-а

### Студија случаја 1: Аутоматизација корисничке подршке у предузећима

Мултинационална корпорација је имплементирала решење засновано на MCP-у за стандардизацију AI интеракција у својим системима корисничке подршке. Ово им је омогућило:

- Креирање јединственог интерфејса за више LLM провајдера
- Одржавање конзистентног управљања упитима у различитим одељењима
- Имплементацију робусних безбедносних и контролних механизама
- Лако пребацивање између различитих AI модела на основу специфичних потреба

**Техничка имплементација:**

```python
# Python MCP server implementation for customer support
import logging
import asyncio
from modelcontextprotocol import create_server, ServerConfig
from modelcontextprotocol.server import MCPServer
from modelcontextprotocol.transports import create_http_transport
from modelcontextprotocol.resources import ResourceDefinition
from modelcontextprotocol.prompts import PromptDefinition
from modelcontextprotocol.tool import ToolDefinition

# Configure logging
logging.basicConfig(level=logging.INFO)

async def main():
    # Create server configuration
    config = ServerConfig(
        name="Enterprise Customer Support Server",
        version="1.0.0",
        description="MCP server for handling customer support inquiries"
    )
    
    # Initialize MCP server
    server = create_server(config)
    
    # Register knowledge base resources
    server.resources.register(
        ResourceDefinition(
            name="customer_kb",
            description="Customer knowledge base documentation"
        ),
        lambda params: get_customer_documentation(params)
    )
    
    # Register prompt templates
    server.prompts.register(
        PromptDefinition(
            name="support_template",
            description="Templates for customer support responses"
        ),
        lambda params: get_support_templates(params)
    )
    
    # Register support tools
    server.tools.register(
        ToolDefinition(
            name="ticketing",
            description="Create and update support tickets"
        ),
        handle_ticketing_operations
    )
    
    # Start server with HTTP transport
    transport = create_http_transport(port=8080)
    await server.run(transport)

if __name__ == "__main__":
    asyncio.run(main())
```

**Резултати:** 30% смањење трошкова модела, 45% побољшање конзистентности одговора и побољшана усклађеност у глобалним операцијама.

### Студија случаја 2: Помоћник за дијагностику у здравству

Пружаоци здравствених услуга развили су MCP инфраструктуру за интеграцију више специјализованих медицинских AI модела уз осигурање заштите осетљивих података пацијената:

- Беспрекорно пребацивање између општих и специјализованих медицинских модела
- Строге контроле приватности и ревизорски трагови
- Интеграција са постојећим системима електронских здравствених картона (EHR)
- Конзистентно управљање упитима за медицинску терминологију

**Техничка имплементација:**

```csharp
// C# MCP host application implementation in healthcare application
using Microsoft.Extensions.DependencyInjection;
using ModelContextProtocol.SDK.Client;
using ModelContextProtocol.SDK.Security;
using ModelContextProtocol.SDK.Resources;

public class DiagnosticAssistant
{
    private readonly MCPHostClient _mcpClient;
    private readonly PatientContext _patientContext;
    
    public DiagnosticAssistant(PatientContext patientContext)
    {
        _patientContext = patientContext;
        
        // Configure MCP client with healthcare-specific settings
        var clientOptions = new ClientOptions
        {
            Name = "Healthcare Diagnostic Assistant",
            Version = "1.0.0",
            Security = new SecurityOptions
            {
                Encryption = EncryptionLevel.Medical,
                AuditEnabled = true
            }
        };
        
        _mcpClient = new MCPHostClientBuilder()
            .WithOptions(clientOptions)
            .WithTransport(new HttpTransport("https://healthcare-mcp.example.org"))
            .WithAuthentication(new HIPAACompliantAuthProvider())
            .Build();
    }
    
    public async Task<DiagnosticSuggestion> GetDiagnosticAssistance(
        string symptoms, string patientHistory)
    {
        // Create request with appropriate resources and tool access
        var resourceRequest = new ResourceRequest
        {
            Name = "patient_records",
            Parameters = new Dictionary<string, object>
            {
                ["patientId"] = _patientContext.PatientId,
                ["requestingProvider"] = _patientContext.ProviderId
            }
        };
        
        // Request diagnostic assistance using appropriate prompt
        var response = await _mcpClient.SendPromptRequestAsync(
            promptName: "diagnostic_assistance",
            parameters: new Dictionary<string, object>
            {
                ["symptoms"] = symptoms,
                patientHistory = patientHistory,
                relevantGuidelines = _patientContext.GetRelevantGuidelines()
            });
            
        return DiagnosticSuggestion.FromMCPResponse(response);
    }
}
```

**Резултати:** Побољшане дијагностичке препоруке за лекаре уз потпуну усклађеност са HIPAA и значајно смањење пребацивања контекста између система.

### Студија случаја 3: Анализа ризика у финансијским услугама

Финансијска институција је имплементирала MCP за стандардизацију процеса анализе ризика у различитим одељењима:

- Креиран јединствени интерфејс за моделе кредитног ризика, откривања превара и инвестиционог ризика
- Имплементиране строге контроле приступа и верзионисање модела
- Осигурана ревизорска способност свих AI препорука
- Одржано конзистентно форматирање података у различитим системима

**Техничка имплементација:**

```java
// Java MCP server for financial risk assessment
import org.mcp.server.*;
import org.mcp.security.*;

public class FinancialRiskMCPServer {
    public static void main(String[] args) {
        // Create MCP server with financial compliance features
        MCPServer server = new MCPServerBuilder()
            .withModelProviders(
                new ModelProvider("risk-assessment-primary", new AzureOpenAIProvider()),
                new ModelProvider("risk-assessment-audit", new LocalLlamaProvider())
            )
            .withPromptTemplateDirectory("./compliance/templates")
            .withAccessControls(new SOCCompliantAccessControl())
            .withDataEncryption(EncryptionStandard.FINANCIAL_GRADE)
            .withVersionControl(true)
            .withAuditLogging(new DatabaseAuditLogger())
            .build();
            
        server.addRequestValidator(new FinancialDataValidator());
        server.addResponseFilter(new PII_RedactionFilter());
        
        server.start(9000);
        
        System.out.println("Financial Risk MCP Server running on port 9000");
    }
}
```

**Резултати:** Побољшана регулаторна усклађеност, 40% бржи циклуси имплементације модела и побољшана конзистентност процене ризика у одељењима.

### Студија случаја 4: Microsoft Playwright MCP сервер за аутоматизацију прегледача

Microsoft је развио [Playwright MCP сервер](https://github.com/microsoft/playwright-mcp) за омогућавање сигурне, стандардизоване аутоматизације прегледача кроз Model Context Protocol. Овај сервер спреман за производњу омогућава AI агентима и LLM-овима интеракцију са веб прегледачима на контролисан, ревизорски и проширив начин—омогућавајући случајеве употребе као што су аутоматизовано тестирање веба, екстракција података и радни токови од краја до краја.

> **🎯 Алат спреман за производњу**
> 
> Ова студија случаја приказује стварни MCP сервер који можете користити већ данас! Сазнајте више о Playwright MCP серверу и још 9 других Microsoft MCP сервера спремних за производњу у нашем [**Microsoft MCP Servers Guide**](microsoft-mcp-servers.md#8--playwright-mcp-server).

**Кључне карактеристике:**
- Омогућава способности аутоматизације прегледача (навигација, попуњавање формулара, снимање екрана итд.) као MCP алате
- Имплементира строге контроле приступа и изолацију ради спречавања неовлашћених радњи
- Пружа детаљне ревизорске записе за све интеракције са прегледачем
- Подржава интеграцију са Azure OpenAI и другим LLM провајдерима за аутоматизацију вођену агентима
- Покреће могућности веб прегледања GitHub Copilot-а

**Техничка имплементација:**

```typescript
// TypeScript: Registering Playwright browser automation tools in an MCP server
import { createServer, ToolDefinition } from 'modelcontextprotocol';
import { launch } from 'playwright';

const server = createServer({
  name: 'Playwright MCP Server',
  version: '1.0.0',
  description: 'MCP server for browser automation using Playwright'
});

// Register a tool for navigating to a URL and capturing a screenshot
server.tools.register(
  new ToolDefinition({
    name: 'navigate_and_screenshot',
    description: 'Navigate to a URL and capture a screenshot',
    parameters: {
      url: { type: 'string', description: 'The URL to visit' }
    }
  }),
  async ({ url }) => {
    const browser = await launch();
    const page = await browser.newPage();
    await page.goto(url);
    const screenshot = await page.screenshot();
    await browser.close();
    return { screenshot };
  }
);

// Start the MCP server
server.listen(8080);
```

**Резултати:**

- Омогућена сигурна, програмска аутоматизација прегледача за AI агенте и LLM-ове
- Смањен ручни напор тестирања и побољшана покривеност тестова за веб апликације
- Пружен поново употребљив, проширив оквир за интеграцију алата заснованих на прегледачу у корпоративним окружењима
- Покреће могућности веб прегледања GitHub Copilot-а

**Референце:**

- [Playwright MCP Server GitHub Repository](https://github.com/microsoft/playwright-mcp)
- [Microsoft AI and Automation Solutions](https://azure.microsoft.com/en-us/products/ai-services/)

### Студија случаја 5: Azure MCP – Model Context Protocol као услуга на нивоу предузећа

Azure MCP сервер ([https://aka.ms/azmcp](https://aka.ms/azmcp)) је Microsoft-ова управљана имплементација Model Context Protocol-а на нивоу предузећа, дизајнирана да пружи скалабилне, сигурне и усклађене MCP серверске могућности као услугу у облаку. Azure MCP омогућава организацијама да брзо имплементирају, управљају и интегришу MCP сервере са Azure AI, подацима и безбедносним услугама, смањујући оперативни терет и убрзавајући усвајање AI-а.

> **🎯 Алат спреман за производњу**
> 
> Ово је стварни MCP сервер који можете користити већ данас! Сазнајте више о Azure AI Foundry MCP серверу у нашем [**Microsoft MCP Servers Guide**](microsoft-mcp-servers.md).

- Потпуно управљено MCP серверско хостовање са уграђеним скалирањем, мониторингом и безбедношћу
- Нативна интеграција са Azure OpenAI, Azure AI Search и другим Azure услугама
- Аутентификација и ауторизација на нивоу предузећа преко Microsoft Entra ID
- Подршка за прилагођене алате, шаблоне упита и конекторе ресурса
- Усклађеност са безбедносним и регулаторним захтевима предузећа

**Техничка имплементација:**

```yaml
# Example: Azure MCP server deployment configuration (YAML)
apiVersion: mcp.microsoft.com/v1
kind: McpServer
metadata:
  name: enterprise-mcp-server
spec:
  modelProviders:
    - name: azure-openai
      type: AzureOpenAI
      endpoint: https://<your-openai-resource>.openai.azure.com/
      apiKeySecret: <your-azure-keyvault-secret>
  tools:
    - name: document_search
      type: AzureAISearch
      endpoint: https://<your-search-resource>.search.windows.net/
      apiKeySecret: <your-azure-keyvault-secret>
  authentication:
    type: EntraID
    tenantId: <your-tenant-id>
  monitoring:
    enabled: true
    logAnalyticsWorkspace: <your-log-analytics-id>
```

**Резултати:**  
- Смањено време до вредности за AI пројекте предузећа пружањем платформе MCP сервера спремне за употребу и усклађене са прописима
- Поједностављена интеграција LLM-ова, алата и извора корпоративних података
- Побољшана безбедност, видљивост и оперативна ефикасност за MCP радне оптерећења
- Побољшан квалитет кода уз најбоље праксе Azure SDK-а и тренутне обрасце аутентификације

**Референце:**  
- [Azure MCP Documentation](https://aka.ms/azmcp)
- [Azure MCP Server GitHub Repository](https://github.com/Azure/azure-mcp)
- [Azure AI Services](https://azure.microsoft.com/en-us/products/ai-services/)
- [Microsoft MCP Center](https://mcp.azure.com)

### Студија случаја 6: NLWeb

MCP (Model Context Protocol) је нови протокол за Chatbot-ове и AI асистенте за интеракцију са алатима. Сваки NLWeb инстанца је такође MCP сервер, који подржава један основни метод, ask, који се користи за постављање питања веб-сајту на природном језику. Одговор користи schema.org, широко коришћену вокабулар за описивање веб података. Укратко, MCP је NLWeb као што је Http за HTML. NLWeb комбинује протоколе, формате Schema.org и узорке кода како би помогао сајтовима да брзо креирају ове крајње тачке, користећи предности како за људе кроз конверзационе интерфејсе, тако и за машине кроз природну интеракцију агента са агентом.

Постоје два различита компонента NLWeb-а:
- Протокол, веома једноставан за почетак, за интерфејс са сајтом на природном језику и формат, користећи json и schema.org за враћени одговор. Погледајте документацију о REST API-ју за више детаља.
- Једноставна имплементација (1) која користи постојеће ознаке, за сајтове који се могу апстраховати као листе ставки (производи, рецепти, атракције, рецензије итд.). Заједно са сетом виџета корисничког интерфејса, сајтови могу лако пружити конверзационе интерфејсе за свој садржај. Погледајте документацију о животном циклусу упита за ћаскање за више детаља о томе како ово функционише.

**Референце:**  
- [Azure MCP Documentation](https://aka.ms/azmcp)  
- [NLWeb](https://github.com/microsoft/NlWeb)

### Студија случаја 7: Azure AI Foundry MCP сервер – Интеграција AI агената у предузећима

Azure AI Foundry MCP сервери показују како MCP може бити коришћен за оркестрацију и управљање AI агентима и радним токовима у корпоративним окружењима. Интеграцијом MCP-а са Azure AI Foundry-јем, организације могу стандардизовати интеракције агената, искористити управљање радним токовима Foundry-ја и осигурати сигурне, скалабилне имплементације.

> **🎯 Алат спреман за производњу**
> 
> Ово је стварни MCP сервер који можете користити већ данас! Сазнајте више о Azure AI Foundry MCP серверу у нашем [**Microsoft MCP Servers Guide**](microsoft-mcp-servers.md#9--azure-ai-foundry-mcp-server).

**Кључне карактеристике:**
- Комплетан приступ Azure AI екосистему, укључујући каталоге модела и управљање имплементацијом
- Индексирање знања са Azure AI Search за RAG апликације
- Алатке за евалуацију перформанси AI модела и осигурање квалитета
- Интеграција са Azure AI Foundry Catalog и Labs за најновије истраживачке моделе
- Управљање агентима и могућности евалуације за производне сценарије

**Резултати:**
- Брзо прототипирање и робусно праћење радних токова AI агената
- Беспрекорна интеграција са Azure AI услугама за напредне сценарије
- Јединствени интерфејс за изградњу, имплементацију и праћење агентских цевовода
- Побољшана безбедност, усклађеност и оперативна ефикасност за предузећа
- Убрзано усвајање AI-а уз задржавање контроле над сложеним процесима вођеним агентима

**Референце:**
- [Azure AI Foundry MCP Server GitHub Repository](https://github.com/azure-ai-foundry/mcp-foundry)
- [Интеграција Azure AI агената са MCP-ом (Microsoft Foundry Blog)](https://devblogs.microsoft.com/foundry/integrating-azure-ai-agents-mcp/)

### Студија случаја 8: Foundry MCP Playground – Експериментисање и прототипирање

Foundry MCP Playground нуди окружење спремно за употребу за експериментисање са MCP серверима и интеграцијама Azure AI Foundry-ја. Програмери могу брзо прототипирати, тестирати и евалуирати AI моделе и радне токове агената користећи ресурсе из Azure AI Foundry Catalog и Labs. Playground поједностављује поставку, пружа узорке пројеката и подржава колаборативни развој, чинећи лакшим истраживање најбољих пракси и нових сценарија уз минималан напор. Посебно је користан за тимове који желе да валидирају идеје, деле експерименте и убрзају учење без потребе за сложеном инфраструктуром. Смањујући баријеру за улазак, Playground помаже у подстицању иновација и доприноса заједнице у MCP и Azure AI Foundry екосистему.

**Референце:**

- [Foundry MCP Playground GitHub Repository](https://github.com/azure-ai-foundry/foundry-mcp-playground)

### Студија случаја 9: Microsoft Learn Docs MCP сервер – Приступ документацији вођен AI-ом

Microsoft Learn Docs MCP сервер је услуга хостована у облаку која омогућава AI асистентима приступ у реалном времену званичној Microsoft документацији кроз Model Context Protocol. Овај сервер спреман за производњу повезује се са свеобухватним Microsoft Learn екосистемом и омогућава семантичко претраживање свих званичних Microsoft извора.
> **🎯 Алат спреман за продукцију**  
>  
> Ово је прави MCP сервер који можете користити већ данас! Сазнајте више о Microsoft Learn Docs MCP серверу у нашем [**Водичу за Microsoft MCP сервере**](microsoft-mcp-servers.md#1--microsoft-learn-docs-mcp-server).
**Кључне карактеристике:**
- Приступ у реалном времену званичној Microsoft документацији, Azure документацији и Microsoft 365 документацији  
- Напредне могућности семантичког претраживања које разумеју контекст и намеру  
- Увек ажуриране информације како се садржај на Microsoft Learn објављује  
- Свеобухватна покривеност кроз Microsoft Learn, Azure документацију и Microsoft 365 изворе  
- Враћа до 10 висококвалитетних делова садржаја са насловима чланака и URL адресама  

**Зашто је ово важно:**
- Решава проблем „застарелог знања AI“ за Microsoft технологије  
- Обезбеђује да AI асистенти имају приступ најновијим .NET, C#, Azure и Microsoft 365 функцијама  
- Пружа ауторитативне, првокласне информације за тачно генерисање кода  
- Кључно за програмере који раде са брзо еволуирајућим Microsoft технологијама  

**Резултати:**
- Драматично побољшана тачност AI-генерисаног кода за Microsoft технологије  
- Смањено време проведено у тражењу актуелне документације и најбољих пракси  
- Повећана продуктивност програмера уз документацију свесну контекста  
- Беспрекорна интеграција са развојним токовима рада без напуштања IDE-а  

**Референце:**
- [Microsoft Learn Docs MCP Server GitHub Repository](https://github.com/MicrosoftDocs/mcp)  
- [Microsoft Learn Documentation](https://learn.microsoft.com/)  

## Практични пројекти  

### Пројекат 1: Изградња MCP сервера са више провајдера  

**Циљ:** Направити MCP сервер који може усмеравати захтеве ка више провајдера AI модела на основу специфичних критеријума.  

**Захтеви:**  
- Подршка за најмање три различита провајдера модела (нпр. OpenAI, Anthropic, локални модели)  
- Имплементација механизма за рутирање на основу метаподатака захтева  
- Креирање система конфигурације за управљање акредитивима провајдера  
- Додавање кеширања ради оптимизације перформанси и трошкова  
- Изградња једноставне контролне табле за праћење коришћења  

**Кораци имплементације:**  
1. Постављање основне инфраструктуре MCP сервера  
2. Имплементација адаптера провајдера за сваку AI услугу модела  
3. Креирање логике рутирања на основу атрибута захтева  
4. Додавање механизама за кеширање за честе захтеве  
5. Развој контролне табле за праћење  
6. Тестирање са различитим обрасцима захтева  

**Технологије:** Изаберите Python (.NET/Java/Python у зависности од ваших преференција), Redis за кеширање и једноставан веб оквир за контролну таблу.  

### Пројекат 2: Систем за управљање предлошцима у предузећу  

**Циљ:** Развити систем заснован на MCP-у за управљање, верзионисање и примену предлошка упита унутар организације.  

**Захтеви:**  
- Креирање централизованог репозиторијума за предлошке упита  
- Имплементација система за верзионисање и одобравање  
- Развој могућности тестирања предлошка са узорцима уноса  
- Увођење контроле приступа засноване на улогама  
- Креирање API-ја за преузимање и примену предлошка  

**Кораци имплементације:**  
1. Дизајн шеме базе података за складиштење предлошка  
2. Креирање основног API-ја за CRUD операције над предлошцима  
3. Имплементација система за верзионисање  
4. Развој процеса одобравања  
5. Изградња оквира за тестирање  
6. Креирање једноставног веб интерфејса за управљање  
7. Интеграција са MCP сервером  

**Технологије:** Ваш избор оквира за backend, SQL или NoSQL базе података и frontend оквира за интерфејс за управљање.  

### Пројекат 3: Платформа за генерисање садржаја заснована на MCP-у  

**Циљ:** Направити платформу за генерисање садржаја која користи MCP за обезбеђивање доследних резултата за различите типове садржаја.  

**Захтеви:**  
- Подршка за више формата садржаја (блогови, друштвене мреже, маркетиншки текстови)  
- Имплементација генерисања заснованог на предлошцима са опцијама прилагођавања  
- Креирање система за преглед и повратне информације о садржају  
- Праћење метрика перформанси садржаја  
- Подршка за верзионисање и итерацију садржаја  

**Кораци имплементације:**  
1. Постављање инфраструктуре MCP клијента  
2. Креирање предлошка за различите типове садржаја  
3. Изградња цевовода за генерисање садржаја  
4. Имплементација система за преглед  
5. Развој система за праћење метрика  
6. Креирање корисничког интерфејса за управљање предлошцима и генерисање садржаја  

**Технологије:** Ваш омиљени програмски језик, веб оквир и систем базе података.  

## Будући правци за MCP технологију  

### Нови трендови  

1. **Мултимодални MCP**  
   - Проширење MCP-а за стандардизацију интеракција са моделима за слике, звук и видео  
   - Развој могућности закључивања између различитих модалитета  
   - Стандардизовани формати упита за различите модалитете  

2. **Федеративна MCP инфраструктура**  
   - Дистрибуиране MCP мреже које могу делити ресурсе између организација  
   - Стандардизовани протоколи за безбедно дељење модела  
   - Технике приватног рачунања  

3. **MCP тржишта**  
   - Екосистеми за дељење и монетизацију MCP предлошка и додатака  
   - Процеси осигурања квалитета и сертификације  
   - Интеграција са тржиштима модела  

4. **MCP за рачунарство на ивици**  
   - Адаптација MCP стандарда за уређаје са ограниченим ресурсима  
   - Оптимизовани протоколи за окружења са малом пропусношћу  
   - Специјализоване MCP имплементације за IoT екосистеме  

5. **Регулаторни оквири**  
   - Развој MCP проширења за регулаторну усклађеност  
   - Стандардизовани трагови ревизије и интерфејси за објашњивост  
   - Интеграција са новим оквирима за управљање AI-ом  

### MCP решења од Microsoft-а  

Microsoft и Azure су развили неколико open-source репозиторијума како би помогли програмерима да имплементирају MCP у различитим сценаријима:  

#### Microsoft организација  

1. [playwright-mcp](https://github.com/microsoft/playwright-mcp) - Playwright MCP сервер за аутоматизацију и тестирање прегледача  
2. [files-mcp-server](https://github.com/microsoft/files-mcp-server) - MCP сервер за OneDrive за локално тестирање и допринос заједнице  
3. [NLWeb](https://github.com/microsoft/NlWeb) - NLWeb је колекција отворених протокола и алата за AI Web  

#### Azure-Samples организација  

1. [mcp](https://github.com/Azure-Samples/mcp) - Линкови ка примерима, алатима и ресурсима за изградњу и интеграцију MCP сервера на Azure-у  
2. [mcp-auth-servers](https://github.com/Azure-Samples/mcp-auth-servers) - Референтни MCP сервери који демонстрирају аутентификацију са тренутном спецификацијом Model Context Protocol-а  
3. [remote-mcp-functions](https://github.com/Azure-Samples/remote-mcp-functions) - MCP сервери у Azure Functions са линковима ка језичким репозиторијумима  
4. [remote-mcp-functions-python](https://github.com/Azure-Samples/remote-mcp-functions-python) - Брзи шаблон за MCP сервере у Python-у  
5. [remote-mcp-functions-dotnet](https://github.com/Azure-Samples/remote-mcp-functions-dotnet) - MCP сервери у .NET/C#  
6. [remote-mcp-functions-typescript](https://github.com/Azure-Samples/remote-mcp-functions-typescript) - MCP сервери у TypeScript-у  
7. [remote-mcp-apim-functions-python](https://github.com/Azure-Samples/remote-mcp-apim-functions-python) - Azure API Management као AI Gateway за MCP сервере у Python-у  
8. [AI-Gateway](https://github.com/Azure-Samples/AI-Gateway) - APIM ❤️ AI експерименти са MCP могућностима  

Ови репозиторијуми пружају различите имплементације, шаблоне и ресурсе за рад са Model Context Protocol-ом у различитим програмским језицима и Azure услугама.  

#### MCP Resources Directory  

[Директоријум MCP ресурса](https://github.com/microsoft/mcp/tree/main/Resources) у званичном Microsoft MCP репозиторијуму нуди курирану колекцију узорака ресурса, предлошка упита и дефиниција алата за употребу са MCP серверима.  

### Истраживачке могућности  

- Ефикасне технике оптимизације упита у MCP оквирима  
- Модели безбедности за MCP имплементације са више корисника  
- Бенчмаркинг перформанси различитих MCP имплементација  
- Формалне методе верификације за MCP сервере  

## Закључак  

Model Context Protocol (MCP) брзо обликује будућност стандардизоване, безбедне и интероперабилне AI интеграције у различитим индустријама. Кроз студије случаја и практичне пројекте у овом лекцији, видели сте како рани усвајачи, укључујући Microsoft и Azure, користе MCP за решавање изазова, убрзавање усвајања AI-а и обезбеђивање усклађености, безбедности и скалабилности.  

## Додатни ресурси  

- [MCP Foundry GitHub Repository](https://github.com/azure-ai-foundry/mcp-foundry)  
- [Foundry MCP Playground](https://github.com/azure-ai-foundry/foundry-mcp-playground)  
- [Integrating Azure AI Agents with MCP (Microsoft Foundry Blog)](https://devblogs.microsoft.com/foundry/integrating-azure-ai-agents-mcp/)  
- [MCP GitHub Repository (Microsoft)](https://github.com/microsoft/mcp)  
- [MCP Resources Directory (Sample Prompts, Tools, and Resource Definitions)](https://github.com/microsoft/mcp/tree/main/Resources)  
- [MCP Community & Documentation](https://modelcontextprotocol.io/introduction)  
- [Azure MCP Documentation](https://aka.ms/azmcp)  
- [Playwright MCP Server GitHub Repository](https://github.com/microsoft/playwright-mcp)  
- [Files MCP Server (OneDrive)](https://github.com/microsoft/files-mcp-server)  
- [Azure-Samples MCP](https://github.com/Azure-Samples/mcp)  
- [MCP Auth Servers (Azure-Samples)](https://github.com/Azure-Samples/mcp-auth-servers)  
- [Remote MCP Functions (Azure-Samples)](https://github.com/Azure-Samples/remote-mcp-functions)  
- [Remote MCP Functions Python (Azure-Samples)](https://github.com/Azure-Samples/remote-mcp-functions-python)  
- [Remote MCP Functions .NET (Azure-Samples)](https://github.com/Azure-Samples/remote-mcp-functions-dotnet)  
- [Remote MCP Functions TypeScript (Azure-Samples)](https://github.com/Azure-Samples/remote-mcp-functions-typescript)  
- [Remote MCP APIM Functions Python (Azure-Samples)](https://github.com/Azure-Samples/remote-mcp-apim-functions-python)  
- [AI-Gateway (Azure-Samples)](https://github.com/Azure-Samples/AI-Gateway)  
- [Microsoft AI and Automation Solutions](https://azure.microsoft.com/en-us/products/ai-services/)  

## Вежбе  

1. Анализирајте једну од студија случаја и предложите алтернативни приступ имплементацији.  
2. Изаберите једну од идеја за пројекат и направите детаљну техничку спецификацију.  
3. Истражите индустрију која није покривена у студијама случаја и опишите како MCP може решити њене специфичне изазове.  
4. Истражите један од будућих праваца и креирајте концепт за ново MCP проширење које га подржава.  

Следеће: [Microsoft MCP Server](../07-LessonsfromEarlyAdoption/microsoft-mcp-servers.md)  

**Одрицање од одговорности**:  
Овај документ је преведен коришћењем услуге за превођење помоћу вештачке интелигенције [Co-op Translator](https://github.com/Azure/co-op-translator). Иако се трудимо да обезбедимо тачност, молимо вас да имате у виду да аутоматски преводи могу садржати грешке или нетачности. Оригинални документ на његовом изворном језику треба сматрати ауторитативним извором. За критичне информације препоручује се професионални превод од стране људи. Не преузимамо одговорност за било каква погрешна тумачења или неспоразуме који могу произаћи из коришћења овог превода.