<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0df1ee78a6dd8300f3a040ca5b411c2e",
  "translation_date": "2025-08-18T16:10:11+00:00",
  "source_file": "00-Introduction/README.md",
  "language_code": "ro"
}
-->
# Introducere în Model Context Protocol (MCP): De ce este important pentru aplicațiile AI scalabile

[![Introducere în Model Context Protocol](../../../translated_images/01.a467036d886b5fb5b9cf7b39bac0e743b6ca0a4a18a492de90061daaf0cc55f0.ro.png)](https://youtu.be/agBbdiOPLQA)

_(Faceți clic pe imaginea de mai sus pentru a viziona videoclipul acestei lecții)_

Aplicațiile AI generative reprezintă un mare pas înainte, deoarece permit utilizatorilor să interacționeze cu aplicația folosind comenzi în limbaj natural. Totuși, pe măsură ce se investesc mai mult timp și resurse în astfel de aplicații, este important să vă asigurați că puteți integra funcționalități și resurse într-un mod ușor de extins, astfel încât aplicația să poată funcționa cu mai multe modele și să gestioneze diversele particularități ale acestora. Pe scurt, construirea aplicațiilor AI generative este ușoară la început, dar, pe măsură ce acestea cresc și devin mai complexe, trebuie să începeți să definiți o arhitectură și, cel mai probabil, să vă bazați pe un standard pentru a vă asigura că aplicațiile sunt construite într-un mod consecvent. Aici intervine MCP pentru a organiza lucrurile și a oferi un standard.

---

## **🔍 Ce este Model Context Protocol (MCP)?**

**Model Context Protocol (MCP)** este o **interfață deschisă și standardizată** care permite modelelor de limbaj de mari dimensiuni (LLMs) să interacționeze fără probleme cu instrumente externe, API-uri și surse de date. MCP oferă o arhitectură consecventă pentru a extinde funcționalitatea modelelor AI dincolo de datele lor de antrenament, permițând sisteme AI mai inteligente, scalabile și mai receptive.

---

## **🎯 De ce contează standardizarea în AI**

Pe măsură ce aplicațiile AI generative devin mai complexe, este esențial să adoptați standarde care să asigure **scalabilitate, extensibilitate, mentenabilitate** și **evitarea dependenței de un singur furnizor**. MCP răspunde acestor nevoi prin:

- Unificarea integrărilor între modele și instrumente  
- Reducerea soluțiilor personalizate fragile  
- Permisiunea ca mai multe modele de la furnizori diferiți să coexiste într-un singur ecosistem  

**Notă:** Deși MCP se prezintă ca un standard deschis, nu există planuri de a standardiza MCP prin organisme de standardizare existente, cum ar fi IEEE, IETF, W3C, ISO sau altele.

---

## **📚 Obiective de învățare**

Până la finalul acestui articol, veți putea:

- Defini **Model Context Protocol (MCP)** și cazurile sale de utilizare  
- Înțelege cum MCP standardizează comunicarea între modele și instrumente  
- Identifica componentele de bază ale arhitecturii MCP  
- Explora aplicații reale ale MCP în contexte de afaceri și dezvoltare  

---

## **💡 De ce Model Context Protocol (MCP) este revoluționar**

### **🔗 MCP rezolvă fragmentarea în interacțiunile AI**

Înainte de MCP, integrarea modelelor cu instrumente necesita:

- Cod personalizat pentru fiecare pereche model-instrument  
- API-uri nestandardizate pentru fiecare furnizor  
- Defecțiuni frecvente din cauza actualizărilor  
- Scalabilitate redusă cu mai multe instrumente  

### **✅ Beneficiile standardizării MCP**

| **Beneficiu**              | **Descriere**                                                                |
|----------------------------|-------------------------------------------------------------------------------|
| Interoperabilitate         | LLM-urile funcționează fără probleme cu instrumente de la diferiți furnizori |
| Consistență                | Comportament uniform pe platforme și instrumente                             |
| Reutilizabilitate          | Instrumentele construite o dată pot fi utilizate în mai multe proiecte       |
| Dezvoltare accelerată      | Reducerea timpului de dezvoltare prin utilizarea interfețelor standardizate   |

---

## **🧱 Prezentare generală a arhitecturii MCP**

MCP urmează un model **client-server**, unde:

- **Gazdele MCP** rulează modelele AI  
- **Clienții MCP** inițiază cereri  
- **Serverele MCP** furnizează context, instrumente și capabilități  

### **Componente cheie:**

- **Resurse** – Date statice sau dinamice pentru modele  
- **Prompts** – Fluxuri de lucru predefinite pentru generare ghidată  
- **Instrumente** – Funcții executabile, cum ar fi căutări, calcule  
- **Sampling** – Comportament agentic prin interacțiuni recursive  

---

## Cum funcționează serverele MCP

Serverele MCP operează astfel:

- **Fluxul cererii**:
    1. O cerere este inițiată de un utilizator final sau de un software care acționează în numele acestuia.  
    2. **Clientul MCP** trimite cererea către o **Gazdă MCP**, care gestionează runtime-ul modelului AI.  
    3. **Modelul AI** primește promptul utilizatorului și poate solicita acces la instrumente sau date externe prin una sau mai multe apeluri de instrumente.  
    4. **Gazda MCP**, nu modelul direct, comunică cu **Serverul MCP** corespunzător folosind protocolul standardizat.  
- **Funcționalitatea gazdei MCP**:
    - **Registrul de instrumente**: Menține un catalog al instrumentelor disponibile și al capabilităților acestora.  
    - **Autentificare**: Verifică permisiunile pentru accesul la instrumente.  
    - **Handler de cereri**: Procesează cererile de instrumente primite de la model.  
    - **Formatarea răspunsurilor**: Structurează ieșirile instrumentelor într-un format pe care modelul îl poate înțelege.  
- **Execuția serverului MCP**:
    - **Gazda MCP** direcționează apelurile de instrumente către unul sau mai multe **Servere MCP**, fiecare expunând funcții specializate (de exemplu, căutări, calcule, interogări de baze de date).  
    - **Serverele MCP** își îndeplinesc operațiunile respective și returnează rezultatele către **Gazda MCP** într-un format consecvent.  
    - **Gazda MCP** formatează și retransmite aceste rezultate către **Modelul AI**.  
- **Finalizarea răspunsului**:
    - **Modelul AI** încorporează ieșirile instrumentelor într-un răspuns final.  
    - **Gazda MCP** trimite acest răspuns înapoi către **Clientul MCP**, care îl livrează utilizatorului final sau software-ului apelant.  

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

## 👨‍💻 Cum să construiți un server MCP (cu exemple)

Serverele MCP vă permit să extindeți capabilitățile LLM-urilor oferind date și funcționalități.

Gata să încercați? Iată SDK-uri specifice limbajului și/sau stack-ului, cu exemple de creare a unor servere MCP simple în diferite limbaje/stack-uri:

- **Python SDK**: https://github.com/modelcontextprotocol/python-sdk  
- **TypeScript SDK**: https://github.com/modelcontextprotocol/typescript-sdk  
- **Java SDK**: https://github.com/modelcontextprotocol/java-sdk  
- **C#/.NET SDK**: https://github.com/modelcontextprotocol/csharp-sdk  

---

## 🌍 Cazuri de utilizare reale pentru MCP

MCP permite o gamă largă de aplicații prin extinderea capabilităților AI:

| **Aplicație**               | **Descriere**                                                                |
|-----------------------------|-------------------------------------------------------------------------------|
| Integrarea datelor în companii | Conectarea LLM-urilor la baze de date, CRM-uri sau instrumente interne       |
| Sisteme AI agentice         | Permite agenților autonomi acces la instrumente și fluxuri de luare a deciziilor |
| Aplicații multi-modale      | Combinarea textului, imaginilor și sunetului într-o singură aplicație AI unificată |
| Integrarea datelor în timp real | Aducerea datelor live în interacțiunile AI pentru rezultate mai precise și actuale |

### 🧠 MCP = Standard universal pentru interacțiunile AI

Model Context Protocol (MCP) acționează ca un standard universal pentru interacțiunile AI, la fel cum USB-C a standardizat conexiunile fizice pentru dispozitive. În lumea AI, MCP oferă o interfață consecventă, permițând modelelor (clienți) să se integreze fără probleme cu instrumente și furnizori de date externi (servere). Acest lucru elimină necesitatea unor protocoale diverse și personalizate pentru fiecare API sau sursă de date.

Sub MCP, un instrument compatibil MCP (denumit server MCP) urmează un standard unificat. Aceste servere pot lista instrumentele sau acțiunile pe care le oferă și le pot executa atunci când sunt solicitate de un agent AI. Platformele de agenți AI care suportă MCP pot descoperi instrumentele disponibile de la servere și le pot invoca prin acest protocol standard.

### 💡 Facilitează accesul la cunoștințe

Dincolo de oferirea de instrumente, MCP facilitează și accesul la cunoștințe. Permite aplicațiilor să ofere context modelelor de limbaj de mari dimensiuni (LLMs) prin conectarea lor la diverse surse de date. De exemplu, un server MCP ar putea reprezenta un depozit de documente al unei companii, permițând agenților să recupereze informații relevante la cerere. Un alt server ar putea gestiona acțiuni specifice, cum ar fi trimiterea de e-mailuri sau actualizarea înregistrărilor. Din perspectiva agentului, acestea sunt pur și simplu instrumente pe care le poate utiliza—unele instrumente returnează date (context de cunoștințe), în timp ce altele efectuează acțiuni. MCP gestionează eficient ambele.

Un agent care se conectează la un server MCP învață automat capabilitățile disponibile și datele accesibile ale serverului printr-un format standard. Această standardizare permite disponibilitatea dinamică a instrumentelor. De exemplu, adăugarea unui nou server MCP în sistemul unui agent face ca funcțiile acestuia să fie imediat utilizabile, fără a necesita personalizări suplimentare ale instrucțiunilor agentului.

Această integrare simplificată se aliniază cu fluxul ilustrat în diagrama următoare, unde serverele oferă atât instrumente, cât și cunoștințe, asigurând o colaborare fără probleme între sisteme.

### 👉 Exemplu: Soluție scalabilă pentru agenți

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

### 🔄 Scenarii avansate MCP cu integrarea LLM pe partea clientului

Dincolo de arhitectura de bază MCP, există scenarii avansate în care atât clientul, cât și serverul conțin LLM-uri, permițând interacțiuni mai sofisticate. În diagrama următoare, **Aplicația Client** ar putea fi un IDE cu un număr de instrumente MCP disponibile pentru utilizare de către LLM:

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

## 🔐 Beneficii practice ale MCP

Iată beneficiile practice ale utilizării MCP:

- **Actualitate**: Modelele pot accesa informații actualizate dincolo de datele lor de antrenament  
- **Extinderea capabilităților**: Modelele pot utiliza instrumente specializate pentru sarcini pentru care nu au fost antrenate  
- **Reducerea halucinațiilor**: Sursele de date externe oferă o bază factuală  
- **Confidențialitate**: Datele sensibile pot rămâne în medii sigure, în loc să fie incluse în prompturi  

---

## 📌 Concluzii cheie

Iată concluziile cheie pentru utilizarea MCP:

- **MCP** standardizează modul în care modelele AI interacționează cu instrumentele și datele  
- Promovează **extensibilitatea, consistența și interoperabilitatea**  
- MCP ajută la **reducerea timpului de dezvoltare, îmbunătățirea fiabilității și extinderea capabilităților modelelor**  
- Arhitectura client-server **permite aplicații AI flexibile și extensibile**  

---

## 🧠 Exercițiu

Gândiți-vă la o aplicație AI pe care doriți să o construiți.

- Ce **instrumente sau date externe** ar putea îmbunătăți capabilitățile acesteia?  
- Cum ar putea MCP să facă integrarea **mai simplă și mai fiabilă**?  

---

## Resurse suplimentare

- [MCP GitHub Repository](https://github.com/modelcontextprotocol)

---

## Ce urmează

Următorul capitol: [Capitolul 1: Concepte de bază](../01-CoreConcepts/README.md)

**Declinare de responsabilitate**:  
Acest document a fost tradus folosind serviciul de traducere AI [Co-op Translator](https://github.com/Azure/co-op-translator). Deși ne străduim să asigurăm acuratețea, vă rugăm să fiți conștienți că traducerile automate pot conține erori sau inexactități. Documentul original în limba sa natală ar trebui considerat sursa autoritară. Pentru informații critice, se recomandă traducerea profesională realizată de un specialist uman. Nu ne asumăm responsabilitatea pentru eventualele neînțelegeri sau interpretări greșite care pot apărea din utilizarea acestei traduceri.