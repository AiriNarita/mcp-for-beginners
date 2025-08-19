<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "787440926586cd064b0899fd1c514f52",
  "translation_date": "2025-07-14T07:15:13+00:00",
  "source_file": "10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/README.md",
  "language_code": "hr"
}
-->
# Optimizacija AI Radnih Tokova: Izgradnja MCP Servera s AI Toolkitom

[![MCP Verzija](https://img.shields.io/badge/MCP-1.9.3-blue.svg)](https://modelcontextprotocol.io/)
[![Python](https://img.shields.io/badge/Python-3.10+-green.svg)](https://python.org)
[![VS Code](https://img.shields.io/badge/VS%20Code-Latest-orange.svg)](https://code.visualstudio.com/)

![logo](../../../translated_images/logo.ec93918ec338dadde1715c8aaf118079e0ed0502e9efdfcc84d6a0f4a9a70ae8.hr.png)

## 🎯 Pregled

[![Izgradnja AI Agenta u VS Code: 4 Praktične Radionice s MCP i AI Toolkitom](../../../translated_images/11.0f6db6a0fb6068856d0468590a120ffe35dbccc49b93dc88b2003f306c81493a.hr.png)](https://youtu.be/r34Csn3rkeQ)

_(Kliknite na sliku iznad za pregled videa ove lekcije)_

Dobrodošli na **Model Context Protocol (MCP) Radionicu**! Ova sveobuhvatna praktična radionica kombinira dvije napredne tehnologije kako bi revolucionirala razvoj AI aplikacija:

- **🔗 Model Context Protocol (MCP)**: Otvoreni standard za besprijekornu integraciju AI alata
- **🛠️ AI Toolkit za Visual Studio Code (AITK)**: Microsoftov moćni dodatak za razvoj AI-a

### 🎓 Što ćete naučiti

Do kraja ove radionice, savladat ćete umjetnost izgradnje inteligentnih aplikacija koje povezuju AI modele s alatima i uslugama iz stvarnog svijeta. Od automatiziranog testiranja do prilagođenih API integracija, steći ćete praktične vještine za rješavanje složenih poslovnih izazova.

## 🏗️ Tehnološki Stack

### 🔌 Model Context Protocol (MCP)

MCP je **"USB-C za AI"** - univerzalni standard koji povezuje AI modele s vanjskim alatima i izvorima podataka.

**✨ Ključne značajke:**
- 🔄 **Standardizirana integracija**: univerzalno sučelje za povezivanje AI alata
- 🏛️ **Fleksibilna arhitektura**: lokalni i udaljeni serveri preko stdio/SSE transporta
- 🧰 **Bogati ekosustav**: alati, promptovi i resursi u jednom protokolu
- 🔒 **Spreman za poduzeća**: ugrađena sigurnost i pouzdanost

**🎯 Zašto je MCP važan:**
Baš kao što je USB-C uklonio nered s kabelima, MCP uklanja složenost AI integracija. Jedan protokol, beskonačne mogućnosti.

### 🤖 AI Toolkit za Visual Studio Code (AITK)

Microsoftov vodeći dodatak za razvoj AI-ja koji pretvara VS Code u moćan AI alat.

**🚀 Osnovne mogućnosti:**
- 📦 **Katalog modela**: pristup modelima s Azure AI, GitHub, Hugging Face, Ollama
- ⚡ **Lokalna inferencija**: ONNX optimizirano izvođenje na CPU/GPU/NPU
- 🏗️ **Agent Builder**: vizualni razvoj AI agenata s MCP integracijom
- 🎭 **Višestruki modaliteti**: podrška za tekst, viziju i strukturirani izlaz

**💡 Prednosti razvoja:**
- Deploy modela bez konfiguracije
- Vizualno kreiranje promptova
- Igralište za testiranje u stvarnom vremenu
- Besprijekorna integracija MCP servera

## 📚 Put Učenja

### [🚀 Modul 1: Osnove AI Toolkita](./lab1/README.md)

**Trajanje**: 15 minuta
- 🛠️ Instalirajte i konfigurirajte AI Toolkit za VS Code
- 🗂️ Istražite Katalog modela (100+ modela s GitHub, ONNX, OpenAI, Anthropic, Google)
- 🎮 Savladajte Interaktivno igralište za testiranje modela u stvarnom vremenu
- 🤖 Izradite svog prvog AI agenta pomoću Agent Buildera
- 📊 Procijenite performanse modela s ugrađenim metrima (F1, relevantnost, sličnost, koherentnost)
- ⚡ Naučite o batch obradi i podršci za višemodalne podatke

**🎯 Ishod učenja**: Izradite funkcionalnog AI agenta s potpunim razumijevanjem AITK mogućnosti

### [🌐 Modul 2: Osnove MCP-a s AI Toolkitom](./lab2/README.md)

**Trajanje**: 20 minuta
- 🧠 Savladajte arhitekturu i koncepte Model Context Protocola (MCP)
- 🌐 Istražite Microsoftov MCP server ekosustav
- 🤖 Izradite agenta za automatizaciju preglednika koristeći Playwright MCP server
- 🔧 Integrirajte MCP servere s AI Toolkit Agent Builderom
- 📊 Konfigurirajte i testirajte MCP alate unutar svojih agenata
- 🚀 Izvezite i implementirajte agente pokretane MCP-om za produkciju

**🎯 Ishod učenja**: Implementirajte AI agenta pojačanog vanjskim alatima putem MCP-a

### [🔧 Modul 3: Napredni razvoj MCP-a s AI Toolkitom](./lab3/README.md)
**Trajanje**: 20 minuta
- 💻 Kreirajte prilagođene MCP servere koristeći AI Toolkit
- 🐍 Konfigurirajte i koristite najnoviji MCP Python SDK (v1.9.3)
- 🔍 Postavite i koristite MCP Inspector za otklanjanje pogrešaka
- 🛠️ Izradite Weather MCP Server s profesionalnim radnim tokovima za debugiranje
- 🧪 Debugirajte MCP servere u Agent Builderu i Inspector okruženjima

**🎯 Ishod učenja**: Razvijajte i otklanjajte pogreške na prilagođenim MCP serverima s modernim alatima

### [🐙 Modul 4: Praktični razvoj MCP-a - prilagođeni GitHub Clone Server](./lab4/README.md)
**Trajanje**: 30 minuta
- 🏗️ Izradite stvarni GitHub Clone MCP Server za razvojne radne tokove
- 🔄 Implementirajte pametno kloniranje repozitorija s validacijom i rukovanjem pogreškama
- 📁 Kreirajte inteligentno upravljanje direktorijima i integraciju s VS Codeom
- 🤖 Koristite GitHub Copilot Agent Mode s prilagođenim MCP alatima
- 🛡️ Primijenite pouzdanost spremnu za produkciju i kompatibilnost na više platformi

**🎯 Ishod učenja**: Implementirajte produkcijski spreman MCP server koji pojednostavljuje stvarne razvojne procese

## 💡 Primjene u Stvarnom Svijetu i Utjecaj

### 🏢 Primjeri za poduzeća

#### 🔄 DevOps automatizacija
Transformirajte svoj razvojni tijek rada inteligentnom automatizacijom:
- **Pametno upravljanje repozitorijima**: AI vođeni pregled koda i odluke o spajanju
- **Inteligentni CI/CD**: automatizirana optimizacija pipelinea na temelju promjena u kodu
- **Triage problema**: automatska klasifikacija i dodjela bugova

#### 🧪 Revolucija osiguranja kvalitete
Podignite testiranje na novu razinu uz AI automatizaciju:
- **Inteligentno generiranje testova**: automatsko kreiranje sveobuhvatnih testnih skupova
- **Vizualno regresijsko testiranje**: AI detekcija promjena u UI-ju
- **Praćenje performansi**: proaktivno otkrivanje i rješavanje problema

#### 📊 Inteligencija podatkovnih tokova
Izgradite pametnije radne tokove obrade podataka:
- **Adaptivni ETL procesi**: samopodešavajuće transformacije podataka
- **Detekcija anomalija**: praćenje kvalitete podataka u stvarnom vremenu
- **Inteligentno usmjeravanje**: pametno upravljanje protokom podataka

#### 🎧 Unapređenje korisničkog iskustva
Stvorite izvanredne interakcije s korisnicima:
- **Podrška svjesna konteksta**: AI agenti s pristupom povijesti korisnika
- **Proaktivno rješavanje problema**: prediktivna korisnička podrška
- **Integracija na više kanala**: jedinstveno AI iskustvo na svim platformama

## 🛠️ Preduvjeti i Postavljanje

### 💻 Zahtjevi sustava

| Komponenta | Zahtjev | Napomene |
|------------|---------|----------|
| **Operativni Sustav** | Windows 10+, macOS 10.15+, Linux | Bilo koji moderni OS |
| **Visual Studio Code** | Najnovija stabilna verzija | Potrebno za AITK |
| **Node.js** | v18.0+ i npm | Za razvoj MCP servera |
| **Python** | 3.10+ | Opcionalno za Python MCP servere |
| **Memorija** | minimalno 8GB RAM | Preporučeno 16GB za lokalne modele |

#### Preporučeni Dodaci za VS Code

#### Preporučeni VS Code dodaci
- **AI Toolkit** (ms-windows-ai-studio.windows-ai-studio)
- **Python** (ms-python.python)
- **Python Debugger** (ms-python.debugpy)
- **GitHub Copilot** (GitHub.copilot) - Opcionalno, ali korisno

#### Opcionalni alati
- **uv**: moderan Python package manager
- **MCP Inspector**: vizualni alat za debugiranje MCP servera
- **Playwright**: za primjere web automatizacije

## 🎖️ Ishodi učenja i put certifikacije

### 🏆 Popis za savladavanje vještina

Završetkom ove radionice postići ćete stručnost u:

#### 🎯 Temeljne kompetencije
- [ ] **MCP protokol**: duboko razumijevanje arhitekture i obrazaca implementacije
- [ ] **AITK stručnost**: vrhunska upotreba AI Toolkita za brzi razvoj
- [ ] **Razvoj prilagođenih servera**: izrada, implementacija i održavanje produkcijskih MCP servera
- [ ] **Izvrsnost u integraciji alata**: besprijekorno povezivanje AI-ja s postojećim razvojnim procesima
- [ ] **Primjena rješavanja problema**: korištenje naučenih vještina za stvarne poslovne izazove

#### 🔧 Tehničke vještine
- [ ] Postavljanje i konfiguracija AI Toolkita u VS Codeu
- [ ] Dizajn i implementacija prilagođenih MCP servera
- [ ] Integracija GitHub modela s MCP arhitekturom
- [ ] Izgradnja automatiziranih testnih radnih tokova s Playwrightom
- [ ] Implementacija AI agenata za produkcijsku upotrebu
- [ ] Otklanjanje grešaka i optimizacija performansi MCP servera

#### 🚀 Napredne sposobnosti
- [ ] Arhitektura AI integracija na razini poduzeća
- [ ] Implementacija sigurnosnih najboljih praksi za AI aplikacije
- [ ] Dizajn skalabilnih MCP server arhitektura
- [ ] Kreiranje prilagođenih lanaca alata za specifične domene
- [ ] Mentoriranje drugih u razvoju AI aplikacija

## 📖 Dodatni resursi
- [MCP specifikacija](https://modelcontextprotocol.io/docs)
- [AI Toolkit GitHub repozitorij](https://github.com/microsoft/vscode-ai-toolkit)
- [Zbirka uzoraka MCP servera](https://github.com/modelcontextprotocol/servers)
- [Vodič najboljih praksi](https://modelcontextprotocol.io/docs/best-practices)

---

**🚀 Spremni za revoluciju u razvoju AI-ja?**

Izgradimo budućnost inteligentnih aplikacija zajedno s MCP-om i AI Toolkitom!

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden korištenjem AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako težimo točnosti, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za kritične informacije preporučuje se profesionalni ljudski prijevod. Ne snosimo odgovornost za bilo kakva nesporazuma ili pogrešna tumačenja koja proizlaze iz korištenja ovog prijevoda.