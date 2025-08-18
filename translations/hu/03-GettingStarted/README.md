<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "858362ce0118de3fec0f9114bf396101",
  "translation_date": "2025-08-18T19:29:30+00:00",
  "source_file": "03-GettingStarted/README.md",
  "language_code": "hu"
}
-->
## Első lépések  

[![Az első MCP szervered létrehozása](../../../translated_images/04.0ea920069efd979a0b2dad51e72c1df7ead9c57b3305796068a6cee1f0dd6674.hu.png)](https://youtu.be/sNDZO9N4m9Y)

_(Kattints a fenti képre a leckéhez tartozó videó megtekintéséhez)_

Ez a rész több leckéből áll:

- **1 Az első szervered**, ebben az első leckében megtanulod, hogyan hozd létre az első szervered, és hogyan vizsgáld meg az ellenőrző eszközzel, amely hasznos módja a szerver tesztelésének és hibakeresésének, [a leckéhez](01-first-server/README.md)

- **2 Kliens**, ebben a leckében megtanulod, hogyan írj egy klienst, amely csatlakozni tud a szerveredhez, [a leckéhez](02-client/README.md)

- **3 Kliens LLM-mel**, egy még jobb módja a kliens írásának, ha hozzáadsz egy LLM-et, amely "tárgyalni" tud a szervereddel arról, hogy mit tegyen, [a leckéhez](03-llm-client/README.md)

- **4 Szerver fogyasztása GitHub Copilot Agent módban a Visual Studio Code-ban**. Itt azt vizsgáljuk, hogyan futtassuk az MCP szerverünket a Visual Studio Code-on belül, [a leckéhez](04-vscode/README.md)

- **5 Fogyasztás SSE (Server Sent Events) segítségével**. Az SSE egy szabvány a szerverről kliensre történő adatfolyamhoz, amely lehetővé teszi a szerverek számára, hogy valós idejű frissítéseket küldjenek a klienseknek HTTP-n keresztül, [a leckéhez](05-sse-server/README.md)

- **6 HTTP adatfolyam MCP-vel (Streamable HTTP)**. Ismerd meg a modern HTTP adatfolyamot, a haladási értesítéseket, és hogyan valósíts meg skálázható, valós idejű MCP szervereket és klienseket Streamable HTTP használatával, [a leckéhez](06-http-streaming/README.md)

- **7 AI Toolkit használata a VSCode-ban** MCP kliensek és szerverek fogyasztásához és teszteléséhez, [a leckéhez](07-aitk/README.md)

- **8 Tesztelés**. Itt különösen arra koncentrálunk, hogyan tesztelhetjük a szerverünket és kliensünket különböző módokon, [a leckéhez](08-testing/README.md)

- **9 Telepítés**. Ez a fejezet az MCP megoldások különböző telepítési módjait vizsgálja, [a leckéhez](09-deployment/README.md)


A Model Context Protocol (MCP) egy nyílt protokoll, amely szabványosítja, hogyan biztosítanak az alkalmazások kontextust az LLM-ek számára. Gondolj az MCP-re úgy, mint egy USB-C portra az AI alkalmazások számára - szabványos módot kínál az AI modellek különböző adatforrásokhoz és eszközökhöz való csatlakoztatására.

## Tanulási célok

A lecke végére képes leszel:

- MCP fejlesztési környezeteket beállítani C#, Java, Python, TypeScript és JavaScript nyelveken
- Alapvető MCP szervereket építeni és telepíteni egyedi funkciókkal (erőforrások, promptok és eszközök)
- Host alkalmazásokat létrehozni, amelyek csatlakoznak MCP szerverekhez
- MCP implementációkat tesztelni és hibakeresni
- Gyakori beállítási kihívásokat és megoldásaikat megérteni
- MCP implementációkat népszerű LLM szolgáltatásokhoz csatlakoztatni

## MCP környezet beállítása

Mielőtt elkezdenéd az MCP-vel való munkát, fontos, hogy előkészítsd a fejlesztési környezetedet, és megértsd az alapvető munkafolyamatot. Ez a rész végigvezet az első lépések beállításán, hogy zökkenőmentesen kezdhesd el az MCP használatát.

### Előfeltételek

Mielőtt belevágnál az MCP fejlesztésbe, győződj meg róla, hogy rendelkezel:

- **Fejlesztési környezet**: A választott nyelvedhez (C#, Java, Python, TypeScript vagy JavaScript)
- **IDE/Szerkesztő**: Visual Studio, Visual Studio Code, IntelliJ, Eclipse, PyCharm vagy bármely modern kódszerkesztő
- **Csomagkezelők**: NuGet, Maven/Gradle, pip vagy npm/yarn
- **API kulcsok**: Az AI szolgáltatásokhoz, amelyeket a host alkalmazásaidban tervezel használni


### Hivatalos SDK-k

A következő fejezetekben Python, TypeScript, Java és .NET megoldásokat fogsz látni. Íme az összes hivatalosan támogatott SDK.

Az MCP több nyelvhez biztosít hivatalos SDK-kat:
- [C# SDK](https://github.com/modelcontextprotocol/csharp-sdk) - Microsofttal együttműködésben karbantartva
- [Java SDK](https://github.com/modelcontextprotocol/java-sdk) - Spring AI-val együttműködésben karbantartva
- [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) - A hivatalos TypeScript implementáció
- [Python SDK](https://github.com/modelcontextprotocol/python-sdk) - A hivatalos Python implementáció
- [Kotlin SDK](https://github.com/modelcontextprotocol/kotlin-sdk) - A hivatalos Kotlin implementáció
- [Swift SDK](https://github.com/modelcontextprotocol/swift-sdk) - Loopwork AI-val együttműködésben karbantartva
- [Rust SDK](https://github.com/modelcontextprotocol/rust-sdk) - A hivatalos Rust implementáció

## Főbb tanulságok

- Az MCP fejlesztési környezet beállítása egyszerű a nyelvspecifikus SDK-k segítségével
- MCP szerverek építése eszközök létrehozását és egyértelmű sémák szerinti regisztrálását igényli
- MCP kliensek csatlakoznak szerverekhez és modellekhez, hogy kibővített képességeket használjanak
- A tesztelés és hibakeresés elengedhetetlen a megbízható MCP implementációkhoz
- A telepítési lehetőségek a helyi fejlesztéstől a felhőalapú megoldásokig terjednek

## Gyakorlás

Van egy mintagyűjteményünk, amely kiegészíti az összes fejezetben látott gyakorlatokat. Ezen kívül minden fejezet saját gyakorlatokat és feladatokat is tartalmaz.

- [Java Kalkulátor](./samples/java/calculator/README.md)
- [.Net Kalkulátor](../../../03-GettingStarted/samples/csharp)
- [JavaScript Kalkulátor](./samples/javascript/README.md)
- [TypeScript Kalkulátor](./samples/typescript/README.md)
- [Python Kalkulátor](../../../03-GettingStarted/samples/python)

## További források

- [Ügynökök építése Model Context Protocol segítségével az Azure-on](https://learn.microsoft.com/azure/developer/ai/intro-agents-mcp)
- [Távoli MCP az Azure Container Apps segítségével (Node.js/TypeScript/JavaScript)](https://learn.microsoft.com/samples/azure-samples/mcp-container-ts/mcp-container-ts/)
- [.NET OpenAI MCP Ügynök](https://learn.microsoft.com/samples/azure-samples/openai-mcp-agent-dotnet/openai-mcp-agent-dotnet/)

## Mi következik?

Következő: [Az első MCP szerver létrehozása](01-first-server/README.md)

**Felelősségkizárás**:  
Ez a dokumentum az [Co-op Translator](https://github.com/Azure/co-op-translator) AI fordítási szolgáltatás segítségével készült. Bár törekszünk a pontosságra, kérjük, vegye figyelembe, hogy az automatikus fordítások hibákat vagy pontatlanságokat tartalmazhatnak. Az eredeti dokumentum az eredeti nyelvén tekintendő hiteles forrásnak. Kritikus információk esetén javasolt a professzionális, emberi fordítás igénybevétele. Nem vállalunk felelősséget a fordítás használatából eredő félreértésekért vagy téves értelmezésekért.