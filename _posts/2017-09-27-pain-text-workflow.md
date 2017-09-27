---
layout: post
title: Plain text workflow
date: 2017-09-27
---
A [doktori disszertációmat](https://zbereczki.github.io{{ site.baseurl }}/booklet/) [Scrivenerrel](https://www.literatureandlatte.com/scrivener.php) írtam, bibliográfiakezelőnek a [Zoterót](https://www.zotero.org) használtam, a végső szerkesztést pedig LibreOffice-ban csináltam. Összességében ez volt a munkafolyamatom:

[Using Scrivener for Writing Scientific Papers](https://danielvreeman.com/using-scrivener-for-writing-scientific-papers/)

Macerásan, de működött. Legjobban a LibreOffice-t utáltam benne, ezért (már a leadás után) elkezdtem utánaolvasni, hogy hogy hagyhatnám ki a folyamatból.

Így találtam rá erre a leírásra:

[Sustainable Authorship in Plain Text using Pandoc and Markdown](https://programminghistorian.org/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown)

Innen nem volt megállás, eldöntöttem, hogy nemcsak a LibreOffice-t, hanem a Scrivenert és úgy általában a word processorokat is magam mögött hagyom, és plain textre váltok.

A rendszer az alábbi elemekből áll:

- text editor
- bibliográfiakezelő
- konverter
- opcionális, de hasznos: markdown previewer

A kívánt workflow a következő:

- cikk (tanulmány, bármi) megírása markdownban, Zoteróból lábjegyzetbe beillesztett hivatkozásokkal
- markdownból .docx vagy .odt generálása tartalomjegyzékkel és megfelelően formázott hivatkozásokkal-bibliográfiával
- végső simítások elvégzése (ha szükséges), majd pdf mentése

A rendszer elemeinek tehát egymással is együtt kell működniük.

# Text editor

Szerkesztőnek a [BBEditet](https://www.barebones.com/products/bbedit/) választottam. Elvileg fizetős program, de van ingyenes változata is, ebben néhány funkció nem működik, de ezekre nekem nincs is szükségem. Nagy előnye, hogy ősrégi Macintosh-szoftver, így teljes mértékben Mac-like (aki Macet használ, tudja, mire gondolok). Fontos, hogy szkriptelhető, és nagyon hasznos még a syntax highlighting is.

## Navigálás a dokumentumban

A Scrivener nekem egy kicsit overkill volt. Amit valóban nagyon hasznosnak tartottam benne, az a Binder, ahol a dokumentum fejezetei és alfejezetei mappákként és fájlokként jelentek meg, így a navigálás nagyon egyszerű volt.

![A Binder a Scrivenerben]({{ site.baseurl }}/assets/Scrivener_Binder.png)

Ezt a funkcionalitást a BBEdit is tudja, valódi mappákkal és fájlokkal, így magában a Finderben hozhatom létre a hosszú dokumentumok alapstruktúráját.

![A „Project” sidebar a BBEditben]({{ site.baseurl }}/assets/BBEdit_Project.png)

Nyilván nem érdemes az összes al-alfejezetet külön fájlban tartani, ezt a tagolást már a fájlon belül Markdownban is megcsinálhatjuk. A BBedit `Functions`-menüje felismeri a Markdown fejezetcímeket, így a segítségével gyorsan lehet navigálni egy fájlon belül is.

![A BBEdit „Functions”-menüje]({{ site.baseurl }}/assets/BBEdit_functions.png)

## Szóba került még:

- [Atom](https://atom.io)
- [Sublime Text](https://www.sublimetext.com)
- [Ulysses](https://ulyssesapp.com)

# Bibliográfiakezelő

Ez maradt a [Zotero](https://www.zotero.org). Sajnos hivatalosan csak Word és LibreOffice-plugin létezik hozzá, de ez nem jelenti azt, hogy kis találékonysággal mással ne lehetne használni. Ehhez az alábbi segédprogramok kellenek.

## [Better BibTeX](https://github.com/retorquere/zotero-better-bibtex)

Ez egy Zotero-plugin, ami a Zoteróban tárolt egyes tételekhez [BibTeX](https://en.wikipedia.org/wiki/BibTeX)-kompatibilis [Citation Key](https://github.com/retorquere/zotero-better-bibtex/wiki/Citation-Keys)eket generál.

**Fontos: a legfrissebb, 5-ös Zoteróval egyelőre nem kompatibilis, de az újraírás már a [pre-release szakaszban](https://github.com/retorquere/zotero-better-bibtex/issues/555) van.**

A beállításoknál bekapcsoltam az `Automatic export` funkciót, így van a gépemen egy folyamatosan frissen tartott .bib-fájl (ami szintén plain text) a teljes Zotero-könyvtárammal. Mivel nagyon sok tétel van a Zoterómban, bekapcsoltam a `When idle`-kapcsolót is.

A `Citation keys` fülön pedig a `QuickCopy format`-ot állítsuk `Pandoc`-ra.

## [Zotpick-pandoc applescript](https://github.com/davepwsmith/zotpick-applescript)

Ez a kis segédprogram felhoz egy ugyanolyan választóablakot, mint a hivatalos LibreOffice/Word Zotero-pluginek, így nagyon egyszerű a hivatkozások beillesztése. Ha belemásoljuk a BBEdit `Scripts`-mappájába, akkor a BBEdit `Scripts`-menüjéből indíthatjuk.

![zotpick-pandoc]({{ site.baseurl }}/assets/zotpic-pandoc.png)

A kiválasztott tételről egy BibTeX cite keyt illeszt a dokumentumunkba. Ha lábjegyzetbe szeretnénk tenni, ezt a karaktert tegyük elé: `^`. Pl. `^@bereczki_reconstruction_2015`

# Konverter

Természetesen a [Pandoc](http://pandoc.org), ami a legkülönfélébb [markup-formátumok](http://pandoc.org/diagram.jpg) között tud parancssorból konvertálni. A [honlapról lehet letölteni](http://pandoc.org/installing.html) a telepítőt.

## YAML header

A Pandocnak szüksége van néhány alapadatra, amit a markdown-file elején az úgynevezett `YAML headser`-ben kell elhelyezni.

Egy alap YAML-header így néz ki:

````markdown
---
title: Plain Text Workflow
author: Bereczki Zoltán
date: 27.09.2017
bibliography: /Users/Zoli/Documents/tudomany/My_Library.bib
csl: /Users/Zoli/Documents/tudomany/csl/Z5.csl
---
````

A `bibliography` alatt a Better BibTeX által generált .bib-fájl elérési útját kell megadni, `csl`-nek pedig azt a Zotero-stílust, amit használni szeretnénk a hivatkozásaink és a bibliográfiánk formázásához.

## Tartalomjegyzék, bibliográfia, formázás

Ha azt szeretnénk, hogy a Pandoc a fájl elejére tartalomjegyzéket, a végére pedig bibliográfiát illesszen, a következők a teendők.

- tartalomjegyzék: konvertálásnál parancssorban használjuk a `—toc` kapcsolót
- bibliográfia: egyszerűen írjuk bele a markdown-fájlba a `Bibliography` szót oda, ahova a bibliográfiát tenni akarjuk; majd konvertálásnál használjuk a `--filter pandoc-citeproc` kapcsolót
- formázás: ha változtatni akarunk azon, ahogy a Pandoc formázza a szöveget, akkor a generált docx-ben állítsuk át a megfelelő stílusokat (tehát ne direkt formázást használjunk), majd adjuk meg a Pandocnak a fájlt referenciának az alábbi kapcsolóval: `--reference-docx=FILE`. ([LibreOffice-szal is működik](https://github.com/jgm/pandoc/wiki/Defining-custom-DOCX-styles-in-LibreOffice-(and-Word), de azt még nem próbáltam, lehet, hogy ott kicsit máshogy van).

## BBedit-script

A Pandoc használata lehetséges parancssor nélkül is. A BBEdithez léteznek Pandoc-szkriptek, én a [BBpandoc csomagból](https://github.com/jrgcmu/BBpandoc) a `pandoc-docx.sh`-t használom. Telepítés után beépül a BBEdit `Scripts`-menüjébe, így grafikus felületen tudok docx-et generálni. Én annyit változtattam rajta, hogy beleírtam a tartalomjegyzék és a bibliográfia generálására szolgáló kapcsolókat is, ez a verzió letölthető [innen](https://github.com/zBereczki/BBpandoc/blob/master/pandoc-docx.sh).

# Markdown previewer

Olyan kellett, ami a Pandocot használja megjelenítéshez. Szerencsére a BBEdit beépített previewere ilyen, de kell hozzá a [pandoc-preview.sh](https://github.com/jrgcmu/BBpandoc/blob/master/pandoc-preview.sh) script, ami szintén a BBpandoc része. Ha ez telepítve van, akkor a BBEdit preview-ablakának a tetején kiválaszthatjuk a `pandoc-preview.sh` filtert. Ennek azért van jelentősége, mert így a hivatkozásaink és a bibliográfiánk már formázva jelenik meg a preview-ban is. 

![saját csl alapján formázott bibliográfia a BBEdit előnézet-ablakában]({{ site.baseurl }}/assets/bibliografia.png)

A lábjegyzetek az előnézet legaljára fognak kerülni, de ezzel ne törődjünk, azért van, mert a BBEdit nem tördeli oldalakra az előnézetet. A generált docx-ben természetesen a helyükön lesznek a lábjegyzetek.

A BBEditnek az előnézet generálásához saját ccs-t is meg lehet adni. Nekem erre azért volt szükségem, mert egyébként a képeket teljes méretben teszi be, nem oldalszélességben. A Marked 2-höz van sok [custom style](https://github.com/ttscoff/MarkedCustomStyles), ezeket BBEditben is használhatjuk. Hogy a képek oldalszélesek legyenek, írjuk bele a használt css-be ezt (ha nem lenne benne alapból):

````css
  img {
    max-width: 100%;
  }
````

## Szóba került még:

- [Atom](https://atom.io)
- [Marked 2](http://marked2app.com)
