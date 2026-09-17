# BV Etiket — opdateringer

Her ligger programpakker og opdateringsmanifest til **BV Etiket**, et
internt printværktøj til EU-plantepasetiketter hos Blomsterverden.

Programmet på pakkestationen læser `opdatering.json` ved opstart og
henter selv en nyere udgave, hvis der er en.

## Hvad ligger her

| | |
|---|---|
| `opdatering.json` | Manifest: nyeste version, adresse på zip-filen og dens SHA-256. Adressen på denne fil står låst i programmets opsætning og må aldrig ændre sig. |
| Releases | `bv-etiket-app-<version>.zip` med programkoden. |

## Hvorfor er repoet offentligt

Pakkestationen skal kunne hente opdateringer uden at logge ind. Et
privat repo ville kræve et token på maskinen, som skulle fornys og
kunne lække.

Zip-filerne indeholder **udelukkende programkode** — `app/` og
`VERSION`. Der er aldrig produktdatabase, operatørnummer eller printlog
i dem. Udgivelsesscriptet afviser at pakke, hvis det finder datafiler.

Kildekoden med produktdata ligger privat i
[Blomsterverden/bv-etiket](https://github.com/Blomsterverden/bv-etiket).

## Sikkerhed

Den, der kan ændre indholdet her, kan afvikle kode på pakkestationen.
Skriveadgang skal derfor holdes stramt. Programmet kontrollerer
SHA-256 mod manifestet og afviser zip-filer med absolutte stier,
`..` eller symlinks, før noget installeres.

## Udgivelse

Fra kildekode-repoet:

```sh
./udgiv-opdatering.sh 1.2.0 "Kort beskrivelse"
```
