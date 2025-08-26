<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d26f746e21775c30b4d7ed97962b24df",
  "translation_date": "2025-08-18T16:14:31+00:00",
  "source_file": "03-GettingStarted/01-first-server/solution/python/README.md",
  "language_code": "fi"
}
-->
# Tämän esimerkin suorittaminen

Suosittelemme asentamaan `uv`, mutta se ei ole pakollista. Katso [ohjeet](https://docs.astral.sh/uv/#highlights)

## -0- Luo virtuaaliympäristö

```bash
python -m venv venv
```

## -1- Aktivoi virtuaaliympäristö

```bash
venv\Scripts\activate
```

## -2- Asenna riippuvuudet

```bash
pip install "mcp[cli]"
```

## -3- Suorita esimerkki

```bash
mcp run server.py
```

## -4- Testaa esimerkkiä

Kun palvelin on käynnissä yhdessä terminaalissa, avaa toinen terminaali ja suorita seuraava komento:

```bash
mcp dev server.py
```

Tämän pitäisi käynnistää verkkopalvelin, jossa on visuaalinen käyttöliittymä, jonka avulla voit testata esimerkkiä.

Kun palvelin on yhdistetty:

- kokeile listata työkalut ja suorita `add` argumenteilla 2 ja 4. Tuloksena pitäisi näkyä 6.

- siirry resurssit ja resurssimalli -osioon ja kutsu get_greeting. Kirjoita nimi, ja sinun pitäisi nähdä tervehdys antamallasi nimellä.

### Testaus CLI-tilassa

Ajamaasi tarkastustyökalua käytetään itse asiassa Node.js-sovelluksena, ja `mcp dev` on sen ympärille rakennettu käynnistysohjelma.

Voit käynnistää sen suoraan CLI-tilassa suorittamalla seuraavan komennon:

```bash
npx @modelcontextprotocol/inspector --cli mcp run server.py --method tools/list
```

Tämä listaa kaikki palvelimessa käytettävissä olevat työkalut. Sinun pitäisi nähdä seuraava tuloste:

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

Työkalun kutsumiseksi kirjoita:

```bash
npx @modelcontextprotocol/inspector --cli mcp run server.py --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

Sinun pitäisi nähdä seuraava tuloste:

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
> Tarkastustyökalun suorittaminen CLI-tilassa on yleensä paljon nopeampaa kuin selaimessa.  
> Lue lisää tarkastustyökalusta [täältä](https://github.com/modelcontextprotocol/inspector).  

**Vastuuvapauslauseke**:  
Tämä asiakirja on käännetty käyttämällä tekoälypohjaista käännöspalvelua [Co-op Translator](https://github.com/Azure/co-op-translator). Vaikka pyrimme tarkkuuteen, huomioithan, että automaattiset käännökset voivat sisältää virheitä tai epätarkkuuksia. Alkuperäinen asiakirja sen alkuperäisellä kielellä tulisi pitää ensisijaisena lähteenä. Kriittisen tiedon osalta suositellaan ammattimaista ihmiskäännöstä. Emme ole vastuussa väärinkäsityksistä tai virhetulkinnoista, jotka johtuvat tämän käännöksen käytöstä.