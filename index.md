--- 
title: "De energietransitie doorgerekend"
subtitle: "Welke samenstelling van zon, wind en kernenergie levert een haalbare mix op?"
date: "Proefversie 2.1, 2022-04-15"
author: "P. Maas"
site: bookdown::bookdown_site
documentclass: book
description: Welke samenstelling van zon, wind en kernenergie levert een haalbare mix op?
link-citations: yes
github-repo: energiemix
url: energiemix.github.io
cover-image: DEDvoorkant.png
dev: "cairo_pdf"
indent: true
papersize: a4
fontsize: 11pt
geometry: margin=2cm # "inner=3cm,outer=1cm,top=2cm,bottom=2cm" # margin=2cm
urlcolor: CornflowerBlue # Black

---

<!-- \thispagestyle{empty} -->

<!-- Render PDF: -->
<!-- HOEFT NIET MEER: Ga naar 06-Simulaties en verander knitr_compile_formaat naar "latex" -->
<!-- verwijder 00-Toewijding.Rmd uit _bookdown.yml -->
<!-- bookdown::render_book("index.Rmd", "bookdown::pdf_book") -->

<!-- === VERSCHILLEN TUSSEN PRINT EN PDF === -->
<!-- 1. Truuk om endnotes te gebruiken ipv hyperlinks is gedefinieerd in preamble-latex.tex. -->
<!--    Daar dus aanpassen om document voor print of pdf klaar te stomen. -->
<!-- 1A.  En je moet een link na ieder hoofdstuk zetten waar de notes komen:  \theendnotes -->
<!-- 2. Pas geometry hierboven aan naar vaste marges voor PDF -->
<!-- 3. pas urlcolor aan naar black voor PRINT (footnotes), en blauw voor PDF -->

<!-- Render git_book: -->
<!-- Ga naar 06-Simulaties en verander knitr_compile_formaat naar "html" -->
<!-- bookdown::render_book() -->
<!-- Publiceren naar energiemix.github.io:
     cd energiemix.github.io
     git add --all
     git commit -m "beschrijf commit"
     git push -u origin main
-->

<!-- set site fonts en meer: https://rstudio4edu.github.io/rstudio4edu-book/book-fancy.html#book-font 
Karla, Lora
-->


# Aan de proeflezer {-}

Welkom! Dit project is een poging uit te vinden hoe de energietransitie er uit ziet, straks, als deze voltooid is. In principe zou er dan alleen nog CO~2~-vrij energie worden geproduceerd. Welke samenstelling van wind-, zon- en kernenergie levert een haalbare energiemix op? Wat werkt?

