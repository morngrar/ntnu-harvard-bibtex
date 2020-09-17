# ntnu-harvard-bibtex

NTNU har på [sine sider](https://innsida.ntnu.no/wiki/-/wiki/Norsk/Bruke+og+referere+til+kilder) listet opp en guide for hvordan bruke sin variant av referansestilen harvard. Denne stilen er ikke standardisert i seg selv, men er en paraplybetegnelse som generelt omfatter såkalte *forfatter-år* stiler for kildehenvisning. Det er finnes imidlertid ingen tidligere eksisterende løsninger for å bruke akkurat denne varianten når man skriver i latex, hvor man ikke har måttet 'jukse til' entries i kildedatabasen for å få resultatet til å se rett ut, og selv da kommer man skjeldent i mål.

Denne bibtexstilen er et arbeid under utvikling for å bøte på dette. Og introduserer nye entrytyper som ikke er så generiske som det som er 'standard', men tilpasser den nå 30 år gamle bibtex teknologien til å fungere i et miljø hvor man gjerne vil kunne referere til digitale og nettbaserte verk.

**Merk:** Dette er en *bibtex* stil for bruk sammen med latex. Den fungerer ikke sammen med biblatex, men er ment å brukes sammen med natbib.

## Hvordan bruke denne stilen

Det antas at du som leser er noenlunde kjent med hvordan man legger kilder inn i en `.bib` fil. Om dette ikke er tilfelle, se [denne siden](https://www.latex-tutorial.com/tutorials/bibtex/) for en innføring i dette.

Denne stilen introduserer som nevnt egne entrytyper som ikke har vært med i bibtex originalt, og som heller ikke er brukt av det konkurrerende systemet *biblatex*. En full oversikt over disse finnes nederst i dette dokumentet.

### Velg språk
Denne stilen støtter norsk og engelsk, så langt. Og for å bruke den trenger du å kopiere to filer fra dette repoet til mappen hvor du har latexdokumentet ditt, men hvilke to dette er avhenger av hvilket språk du vil skrive på. 
- Norsk
    - `ntnu-harvard-no.bst` og `norskbst.tex`
- Engelsk
    - `ntnu-harvard-en.bst` og `englishbst.tex`

### Legg bibliografikommandoer til latex
I ditt dokuments hovedfil legger du til følgende i *preamblen* (før `\begin{document}`) for å bruke stilen:

    \usepackage{natbib}
    \bibliographystyle{ntnu-harvard-no}

Om du har valgt engelsk, skriv `ntnu-harvard-en` i stedet!

Og følgende helt mot slutten, rett før `\end{document}`:

    \bibliography{referanser}

Hvor `referanser` byttes ut med navnet på din `.bib` fil. **Merk at du ikke trenger å ha med filutvidelsen i filnavnet her**.

### Kompiler dokumentet
Eksemplet under er kommandoer du må kjøre for å kompilere et latexdokument som har navnet `main.tex`, under linux eller iOS. Samme kommandoer skal goså fungere på windows. Og man kan sette opp editorer eller IDE'er til å gjøre dette for seg, eller skrive kommandoene inn i en scriptfil og heller kjøre denne. Dollartegnet representerer kommandolinjens prompt, og er ikke en del av selve kommandoen.

    $ pdflatex main.tex
    $ bibtex main.aux
    $ pdflatex main.tex
    $ pdflatex main.tex

Grunnen til at man kjører `pdflatex` flere ganger er for å få alle kryssreferanser i siteringer og referanser til figurer, tabeller og utregninger med i den ferdige PDFen.


## Nye bibtex entry typer introdusert i denne stilen
Denne bibtexstilen fraviker med vilje etablerte 'standarder' for hvilke bibtex entry typer man skal bruke, og introduserer flere nye typer, for å være mer tilpasset eksemplene på [innsida](https://innsida.ntnu.no/wiki/-/wiki/Norsk/Bruke+referansestilen+Harvard).

De øvrige 'vanlige' entry typene som `book` og `incollection` skal også fungere som normalt. For en komplett oversikt over de originale entrytypene, se [denne siden](http://bib-it.sourceforge.net/help/fieldsAndEntryTypes.php).

Følgende er nye entrytyper introdusert med denne stilen:
- image
    - Brukes for å referere til bilder funnet på nettet jmf. eksempelet 'Digitalt bilde' på [ntnu.no](https://www.ntnu.no/viko/harvard-eksempler).

    - Har følgende støttede felter:
        - title
        - author
        - medium
            - Hva bildet er for noe, f.eks. 'digitalt foto' eller 'digitalt maleri'. Dersom det er et kunstverk som finnes ved et museum eller galleri, er ikke dette den rette entrytypen (i fremtiden vil det finnes en 'artwork' type for dette).
        - url
        - urldate
            - Dato nettressursen ble lastet ned

- video
    - Brukes for å referere til videoer funnet på nettet
    - Har følgende støttede felter:
        - title
        - author
        - url
        - urldate

- webarticle
    - Oppfører seg som 'article' men er tilpasset artikler fra nettet fremfor trykte tidsskrift. Kan brukes om enkeltstående nettartikler og blogginnlegg som har en forfatter. Se eksempelet eksempelet 'Nettside' på [ntnu.no](https://www.ntnu.no/viko/harvard-eksempler).

    - Har følgende støttede felter:
        - title
        - author
        - url
        - urldate

- website
    - Ment for å referere til nettsider. Funksjonelt et alias til `webarticle`.
    - Har følgende støttede felter:
        - title
        - author
        - url
        - urldate

### Entrytyper for verk uten forfatter
Noen av de nye entrytypene over har også fått varianter for tilfellet hvor det ikke er oppgitt en forfatter av verket. Generelt kan man da bare legge til `-noauthor` til entryen for å få rett formatering:

- image-noauthor
    - Ment for å referere til bilder hentet fra nettet hvor det ikke finnes en forfatter. I tilfelle det heller ikke er oppgitt noen tittel, bruk 'Uten tittel' som tittel.
    - Har følgende støttede felter:
        - title
        - author
        - medium
            - Hva bildet er for noe, f.eks. 'digitalt foto' eller 'digitalt maleri'. Dersom det er et kunstverk som finnes ved et museum eller galleri, er ikke dette den rette entrytypen (i fremtiden vil det finnes en 'artwork' type for dette).
        - url
        - urldate

- website-noauthor
    - Ment for å referere til nettsider hvor det ikke er oppgitt noen forfatter, og ingen organisasjon kan ansees som forfatter.
    - Har følgende støttede felter:
        - title
        - url
        - urldate

- wiki-noauthor
    - Ment for å referere til artikler uten forfatter i elektroniske oppslagsverk som f.eks. wikipedia eller store norske leksikon.
    - Har følgende støttede felter:
        - title
        - wikititle
            - Oppslagsverkets tittel
        - url
        - urldate

### Entrytyper for verk med organisasjon som forfatter
Noen av de nye entrytypene over har også fått varianter for tilfellet hvor forfatteren av verket må regnes som en organisasjon, eller navnet av annen grunn må oppgis i sin helhet. Generelt kan man da bare legge til `-organization` til entryen for å få rett formatering:

- image-organization
    - Ment for å referere til bilder hentet fra nettet hvor opphavspersonen må regnes som en organisasjon med tanke på referanseliste og sitering. 
    - Har følgende støttede felter:
        - title
        - author
        - medium
            - Hva bildet er for noe, f.eks. 'digitalt foto' eller 'digitalt maleri'. Dersom det er et kunstverk som finnes ved et museum eller galleri, er ikke dette den rette entrytypen (i fremtiden vil det finnes en 'artwork' type for dette).
        - url
        - urldate
- webarticle-organization
    - Har følgende støttede felter:
        - title
        - author
            - Navnet på organisasjon/entitet som regnes som forfatteren
        - url
        - urldate