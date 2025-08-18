<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0df1ee78a6dd8300f3a040ca5b411c2e",
  "translation_date": "2025-08-18T22:41:29+00:00",
  "source_file": "00-Introduction/README.md",
  "language_code": "sl"
}
-->
# Uvod v Model Context Protocol (MCP): Zakaj je pomemben za razširljive AI aplikacije

[![Uvod v Model Context Protocol](../../../translated_images/01.a467036d886b5fb5b9cf7b39bac0e743b6ca0a4a18a492de90061daaf0cc55f0.sl.png)](https://youtu.be/agBbdiOPLQA)

_(Kliknite na zgornjo sliko za ogled videa te lekcije)_

Generativne AI aplikacije predstavljajo velik korak naprej, saj pogosto omogočajo uporabniku interakcijo z aplikacijo prek naravnih jezikovnih pozivov. Vendar pa, ko se v takšne aplikacije vlaga več časa in virov, želite zagotoviti, da lahko funkcionalnosti in vire enostavno integrirate na način, ki omogoča razširljivost, da aplikacija podpira več modelov in obvladuje različne posebnosti modelov. Skratka, gradnja generativnih AI aplikacij je na začetku enostavna, vendar postane bolj zapletena, ko rastejo in se razvijajo. Takrat je treba začeti definirati arhitekturo in se verjetno zanašati na standard, ki zagotavlja dosledno gradnjo aplikacij. Tukaj nastopi MCP, ki organizira stvari in zagotavlja standard.

---

## **🔍 Kaj je Model Context Protocol (MCP)?**

**Model Context Protocol (MCP)** je **odprt, standardiziran vmesnik**, ki omogoča brezhibno interakcijo velikih jezikovnih modelov (LLM) z zunanjimi orodji, API-ji in viri podatkov. Ponuja dosledno arhitekturo za izboljšanje funkcionalnosti AI modelov onkraj njihovih učnih podatkov, kar omogoča pametnejše, razširljive in bolj odzivne AI sisteme.

---

## **🎯 Zakaj je standardizacija v AI pomembna**

Ko generativne AI aplikacije postajajo bolj kompleksne, je ključnega pomena sprejeti standarde, ki zagotavljajo **razširljivost, prilagodljivost, vzdržljivost** in **izogibanje odvisnosti od enega ponudnika**. MCP naslavlja te potrebe z:

- Poenotenjem integracij med modeli in orodji
- Zmanjšanjem krhkih, enkratnih rešitev po meri
- Omogočanjem sobivanja več modelov različnih ponudnikov znotraj enega ekosistema

**Opomba:** Čeprav MCP sebe predstavlja kot odprt standard, ni načrtov za standardizacijo MCP prek obstoječih standardizacijskih teles, kot so IEEE, IETF, W3C, ISO ali katero koli drugo telo.

---

## **📚 Cilji učenja**

Do konca tega članka boste lahko:

- Definirali **Model Context Protocol (MCP)** in njegove primere uporabe
- Razumeli, kako MCP standardizira komunikacijo med modeli in orodji
- Identificirali ključne komponente MCP arhitekture
- Raziskali resnične primere uporabe MCP v podjetniških in razvojnih kontekstih

---

## **💡 Zakaj je Model Context Protocol (MCP) prelomnica**

### **🔗 MCP rešuje fragmentacijo v AI interakcijah**

Pred MCP je integracija modelov z orodji zahtevala:

- Kodo po meri za vsak par orodje-model
- Nestandardne API-je za vsakega ponudnika
- Pogoste prekinitve zaradi posodobitev
- Slabo razširljivost z več orodji

### **✅ Prednosti standardizacije MCP**

| **Prednost**              | **Opis**                                                                        |
|---------------------------|--------------------------------------------------------------------------------|
| Interoperabilnost         | LLM-ji delujejo brezhibno z orodji različnih ponudnikov                        |
| Doslednost                | Enotno vedenje na različnih platformah in orodjih                              |
| Ponovna uporaba           | Orodja, zgrajena enkrat, se lahko uporabljajo v različnih projektih in sistemih |
| Pospešen razvoj           | Zmanjšanje časa razvoja z uporabo standardiziranih vmesnikov, ki jih je mogoče enostavno vključiti |

---

## **🧱 Pregled visoke ravni MCP arhitekture**

MCP sledi **modelu odjemalec-strežnik**, kjer:

- **MCP gostitelji** poganjajo AI modele
- **MCP odjemalci** sprožijo zahteve
- **MCP strežniki** zagotavljajo kontekst, orodja in zmogljivosti

### **Ključne komponente:**

- **Viri** – Statični ali dinamični podatki za modele  
- **Pozivi** – Vnaprej določeni delovni tokovi za usmerjeno generacijo  
- **Orodja** – Izvedljive funkcije, kot so iskanje, izračuni  
- **Vzorčenje** – Agentno vedenje prek rekurzivnih interakcij

---

## Kako delujejo MCP strežniki

MCP strežniki delujejo na naslednji način:

- **Tok zahteve**:
    1. Zahtevo sproži končni uporabnik ali programska oprema, ki deluje v njegovem imenu.
    2. **MCP odjemalec** pošlje zahtevo **MCP gostitelju**, ki upravlja z AI modelom.
    3. **AI model** prejme uporabniški poziv in lahko zahteva dostop do zunanjih orodij ali podatkov prek enega ali več klicev orodij.
    4. **MCP gostitelj**, ne model neposredno, komunicira z ustreznim **MCP strežnikom** prek standardiziranega protokola.
- **Funkcionalnost MCP gostitelja**:
    - **Register orodij**: Vzdržuje katalog razpoložljivih orodij in njihovih zmogljivosti.
    - **Avtentikacija**: Preverja dovoljenja za dostop do orodij.
    - **Obdelovalec zahtev**: Obdeluje dohodne zahteve za orodja od modela.
    - **Oblikovalec odgovorov**: Strukturira izhode orodij v format, ki ga model razume.
- **Izvedba MCP strežnika**:
    - **MCP gostitelj** usmerja klice orodij na enega ali več **MCP strežnikov**, ki izpostavljajo specializirane funkcije (npr. iskanje, izračuni, poizvedbe v podatkovnih bazah).
    - **MCP strežniki** izvajajo svoje operacije in vrnejo rezultate **MCP gostitelju** v doslednem formatu.
    - **MCP gostitelj** oblikuje in posreduje te rezultate **AI modelu**.
- **Zaključek odgovora**:
    - **AI model** vključi izhode orodij v končni odgovor.
    - **MCP gostitelj** pošlje ta odgovor nazaj **MCP odjemalcu**, ki ga dostavi končnemu uporabniku ali programski opremi.

```mermaid
---
title: MCP Architecture and Component Interactions
description: A diagram showing the flows of the components in MCP.
---
graph TD
    Client[MCP Client/Application] -->|Sends Request| H[MCP Host]
    H -->|Invokes| A[AI Model]
    A -->|Tool Call Request| H
    H -->|MCP Protocol| T1[MCP Server Tool 01: Web Search]
    H -->|MCP Protocol| T2[MCP Server Tool 02: Calculator tool]
    H -->|MCP Protocol| T3[MCP Server Tool 03: Database Access tool]
    H -->|MCP Protocol| T4[MCP Server Tool 04: File System tool]
    H -->|Sends Response| Client

    subgraph "MCP Host Components"
        H
        G[Tool Registry]
        I[Authentication]
        J[Request Handler]
        K[Response Formatter]
    end

    H <--> G
    H <--> I
    H <--> J
    H <--> K

    style A fill:#f9d5e5,stroke:#333,stroke-width:2px
    style H fill:#eeeeee,stroke:#333,stroke-width:2px
    style Client fill:#d5e8f9,stroke:#333,stroke-width:2px
    style G fill:#fffbe6,stroke:#333,stroke-width:1px
    style I fill:#fffbe6,stroke:#333,stroke-width:1px
    style J fill:#fffbe6,stroke:#333,stroke-width:1px
    style K fill:#fffbe6,stroke:#333,stroke-width:1px
    style T1 fill:#c2f0c2,stroke:#333,stroke-width:1px
    style T2 fill:#c2f0c2,stroke:#333,stroke-width:1px
    style T3 fill:#c2f0c2,stroke:#333,stroke-width:1px
    style T4 fill:#c2f0c2,stroke:#333,stroke-width:1px
```

## 👨‍💻 Kako zgraditi MCP strežnik (z zgledi)

MCP strežniki omogočajo razširitev zmogljivosti LLM-jev z zagotavljanjem podatkov in funkcionalnosti.

Pripravljeni za preizkus? Tukaj so SDK-ji za specifične jezike in/ali ogrodja z zgledi za ustvarjanje preprostih MCP strežnikov v različnih jezikih/ogrodjih:

- **Python SDK**: https://github.com/modelcontextprotocol/python-sdk

- **TypeScript SDK**: https://github.com/modelcontextprotocol/typescript-sdk

- **Java SDK**: https://github.com/modelcontextprotocol/java-sdk

- **C#/.NET SDK**: https://github.com/modelcontextprotocol/csharp-sdk

---

## 🌍 Resnični primeri uporabe MCP

MCP omogoča širok spekter aplikacij z razširitvijo zmogljivosti AI:

| **Aplikacija**              | **Opis**                                                                        |
|-----------------------------|--------------------------------------------------------------------------------|
| Integracija podatkov v podjetju | Povezovanje LLM-jev s podatkovnimi bazami, CRM-ji ali internimi orodji         |
| Agentni AI sistemi          | Omogočanje avtonomnih agentov z dostopom do orodij in delovnimi tokovi odločanja |
| Multimodalne aplikacije     | Združevanje besedilnih, slikovnih in zvočnih orodij znotraj ene AI aplikacije   |
| Integracija podatkov v realnem času | Vključevanje živih podatkov v AI interakcije za bolj natančne, aktualne izhode |

---

### 🧠 MCP = Univerzalni standard za AI interakcije

Model Context Protocol (MCP) deluje kot univerzalni standard za AI interakcije, podobno kot je USB-C standardiziral fizične povezave za naprave. V svetu AI MCP zagotavlja dosleden vmesnik, ki omogoča modelom (odjemalcem) brezhibno integracijo z zunanjimi orodji in ponudniki podatkov (strežniki). To odpravlja potrebo po raznolikih, prilagojenih protokolih za vsak API ali vir podatkov.

---

### 💡 Omogoča dostop do znanja

Poleg ponujanja orodij MCP omogoča tudi dostop do znanja. Aplikacijam omogoča, da zagotavljajo kontekst velikim jezikovnim modelom (LLM) z povezovanjem z različnimi viri podatkov. Na primer, MCP strežnik lahko predstavlja dokumentni repozitorij podjetja, ki agentom omogoča pridobivanje relevantnih informacij po potrebi. Drug strežnik lahko obravnava specifične akcije, kot so pošiljanje e-pošte ali posodabljanje zapisov. Iz perspektive agenta so to preprosto orodja, ki jih lahko uporablja—nekatera orodja vračajo podatke (kontekst znanja), druga pa izvajajo akcije. MCP učinkovito upravlja oboje.

---

### 👉 Primer: Razširljiva rešitev za agente

```mermaid
---
title: Scalable Agent Solution with MCP
description: A diagram illustrating how a user interacts with an LLM that connects to multiple MCP servers, with each server providing both knowledge and tools, creating a scalable AI system architecture
---
graph TD
    User -->|Prompt| LLM
    LLM -->|Response| User
    LLM -->|MCP| ServerA
    LLM -->|MCP| ServerB
    ServerA -->|Universal connector| ServerB
    ServerA --> KnowledgeA
    ServerA --> ToolsA
    ServerB --> KnowledgeB
    ServerB --> ToolsB

    subgraph Server A
        KnowledgeA[Knowledge]
        ToolsA[Tools]
    end

    subgraph Server B
        KnowledgeB[Knowledge]
        ToolsB[Tools]
    end
```

---

### 🔄 Napredni scenariji MCP z integracijo LLM na strani odjemalca

Poleg osnovne MCP arhitekture obstajajo napredni scenariji, kjer sta tako odjemalec kot strežnik opremljena z LLM-ji, kar omogoča bolj sofisticirane interakcije. Na spodnjem diagramu je **odjemalska aplikacija** lahko IDE z več MCP orodji, ki jih LLM lahko uporablja:

```mermaid
---
title: Advanced MCP Scenarios with Client-Server LLM Integration
description: A sequence diagram showing the detailed interaction flow between user, client application, client LLM, multiple MCP servers, and server LLM, illustrating tool discovery, user interaction, direct tool calling, and feature negotiation phases
---
sequenceDiagram
    autonumber
    actor User as 👤 User
    participant ClientApp as 🖥️ Client App
    participant ClientLLM as 🧠 Client LLM
    participant Server1 as 🔧 MCP Server 1
    participant Server2 as 📚 MCP Server 2
    participant ServerLLM as 🤖 Server LLM
    
    %% Discovery Phase
    rect rgb(220, 240, 255)
        Note over ClientApp, Server2: TOOL DISCOVERY PHASE
        ClientApp->>+Server1: Request available tools/resources
        Server1-->>-ClientApp: Return tool list (JSON)
        ClientApp->>+Server2: Request available tools/resources
        Server2-->>-ClientApp: Return tool list (JSON)
        Note right of ClientApp: Store combined tool<br/>catalog locally
    end
    
    %% User Interaction
    rect rgb(255, 240, 220)
        Note over User, ClientLLM: USER INTERACTION PHASE
        User->>+ClientApp: Enter natural language prompt
        ClientApp->>+ClientLLM: Forward prompt + tool catalog
        ClientLLM->>-ClientLLM: Analyze prompt & select tools
    end
    
    %% Scenario A: Direct Tool Calling
    alt Direct Tool Calling
        rect rgb(220, 255, 220)
            Note over ClientApp, Server1: SCENARIO A: DIRECT TOOL CALLING
            ClientLLM->>+ClientApp: Request tool execution
            ClientApp->>+Server1: Execute specific tool
            Server1-->>-ClientApp: Return results
            ClientApp->>+ClientLLM: Process results
            ClientLLM-->>-ClientApp: Generate response
            ClientApp-->>-User: Display final answer
        end
    
    %% Scenario B: Feature Negotiation (VS Code style)
    else Feature Negotiation (VS Code style)
        rect rgb(255, 220, 220)
            Note over ClientApp, ServerLLM: SCENARIO B: FEATURE NEGOTIATION
            ClientLLM->>+ClientApp: Identify needed capabilities
            ClientApp->>+Server2: Negotiate features/capabilities
            Server2->>+ServerLLM: Request additional context
            ServerLLM-->>-Server2: Provide context
            Server2-->>-ClientApp: Return available features
            ClientApp->>+Server2: Call negotiated tools
            Server2-->>-ClientApp: Return results
            ClientApp->>+ClientLLM: Process results
            ClientLLM-->>-ClientApp: Generate response
            ClientApp-->>-User: Display final answer
        end
    end
```

---

## 🔐 Praktične prednosti MCP

Tukaj so praktične prednosti uporabe MCP:

- **Svežina**: Modeli lahko dostopajo do aktualnih informacij onkraj svojih učnih podatkov
- **Razširitev zmogljivosti**: Modeli lahko uporabljajo specializirana orodja za naloge, za katere niso bili usposobljeni
- **Zmanjšanje halucinacij**: Zunanji viri podatkov zagotavljajo dejansko utemeljitev
- **Zasebnost**: Občutljivi podatki lahko ostanejo znotraj varnih okolij namesto da bi bili vključeni v pozive

---

## 📌 Ključne točke

Naslednje so ključne točke za uporabo MCP:

- **MCP** standardizira, kako AI modeli komunicirajo z orodji in podatki
- Spodbuja **razširljivost, doslednost in interoperabilnost**
- MCP pomaga **zmanjšati čas razvoja, izboljšati zanesljivost in razširiti zmogljivosti modelov**
- Arhitektura odjemalec-strežnik **omogoča prilagodljive, razširljive AI aplikacije**

---

## 🧠 Naloga

Razmislite o AI aplikaciji, ki jo želite zgraditi.

- Katera **zunanja orodja ali podatki** bi lahko izboljšali njene zmogljivosti?
- Kako bi MCP lahko naredil integracijo **enostavnejšo in zanesljivejšo?**

---

## Dodatni viri

- [MCP GitHub repozitorij](https://github.com/modelcontextprotocol)

---

## Kaj sledi

Naprej: [Poglavje 1: Osnovni koncepti](../01-CoreConcepts/README.md)

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za strojno prevajanje [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas opozarjamo, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo strokovno človeško prevajanje. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki izhajajo iz uporabe tega prevoda.