Dit project is onstaan uit een groepje geïnteresseerde mensen die zich afvroegen waar Nederland met de energietransitie op weg naar toe is. Een aantal daarvan hadden het fantastische boek van natuurkundeprof David MacKay -- [*Sustainable energy without the hot air*](https://www.withouthotair.com/download.html) -- gelezen en daaruit geleerd dat de meeste vormen van duurzame energie een lage energiedichtheid hebben. Tweederde van de  groene energie werd in Nederland in 2019 bijvoorbeeld nog opgewekt door verbranding van gewassen (o.a. houtsnippers). Gewassen hebben een bedroevend lage energiedichtheid en het leek uitgesloten dat we daarmee straks *net-zero* zouden bereiken. Waarom zetten we er dan op in?

Er lijkt niet echt een plan te zijn. Wat we niet konden ontdekken, in Nederland, maar ook in de rest van de rijke wereld, is met welke middelen we *net-zero* daadwerkelijk zouden kunnen bereiken. Dat is eigenlijk vreemd, want de transitie vervangt fossiele energiebronnen met een hoge energiedichtheid door duurzame bronnen die een lage dichtheid hebben. Nederland is een klein land, en veel ruimte heeft al een bestemming. Zouden we het redden met windmolens? Met zon? 

Het niet hebben van een plan kan grote gevolgen hebben. We mikken op ‘klimaatdoelen’ kennelijk onder andere door in te zetten op het verbranden van houtsnippers, maar dat kan niet de eindoplossing zijn (Bedenk dat Europa in de middeleeuwen ontbost raakte omdat voor koken, verwarming en industrie hout de enige brandstof was. Hoe zouden we dat nu met een veel hoger verbruik wel voor elkaar moeten krijgen?). Het behalen van een kleine reductie brengt ons niet bij *net-zero*. Zelfs het halen van een klimaatdoel brengt ons niet automatisch bij *net-zero*. Is investering in techniek waarmee het einddoel niet wordt gehaald dan eigenlijk wel een slimme zet? Kan dat geld niet beter worden ingezet voor techniek die toekomst heeft, die ons op lange termijn tot *net-zero* kan leiden? 

Langzaam kwam de realisatie dat schaal in de energietransitie belangrijk is. Het is onvoldoende een bron te selecteren enkel omdat deze duurzaam is. Kan de bron ook voldoende worden opgeschaald om er *net-zero* mee te bereiken? Het is belangrijk om na te denken over hoeveelheid, bijvoorbeeld hoeveel windmolens en zonnecellen er nodig zijn en waar je die neerzet.

Een tweede punt dat het groepje opviel is dat de twee opties waar nu voor wordt gekozen, zon en wind, lang niet altijd volop energie leveren. Wat doe je met windstilte? Opgevallen was dat vanaf eind september de zonnecellen op de boot niet meer voldoende waren om het verbruik te dekken en de accu’s vol te krijgen, waar dat in de zomer nog probleemloos lukte. In de winter was men afhankelijk van de walstroom. Hoe werkt dat eigenlijk op het niveau van Nederland, als een heel land permanent energie nodig heeft? 

Die vragen waren bij MacKay onderbelicht gebleven. Er wordt door hem kort gerekend aan de problematiek van uitval, maar niet voor de energiehuishouding van een heel land, voor een representatieve periode van vele jaren. Daarmee werd het huidige project eigenlijk geboren. Zou je dat voor Nederland kunnen schatten? Zou je kunnen schatten hoeveel extra molens je nodig zou hebben om uitval te voorkomen, of hoeveel accu’s je nodig zou hebben om energie in te kunnen opslaan? Het bleek dat de KNMI daar geweldige data voor heeft: zoninstraling en windsnelheid per tijdsvakken van tien minuten, en dat over de afgelopen tientallen jaren. Dat leverde een berg met data waar een schatting mee gemaakt kon worden. Er werd programmacode geschreven om het uit te rekenen. De conclusies die daaruit konden worden getrokken hebben hun weerslag gevonden in deze tekst.

Helaas is Knud Boucher, de andere geestelijke vader van dit project, niet meer onder ons. Hij had een zeldzaam breed blikveld die werd gecombineerd met een kritische houding zonder daarbij de welwillendheid te verliezen. Hij wilde echt een oplossing. Als je de energietransitie zou willen laten slagen, hoe doe je dat dan zonder dat daarbij fysieke grenzen overschreden worden? Wat zou een verstandige aanpak zijn?

Onze inzet, die van Knud en die van mij, was om onderzoek te doen naar de mogelijkheden, zonder daarbij te kiezen voor een bepaalde uitvoering. Dat wordt graag overgelaten aan de democratische besluitvorming. Sommigen willen geen kernenergie, anderen vinden windmolens lelijk. Dat moet ieder voor zich weten, en wij met z’n allen op een of andere manier zien te besluiten. De tekst wil wat dat betreft neutraal zijn. Het gaat ons om de randvoorwaarden bij een bepaalde energiemix. Daarvoor is er gerekend aan verschillende inrichtingen van een energiemix. Wij hoopten te leren welke inrichtingen haalbaar zijn. Met haalbaar wordt bedoeld: het bereiken van *net-zero*, zodanig dat Nederland zonder uitval van energie wordt voorzien. De insteek hier is om een eenvoudig rekenmodel te gebruiken om een schatting te maken van de schaal van de onderneming. Misschien geeft dat een indruk wat betere en wat minder goede oplossingen zijn.

Niet iedere duurzame energiebron wordt in het model meegenomen. Van de niet-continue energiebronnen leveren wind en zon het meeste op. Andere mogelijke bronnen zoals bijv. gewassen of aardwarmte werden minder zinvol geacht om mee te nemen wegens de lage opbrengst. De lezer wordt van harte aangeraden om MacKay er op na te slaan om zelf een indruk te krijgen van de potentie van verschillende energiebronnen. In tegenstelling tot dit stuk is MacKay vrij compleet.   Hetzelfde geldt voor opslagmethoden, waar er drie van worden bekeken (accu’s, spaarbekkens en waterstofopslag). Andere vormen zoals compressed air storage of ondergrondse opslagbekkens schalen slecht en worden minder zinvol geacht. Het kan natuurlijk zijn dat hierbij inschattingfouten zijn gemaakt en er een mooie vorm van opslag of energieopwekking  ten onrechte genegeerd is. Hopelijk kan een toekomstige versie van de tekst daar dan op worden aangepast.

Natuurlijk ben je als (proef)lezer van harte uitgenodigd te reageren. Ik zou vooral willen dat de tekst neutraal en betrouwbaar is. *Neutraal* in de zin dat er naar feiten wordt gekeken. Als de lezer ergens het gevoel krijgt dat er een keuze wordt opgedrongen, dan hoor ik het graag, want dat is niet de bedoeling. *Betrouwbaar* in de zin dat de tekst en conclusies afleidbaar zijn. Bronverantwoording voor de gebrachte feiten moet betrouwbaar zijn. Naast MacKay wordt Wikipedia vaak gebruikt als bron. Voor factuele zaken wordt Wikipedia betrouwbaar genoeg geacht. Het is in ieder geval een openbare bron die makkelijk verder te toetsen is. Mochten er bepaalde feiten niet kloppen, of er een betere bronvermelding mogelijk zijn, dan kan een toekomstige versie daarop worden aangepast. Ik zou het geweldig vinden als de gebruikte feiten en bronnen in dit verhaal steeds beter geborgd zouden worden. De programmacode van de gebruikte berekeningen moet nog openbaar op internet breikbaar worden gemaakt, zodat ook deze gecontroleerd kan worden. Ik zou graag nog een onafhankelijk controleur over de schouders mee laten kijken of alle berekeningen kloppen. Zou je dat willen doen of ken je iemand, dan houd ik me zeer aanbevolen.

Tot slot: vind je het onderwerp belangrijk en de tekst iets toevoegen, geef het dan door. Voor wie de printversie heeft gekregen: er is ook een elektronische versie beschikbaar die zich makkelijker laat verspreiden. 

\bigskip
\noindent
Dank voor het lezen!

\bigskip
\noindent
Pascal Maas,

\noindent
Januari 2022    
