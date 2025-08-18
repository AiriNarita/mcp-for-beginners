<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "69ba3bd502bd743233137bac5539c08b",
  "translation_date": "2025-08-18T17:35:53+00:00",
  "source_file": "03-GettingStarted/05-sse-server/solution/python/README.md",
  "language_code": "it"
}
-->
# Eseguire questo esempio

Si consiglia di installare `uv`, ma non è obbligatorio. Consulta le [istruzioni](https://docs.astral.sh/uv/#highlights).

## -0- Crea un ambiente virtuale

```bash
python -m venv venv
```

## -1- Attiva l'ambiente virtuale

```bash
venv\Scrips\activate
```

## -2- Installa le dipendenze

```bash
pip install "mcp[cli]"
```

## -3- Esegui l'esempio

```bash
uvicorn server:app
```

## -4- Testa l'esempio

Con il server in esecuzione in un terminale, apri un altro terminale ed esegui il seguente comando:

```bash
mcp dev server.py
```

Questo avvierà un server web con un'interfaccia visiva che ti permetterà di testare l'esempio.

Una volta che il server è connesso:

- prova a elencare gli strumenti ed esegui `add`, con gli argomenti 2 e 4; dovresti vedere 6 come risultato.
- vai alle risorse e al modello di risorsa e chiama `get_greeting`, inserisci un nome e dovresti vedere un saluto con il nome che hai fornito.

### Testare in modalità CLI

L'inspector che hai avviato è in realtà un'app Node.js e `mcp dev` è un wrapper intorno ad essa.

Puoi avviarlo direttamente in modalità CLI eseguendo il seguente comando:

```bash
npx @modelcontextprotocol/inspector --cli http://localhost:8000/sse --method tools/list
```

Questo elencherà tutti gli strumenti disponibili nel server. Dovresti vedere il seguente output:

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

Per invocare uno strumento, digita:

```bash
npx @modelcontextprotocol/inspector --cli http://localhost:8000/sse --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

Dovresti vedere il seguente output:

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
> Di solito è molto più veloce eseguire l'inspector in modalità CLI rispetto al browser.
> Leggi di più sull'inspector [qui](https://github.com/modelcontextprotocol/inspector).

**Disclaimer**:  
Questo documento è stato tradotto utilizzando il servizio di traduzione automatica [Co-op Translator](https://github.com/Azure/co-op-translator). Sebbene ci impegniamo per garantire l'accuratezza, si prega di notare che le traduzioni automatiche possono contenere errori o imprecisioni. Il documento originale nella sua lingua nativa deve essere considerato la fonte autorevole. Per informazioni critiche, si consiglia una traduzione professionale eseguita da un traduttore umano. Non siamo responsabili per eventuali fraintendimenti o interpretazioni errate derivanti dall'uso di questa traduzione.