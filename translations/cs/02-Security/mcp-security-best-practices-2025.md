<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "057dd5cc6bea6434fdb788e6c93f3f3d",
  "translation_date": "2025-08-18T15:02:19+00:00",
  "source_file": "02-Security/mcp-security-best-practices-2025.md",
  "language_code": "cs"
}
-->
# MCP Bezpečnostní osvědčené postupy - Aktualizace srpen 2025

> **Důležité**: Tento dokument odráží nejnovější bezpečnostní požadavky [MCP Specifikace 2025-06-18](https://spec.modelcontextprotocol.io/specification/2025-06-18/) a oficiální [MCP Bezpečnostní osvědčené postupy](https://modelcontextprotocol.io/specification/2025-06-18/basic/security_best_practices). Vždy se odkazujte na aktuální specifikaci pro nejaktuálnější pokyny.

## Základní bezpečnostní postupy pro implementace MCP

Model Context Protocol přináší jedinečné bezpečnostní výzvy, které přesahují tradiční softwarovou bezpečnost. Tyto postupy se zaměřují na základní bezpečnostní požadavky i na specifické hrozby MCP, včetně injekce promptů, otravy nástrojů, únosu relací, problémů zmateného zástupce a zranitelností při předávání tokenů.

### **POVINNÉ bezpečnostní požadavky**

**Kritické požadavky ze specifikace MCP:**

> **NESMÍ**: MCP servery **NESMÍ** přijímat žádné tokeny, které nebyly výslovně vydány pro MCP server  
> 
> **MUSÍ**: MCP servery implementující autorizaci **MUSÍ** ověřovat VŠECHNY příchozí požadavky  
>  
> **NESMÍ**: MCP servery **NESMÍ** používat relace pro autentizaci  
>
> **MUSÍ**: MCP proxy servery používající statické ID klientů **MUSÍ** získat souhlas uživatele pro každého dynamicky registrovaného klienta  

---

## 1. **Bezpečnost tokenů a autentizace**

**Kontroly autentizace a autorizace:**
   - **Důkladná revize autorizace**: Provádějte komplexní audity logiky autorizace MCP serveru, abyste zajistili, že přístup k prostředkům mají pouze zamýšlení uživatelé a klienti  
   - **Integrace externího poskytovatele identity**: Používejte zavedené poskytovatele identity, jako je Microsoft Entra ID, místo implementace vlastní autentizace  
   - **Ověření cílového publika tokenů**: Vždy ověřujte, že tokeny byly výslovně vydány pro váš MCP server – nikdy nepřijímejte tokeny z jiných zdrojů  
   - **Správný životní cyklus tokenů**: Implementujte bezpečnou rotaci tokenů, politiky expirace a zabraňte útokům na opětovné použití tokenů  

**Chráněné úložiště tokenů:**
   - Používejte Azure Key Vault nebo podobná bezpečná úložiště pro všechny tajné klíče  
   - Implementujte šifrování tokenů jak v klidovém stavu, tak během přenosu  
   - Pravidelná rotace přihlašovacích údajů a monitorování neoprávněného přístupu  

## 2. **Správa relací a bezpečnost přenosu**

**Bezpečné praktiky pro relace:**
   - **Kryptograficky bezpečné ID relací**: Používejte bezpečná, nedeterministická ID relací generovaná pomocí bezpečných generátorů náhodných čísel  
   - **Vazba na konkrétního uživatele**: Vážte ID relací na identity uživatelů pomocí formátů jako `<user_id>:<session_id>`, abyste zabránili zneužití relací mezi uživateli  
   - **Správa životního cyklu relací**: Implementujte správnou expiraci, rotaci a zneplatnění relací pro omezení zranitelnosti  
   - **Vynucení HTTPS/TLS**: Povinné HTTPS pro veškerou komunikaci, aby se zabránilo zachycení ID relací  

**Bezpečnost transportní vrstvy:**
   - Konfigurujte TLS 1.3, pokud je to možné, s odpovídající správou certifikátů  
   - Implementujte připnutí certifikátů pro kritická spojení  
   - Pravidelná rotace certifikátů a ověřování jejich platnosti  

## 3. **Ochrana proti hrozbám specifickým pro AI** 🤖

**Obrana proti injekci promptů:**
   - **Microsoft Prompt Shields**: Nasazení AI Prompt Shields pro pokročilou detekci a filtrování škodlivých instrukcí  
   - **Sanitizace vstupů**: Ověřujte a čistěte všechny vstupy, abyste zabránili útokům injekcí a problémům zmateného zástupce  
   - **Obsahové hranice**: Používejte systémy oddělovačů a označování dat pro rozlišení mezi důvěryhodnými instrukcemi a externím obsahem  

**Prevence otravy nástrojů:**
   - **Ověření metadat nástrojů**: Implementujte kontroly integrity definic nástrojů a monitorujte neočekávané změny  
   - **Dynamické monitorování nástrojů**: Sledujte chování za běhu a nastavte upozornění na neočekávané vzory provádění  
   - **Schvalovací procesy**: Vyžadujte výslovné schválení uživatelem pro úpravy nástrojů a změny schopností  

## 4. **Řízení přístupu a oprávnění**

**Princip minimálních oprávnění:**
   - Udělujte MCP serverům pouze minimální oprávnění potřebná pro zamýšlenou funkčnost  
   - Implementujte řízení přístupu založené na rolích (RBAC) s jemně odstupňovanými oprávněními  
   - Pravidelné revize oprávnění a průběžné monitorování eskalace oprávnění  

**Kontroly oprávnění za běhu:**
   - Aplikujte limity zdrojů, abyste zabránili útokům na vyčerpání zdrojů  
   - Používejte izolaci kontejnerů pro prostředí nástrojů  
   - Implementujte přístup „just-in-time“ pro administrativní funkce  

## 5. **Bezpečnost obsahu a monitorování**

**Implementace bezpečnosti obsahu:**
   - **Integrace Azure Content Safety**: Používejte Azure Content Safety pro detekci škodlivého obsahu, pokusů o obejití pravidel a porušení politik  
   - **Analýza chování**: Implementujte monitorování chování za běhu pro detekci anomálií v MCP serveru a provádění nástrojů  
   - **Komplexní logování**: Logujte všechny pokusy o autentizaci, volání nástrojů a bezpečnostní události s bezpečným, nezměnitelným úložištěm  

**Průběžné monitorování:**
   - Upozornění v reálném čase na podezřelé vzory a pokusy o neoprávněný přístup  
   - Integrace se systémy SIEM pro centralizovanou správu bezpečnostních událostí  
   - Pravidelné bezpečnostní audity a penetrační testování implementací MCP  

## 6. **Bezpečnost dodavatelského řetězce**

**Ověření komponent:**
   - **Skenování závislostí**: Používejte automatizované skenování zranitelností pro všechny softwarové závislosti a AI komponenty  
   - **Ověření původu**: Ověřujte původ, licencování a integritu modelů, zdrojů dat a externích služeb  
   - **Podepsané balíčky**: Používejte kryptograficky podepsané balíčky a ověřujte podpisy před nasazením  

**Bezpečný vývojový proces:**
   - **GitHub Advanced Security**: Implementujte skenování tajných klíčů, analýzu závislostí a statickou analýzu CodeQL  
   - **Bezpečnost CI/CD**: Integrujte bezpečnostní validace do automatizovaných nasazovacích procesů  
   - **Integrita artefaktů**: Implementujte kryptografické ověřování nasazených artefaktů a konfigurací  

## 7. **Bezpečnost OAuth a prevence zmateného zástupce**

**Implementace OAuth 2.1:**
   - **Implementace PKCE**: Používejte Proof Key for Code Exchange (PKCE) pro všechny autorizační požadavky  
   - **Výslovný souhlas**: Získejte souhlas uživatele pro každého dynamicky registrovaného klienta, abyste zabránili útokům zmateného zástupce  
   - **Validace přesměrovacích URI**: Implementujte přísnou validaci přesměrovacích URI a identifikátorů klientů  

**Bezpečnost proxy:**
   - Zabraňte obcházení autorizace prostřednictvím zneužití statických ID klientů  
   - Implementujte správné pracovní postupy pro získání souhlasu pro přístup k API třetích stran  
   - Monitorujte krádeže autorizačních kódů a neoprávněný přístup k API  

## 8. **Reakce na incidenty a obnova**

**Schopnosti rychlé reakce:**
   - **Automatizovaná reakce**: Implementujte automatizované systémy pro rotaci přihlašovacích údajů a omezení hrozeb  
   - **Postupy pro návrat zpět**: Schopnost rychle se vrátit k ověřeným konfiguracím a komponentám  
   - **Forenzní schopnosti**: Detailní auditní stopy a logování pro vyšetřování incidentů  

**Komunikace a koordinace:**
   - Jasné postupy eskalace pro bezpečnostní incidenty  
   - Integrace s organizačními týmy pro reakci na incidenty  
   - Pravidelné simulace bezpečnostních incidentů a cvičení  

## 9. **Soulad a správa**

**Regulační soulad:**
   - Zajistěte, aby implementace MCP splňovaly požadavky specifické pro dané odvětví (GDPR, HIPAA, SOC 2)  
   - Implementujte klasifikaci dat a kontrolu ochrany soukromí pro zpracování dat AI  
   - Udržujte komplexní dokumentaci pro audity souladu  

**Řízení změn:**
   - Formální bezpečnostní revize všech změn systému MCP  
   - Řízení verzí a pracovní postupy schvalování pro změny konfigurace  
   - Pravidelné hodnocení souladu a analýza mezer  

## 10. **Pokročilé bezpečnostní kontroly**

**Architektura Zero Trust:**
   - **Nikdy nedůvěřuj, vždy ověřuj**: Průběžné ověřování uživatelů, zařízení a připojení  
   - **Mikrosegmentace**: Granulární síťové kontroly izolující jednotlivé komponenty MCP  
   - **Podmíněný přístup**: Kontroly přístupu založené na rizicích přizpůsobené aktuálnímu kontextu a chování  

**Ochrana aplikací za běhu:**
   - **Runtime Application Self-Protection (RASP)**: Nasazení technik RASP pro detekci hrozeb v reálném čase  
   - **Monitorování výkonu aplikací**: Monitorování výkonových anomálií, které mohou naznačovat útoky  
   - **Dynamické bezpečnostní politiky**: Implementace bezpečnostních politik, které se přizpůsobují aktuální hrozbě  

## 11. **Integrace s bezpečnostním ekosystémem Microsoftu**

**Komplexní bezpečnost Microsoftu:**
   - **Microsoft Defender for Cloud**: Správa bezpečnostního stavu cloudu pro pracovní zátěže MCP  
   - **Azure Sentinel**: Nativní cloudové SIEM a SOAR schopnosti pro pokročilou detekci hrozeb  
   - **Microsoft Purview**: Správa dat a soulad pro pracovní postupy AI a zdroje dat  

**Správa identity a přístupu:**
   - **Microsoft Entra ID**: Podniková správa identity s politikami podmíněného přístupu  
   - **Privileged Identity Management (PIM)**: Přístup „just-in-time“ a pracovní postupy schvalování pro administrativní funkce  
   - **Ochrana identity**: Podmíněný přístup založený na rizicích a automatizovaná reakce na hrozby  

## 12. **Průběžný vývoj bezpečnosti**

**Udržování aktuálnosti:**
   - **Monitorování specifikací**: Pravidelná revize aktualizací specifikací MCP a změn bezpečnostních pokynů  
   - **Zpravodajství o hrozbách**: Integrace zdrojů hrozeb specifických pro AI a indikátorů kompromitace  
   - **Zapojení do bezpečnostní komunity**: Aktivní účast v bezpečnostní komunitě MCP a programech pro oznamování zranitelností  

**Adaptivní bezpečnost:**
   - **Bezpečnost strojového učení**: Používání detekce anomálií založené na ML pro identifikaci nových vzorců útoků  
   - **Prediktivní bezpečnostní analýzy**: Implementace prediktivních modelů pro proaktivní identifikaci hrozeb  
   - **Automatizace bezpečnosti**: Automatizované aktualizace bezpečnostních politik na základě zpravodajství o hrozbách a změn specifikací  

---

## **Klíčové bezpečnostní zdroje**

### **Oficiální dokumentace MCP**
- [MCP Specifikace (2025-06-18)](https://spec.modelcontextprotocol.io/specification/2025-06-18/)  
- [MCP Bezpečnostní osvědčené postupy](https://modelcontextprotocol.io/specification/2025-06-18/basic/security_best_practices)  
- [MCP Specifikace autorizace](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)  

### **Bezpečnostní řešení Microsoftu**
- [Microsoft Prompt Shields](https://learn.microsoft.com/azure/ai-services/content-safety/concepts/jailbreak-detection)  
- [Azure Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/)  
- [Microsoft Entra ID Security](https://learn.microsoft.com/entra/identity-platform/secure-least-privileged-access)  
- [GitHub Advanced Security](https://github.com/security/advanced-security)  

### **Bezpečnostní standardy**
- [OAuth 2.0 Bezpečnostní osvědčené postupy (RFC 9700)](https://datatracker.ietf.org/doc/html/rfc9700)  
- [OWASP Top 10 pro velké jazykové modely](https://genai.owasp.org/)  
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)  

### **Implementační příručky**
- [Azure API Management MCP Authentication Gateway](https://techcommunity.microsoft.com/blog/integrationsonazureblog/azure-api-management-your-auth-gateway-for-mcp-servers/4402690)  
- [Microsoft Entra ID s MCP servery](https://den.dev/blog/mcp-server-auth-entra-id-session/)  

---

> **Bezpečnostní upozornění**: Bezpečnostní postupy MCP se rychle vyvíjejí. Vždy ověřujte podle aktuální [specifikace MCP](https://spec.modelcontextprotocol.io/) a [oficiální bezpečnostní dokumentace](https://modelcontextprotocol.io/specification/2025-06-18/basic/security_best_practices) před implementací.  

**Prohlášení:**  
Tento dokument byl přeložen pomocí služby pro automatický překlad [Co-op Translator](https://github.com/Azure/co-op-translator). Ačkoli se snažíme o přesnost, mějte prosím na paměti, že automatické překlady mohou obsahovat chyby nebo nepřesnosti. Původní dokument v jeho původním jazyce by měl být považován za autoritativní zdroj. Pro důležité informace se doporučuje profesionální lidský překlad. Neodpovídáme za žádná nedorozumění nebo nesprávné interpretace vyplývající z použití tohoto překladu.