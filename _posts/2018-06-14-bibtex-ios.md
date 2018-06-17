---
layout: post
title: BibTeX iOS-en
date: 2018-06-14
---
A [plain text workflow-mat](https://zbereczki.github.io/blog/2017/09/27/plain-text-workflow.html) a bejegyzés megírása óta továbbfejlesztettem olyan módon, hogy már a bibliográfiai adatbázisom is plain textben van, ehhez a [BibDesket](https://bibdesk.sourceforge.io) használom. Majd fogok is erről egy bejegyzést írni, de a lényeg az, hogy ez talán a legfontosabb fájlom a kutatásaim szempontjából: minden elolvasott szakirodalom bibliográfiai adatai ebben vannak, és a saját kapcsolódó jegyzeteim is. Jelenleg ez 971 tételt jelent. A [Zoteróban](https://www.zotero.org) mindig zavart, hogy ezek az értékes, pótolhatatlan adatok egy adatbázis mélyén vannak.

A BibDesk ebből a szempontból sokkal jobb: az egész bibliográfiai adatbázisom (jegyzetekkel együtt) egyetlen 984 KB-os plain text fájl `.bib` kiterjesztéssel.

Nagyon jó lenne, ha telefonon is tudnám használni, főleg az egyes tételekhez kapcsolódó jegyzetek miatt, de jelenleg ez nem tűnik megoldhatónak. Annak ellenére, hogy az adatbázis egy egyszerű szövegfájl, nincs olyan kliens iOS-re, amivel egyszerűen lehetne böngészni. Arra már nem is vágyom, hogy telefonon is szerkeszteni tudjam, beérném a böngészéssel is.

Jelenleg ezek a megoldások vannak:

- [iBibTeX](https://itunes.apple.com/US/app/id924874217?mt=8): ez elvileg azt tudja, amire szükségem van, de régen volt frissítve, így a Google Drive már nem hajlandó működni vele (403 disallowed_useragent), mással meg nem szinkronizál.
- [Papers 3](https://itunes.apple.com/app/papers-3-for-ios/id700959105?mt=8&ign-mpt=uo%3D4): tud iCloudban (vagy bárhol) tárolt .bib-fájlt importálni, de minden változtatásnál újra kellene importálnom az egészet.
- [Mendeley](https://itunes.apple.com/gb/app/mendeley-reference-manager/id380669300?mt=8): ugyanaz, csak még egy extra lépéssel: először a Mendeley Desktoppal kell importálni a .bib-fájlt, ez szinkronizálja az adatbázist a szerverrel, és így lesz elérhető a dolog iOS-en. Felesleges túlbonyolítás. A Mendeley ráadásul a [közellenség](https://444.hu/2016/12/22/fellazadtak-a-nemet-egyetemek-es-konyvtarak-a-szabad-tudasert) Elsevier tulajdona.
- A purista megoldás: lementem időnként a .bib-fájlt iCloudba, megváltoztatom a kiterjesztést .txt-re, és iPhone-on megnyitom bármilyen text editorral. Böngészni a fájlt így nyilván nem lehet, de a keresés működik, ha lassan is.

Nem akarja valaki portolni a BibDesket iOS-re? Elvileg [lehetséges](https://sourceforge.net/p/bibdesk/wiki/BibDesk_iOS/).

# Frissítés:

A purista megoldás mellett maradtam. Így működik most a dolog:

- A library.bib-et a Dropboxomba költöztettem, így mindig up to date a telefonomon is.
- A telefonon csináltam egy [workflow-t](https://workflow.is), ami azt csinálja, hogy amikor elindítom, készít egy másolatot a library.bib-ről library-*aktuális dátum*.txt néven, és megnyitja a 1Writerben. Így egyrészt nem kézzel kell átnevezgetnem (a .bib-et nem hajlandó a 1Writer megnyitni), másrészt az eredeti fájlom érintetlen marad. A workflow-t a home screenről tudom indítani.
