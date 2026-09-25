---
name: kielelliset-oikeudet-ja-velvoitteet
description: > Use when this capability is needed.
metadata:
  author: akunikkola
---

# Kielelliset oikeudet ja velvoitteet — asiointikieli ja viranomaisen velvoitteet

Tämä skill jäsentää yksilön kielelliset oikeudet ja viranomaisen
kielelliset velvoitteet. Lähteet ja käsitteet:
`../oikeuskielen-kaantaminen/references/kaksikielisyys-perusteet.md`.

> **Vastuuvapaus:** arvio on tarkistettava luonnos — ei oikeudellista
> neuvontaa. Velvoitteet ja määräajat tarkistetaan kielilaista ja
> perustuslaista lähteestä. Saamen kieli on oma kokonaisuutensa. Katso
> `kaksikielisyys/CLAUDE.md`.

## Tarkista säännökset lähteestä

Hae kielilain (423/2003), perustuslain (731/1999) 17 §:n,
kielitaitolain (424/2003) ja tarvittaessa saamen kielilain (1086/2003)
säännökset **`juristi:oikeustutkimus`-skillillä**. Soveltamiskäytäntö
(mm. kielelliset oikeudet hallinto- ja tuomioistuinmenettelyssä)
lähteestä.

## Vaihe 1: Onko viranomainen kaksikielinen vai yksikielinen?

- **Kaksikielinen viranomainen** (esim. valtion viranomainen tai
  kaksikielinen kunta) palvelee molemmilla kansalliskielillä;
  **yksikielinen** pääosin yhdellä. Viranomaisen kielellinen asema
  vaikuttaa velvoitteiden laajuuteen.
- Selvitä viranomaisen asema ennen velvoitteiden arviointia — `[tarkista]`.

## Vaihe 2: Yksilön asiointikieli

1. **Oikeus omaan kieleen**: Suomen kansalaisella on oikeus käyttää
   omaa kieltään (suomi tai ruotsi) viranomaisessa perustuslain 17 §:n
   ja kielilain mukaisesti.
2. **Käytännön laajuus** (suullinen ja kirjallinen asiointi, tulkkaus,
   asiakirjan kieli) riippuu viranomaisen asemasta ja asiasta —
   tarkista lähteestä.
3. **Tuomioistuin- ja hallintomenettely**: oikeudenkäynnin ja
   hallintoasian käsittelykieli ja asianosaisen kielelliset oikeudet
   omine säännöksineen → kytkös `hallinto-oikeus` ja `riidanratkaisu`.

## Vaihe 3: Viranomaisen velvoitteet

- **Palvelu- ja tiedotusvelvoite** omalla kielellä (kaksikielisellä
  viranomaisella molemmilla).
- **Päätöksen ja toimituskirjan kieli**: millä kielellä päätös
  annetaan asianosaiselle; **käännös- ja tiedoksiantovelvollisuus**
  edellytyksineen — tarkista lähteestä.
- **Oma-aloitteinen kielellisten oikeuksien turvaaminen**: viranomaisen
  on huolehdittava oikeuksien toteutumisesta ilman, että yksilön
  tarvitsee erikseen vedota niihin.

## Vaihe 4: Henkilöstön kielitaito (424/2003)

- Julkisyhteisön henkilöstöltä vaadittava kielitaito ja sen
  osoittaminen; viran kelpoisuusvaatimukset kielitaidon osalta.
  Tarkista vaatimukset lähteestä.

## Vaihe 5: Saamen kieli (erikseen)

- **Saamen kielilaki 1086/2003** turvaa saamen kielen käytön omine
  edellytyksineen erityisesti saamelaisten kotiseutualueella. **Älä
  rinnasta saamen oikeuksia ruotsin kielen sääntelyyn** — käsittele
  erikseen ja ohjaa tarvittaessa erityissääntelyyn ja -viranomaisiin.

## Vaihe 6: Kokoava arvio

Esitä: viranomaisen kielellinen asema, yksilön asiointikieli ja sen
laajuus, viranomaisen käännös- ja tiedoksiantovelvoitteet sekä
mahdolliset puutteet ja korjaustoimet. Merkitse tulkinnanvaraiset
kohdat ja tarkistustarpeet.

## Mitä tämä skill EI tee

- **Ei esitä viranomaisen velvoitetta tai määräaikaa muistista** —
  kielilaista ja perustuslaista lähteestä.
- **Ei rinnasta saamen kieltä ruotsiin** — oma sääntelynsä.
- **Ei tuota virallista käännöstä** → `oikeuskielen-kaantaminen` ja
  auktorisoitu kääntäjä.
- **Ei ratkaise kielellisten oikeuksien loukkausta** — se voi edetä
  hallintomenettelyssä tai valvonnassa (mm. oikeusasiamies).

## Jatka tästä

- Asiakirjan tai termin kääntäminen FI↔SV → /kaksikielisyys:oikeuskielen-kaantaminen
- Päätöksen kieli ja muutoksenhaku hallintoasiassa → /hallinto-oikeus:muutoksenhaku
- Asiakirjajulkisuus ja tiedoksianto → /hallinto-oikeus:julkisuus-ja-tietopyynnot
- Säännöksen tarkistus → /juristi:oikeustutkimus

---
> Source: [akunikkola/claude-for-legal-finland](https://github.com/akunikkola/claude-for-legal-finland) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
