---
name: oikeuskielen-kaantaminen
description: > Use when this capability is needed.
metadata:
  author: akunikkola
---

# Oikeuskielen kääntäminen — FI↔SV vakiintunein termein

Tämä skill tukee juridisen tekstin kääntämistä suomen ja ruotsin välillä
niin, että oikeudellinen merkitys säilyy. Termistö ja viralliset lähteet:
`references/kaksikielisyys-perusteet.md` — lue se tehtävän alussa.

> **Vastuuvapaus:** käännös on tarkistettava luonnos — ei oikeudellista
> neuvontaa eikä virallinen käännös. Virallisen käännöksen tekee
> auktorisoitu kääntäjä. **Älä keksi termiä — käytä vakiintunutta
> vastinetta lähteestä.** Katso `kaksikielisyys/CLAUDE.md`.

## Tarkista termit ja säädösnimet lähteestä

Säädöksen **virallinen ruotsinkielinen nimi ja sanamuoto** Finlexin
rinnakkaistekstistä (`juristi:oikeustutkimus`). Termien vakiintuneet
vastineet valtioneuvoston termipankista (Valter), Sanastokeskuksen
TEPA:sta ja Kotuksen ohjeista. Älä esitä keksittyä tai sanasanaista
vastinetta varmana.

## Vaihe 1: Tekstilaji ja tarkoitus

- **Mikä teksti** (sopimus, päätös, kirjelmä, säädössitaatti, markkinointi)
  ja **mihin käyttöön** (virallinen vai sisäinen, viranomaiselle vai
  asiakkaalle)? Virallinen tai oikeudessa käytettävä käännös → ohjaa
  auktorisoidulle kääntäjälle; tämä skill tukee valmistelua ja tarkistusta.
- Tunnista käännössuunta ja kohdeyleisön kielitaso.

## Vaihe 2: Säädös- ja viranomaisnimet ensin

- Hae jokaisen viitatun **säädöksen virallinen ruotsinkielinen nimi**
  Finlexistä (rinnakkaisteksti) — älä käännä nimeä itse.
- **Tuomioistuinten ja viranomaisten nimet** vakiintuneessa muodossa
  (ks. referenssin termitaulukko); ratkaisulyhenteet (KKO/HD, KHO/HFD).
- Säilytä säädösnumero ja pykäläviittaus muuttumattomana molemmilla
  kielillä.

## Vaihe 3: Termivastineet

1. **Tunnista oikeustermit** lähtötekstistä (käsitteet, joilla on
   määritelty oikeudellinen merkitys).
2. **Hae kullekin vakiintunut vastine** virallisesta termilähteestä.
   Esimerkkejä vakiintuneista vastineista on referenssin taulukossa.
3. **Merkitse epävarmat** `[vastine varmistettava]` äläkä esitä
   keksittyä termiä. Sama suomen termi voi saada eri vastineen
   asiayhteyden mukaan — varmista konteksti.
4. **Vältä kavereita ja sanasanaisuutta** — käännä käsite, ei sana.

## Vaihe 4: Rakenne ja kielenhuolto

- Noudata kohdekielen oikeuskielen konventioita (lauserakenne,
  passiivin käyttö, yhdyssanat). Suomen kielen tarkistus →
  `juristi:suomen-kieli`; ruotsin osalta nojaa virallisiin ruotsin
  kielenhuolto-ohjeisiin (Kotus / statsrådets svenska språknämnd).
- Pidä numerot, päivämäärät ja viittausmuodot kohdekielen mukaisina.

## Vaihe 5: Kaksikielinen asiakirja

- Kun sama asiakirja laaditaan kahdella kielellä, varmista, että
  **molemmat versiot vastaavat oikeudellisesti toisiaan**; merkitse,
  kumpi on alkuperäinen tai ratkaiseva, jos sopimukseen otetaan
  kieliehto.
- Olemassa olevan asiakirjan käännösehdotukset voi tehdä Adeu-MCP:llä
  jälkimuutoksina (Track Changes).

## Vaihe 6: Tarkistuslista

Termivastineet lähteestä ✓ · säädösnimet Finlexin rinnakkaistekstistä ✓
· epävarmat merkitty `[vastine varmistettava]` ✓ · merkitys säilynyt
(ei sanasanaisuutta) ✓ · virallista käyttöä varten auktorisoitu kääntäjä ✓.

## Mitä tämä skill EI tee

- **Ei tuota virallista tai oikeudessa pätevää käännöstä** — se on
  auktorisoidun kääntäjän tehtävä.
- **Ei keksi termivastineita** — vakiintunut vastine lähteestä tai
  `[vastine varmistettava]`.
- **Ei käännä säädöksen nimeä itse** — virallinen nimi Finlexistä.
- **Ei käsittele saamen kieltä ruotsin tapaan** → omat oikeutensa.

## Jatka tästä

- Viranomaisen kielelliset velvoitteet ja asiointikieli → /kaksikielisyys:kielelliset-oikeudet-ja-velvoitteet
- Suomenkielisen tekstin oikeinkirjoitus ja tyyli → /juristi:suomen-kieli
- Säädöksen ruotsinkielisen nimen ja tekstin tarkistus → /juristi:oikeustutkimus

---
> Source: [akunikkola/claude-for-legal-finland](https://github.com/akunikkola/claude-for-legal-finland) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
