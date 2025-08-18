<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d26f746e21775c30b4d7ed97962b24df",
  "translation_date": "2025-08-18T15:45:49+00:00",
  "source_file": "03-GettingStarted/01-first-server/solution/python/README.md",
  "language_code": "no"
}
-->
# Kjøre dette eksempelet

Det anbefales å installere `uv`, men det er ikke et krav. Se [instruksjoner](https://docs.astral.sh/uv/#highlights)

## -0- Opprett et virtuelt miljø

```bash
python -m venv venv
```

## -1- Aktiver det virtuelle miljøet

```bash
venv\Scripts\activate
```

## -2- Installer avhengighetene

```bash
pip install "mcp[cli]"
```

## -3- Kjør eksempelet

```bash
mcp run server.py
```

## -4- Test eksempelet

Med serveren kjørende i én terminal, åpne en annen terminal og kjør følgende kommando:

```bash
mcp dev server.py
```

Dette skal starte en webserver med et visuelt grensesnitt som lar deg teste eksempelet.

Når serveren er tilkoblet:

- Prøv å liste opp verktøyene og kjør `add` med argumentene 2 og 4. Du bør se 6 som resultat.

- Gå til ressurser og ressursmal, og kall `get_greeting`. Skriv inn et navn, og du bør se en hilsen med navnet du oppga.

### Testing i CLI-modus

Inspektøren du kjørte er faktisk en Node.js-app, og `mcp dev` er en wrapper rundt den.

Du kan starte den direkte i CLI-modus ved å kjøre følgende kommando:

```bash
npx @modelcontextprotocol/inspector --cli mcp run server.py --method tools/list
```

Dette vil liste opp alle verktøyene som er tilgjengelige på serveren. Du bør se følgende utdata:

```text
{
  "tools": [
    {
      "name": "add",
      "description": "Add two numbers",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "title": "A",
            "type": "integer"
          },
          "b": {
            "title": "B",
            "type": "integer"
          }
        },
        "required": [
          "a",
          "b"
        ],
        "title": "addArguments"
      }
    }
  ]
}
```

For å bruke et verktøy, skriv:

```bash
npx @modelcontextprotocol/inspector --cli mcp run server.py --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

Du bør se følgende utdata:

```text
{
  "content": [
    {
      "type": "text",
      "text": "3"
    }
  ],
  "isError": false
}
```

> [!TIP]
> Det er vanligvis mye raskere å kjøre inspektøren i CLI-modus enn i nettleseren.
> Les mer om inspektøren [her](https://github.com/modelcontextprotocol/inspector).

**Ansvarsfraskrivelse**:  
Dette dokumentet er oversatt ved hjelp av AI-oversettelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selv om vi tilstreber nøyaktighet, vennligst vær oppmerksom på at automatiske oversettelser kan inneholde feil eller unøyaktigheter. Det originale dokumentet på sitt opprinnelige språk bør anses som den autoritative kilden. For kritisk informasjon anbefales profesjonell menneskelig oversettelse. Vi er ikke ansvarlige for eventuelle misforståelser eller feiltolkninger som oppstår ved bruk av denne oversettelsen.