Steps

1. Import 
Zie Evernote
- line based, zodat alles in 1 column staat, en ik stap voor stap eruit kan halen
- encode UTF-8, best voor text (en anders extra tekens in tekst, waardoor je niet kan filteren) 

2. fix first column replace(/\uF04A/, "#XX") [script](https://github.com/emcoding/openrefinescripts/blob/4415558ffef1123ee20849f74339ccd13ac1f0db/replace_with_XX.json)

3. Verplaats In-bezit? (#ja, #ne, #xx) naar nieuwe column: eerst nieuwe kolom op basis van oude, #NE #NEEdan text weg uit oude.

# Eerst kolom hernoemen naar 'source' field, 
dan kun je gemakkelijk scripts hergebruiken. 

# ISBN
- facet: zet flag op rij (niet record) met woord "ISBN"
- extract column with regex `value.find(/ISBN\s?[\d -\/]*X?/i)[0])` = ISBN +/- spatie; dan een combinatie van cijfers, - en /; al dan niet afgesloten met een x/X
- Niet alles goed overgekomen, les 1: eerst opschonen, dan massa-handelingen 
- Wat kan misgaan met ISBN: spaties of / ipv -, 13 en x/X 
- Eerst alle afwijkingen gestarred. Veel werk, onhandig. Dan regex gebruikt om afwijkingen te zoeken. Enkele kun je inline editen.
- BETER: 
- [ ]  gebruik de regex. 
- [ ]  remove "ISBN" uit nieuwe column . (en normaliseren: toUpperCase om x=> X, chomp("."), ) 
- [ ]  (opt)Fix naar standaardformaat dat jullie gebruiken. bijv punctutaion verwijderen. maar deze verfijningnen doe je liever aan het eind  
- [ ]  [permalink tot hier](http://localhost:3333/project?project=1830991407554&ui=%7B%22facets%22%3A%5B%7B%22c%22%3A%7B%22type%22%3A%22list%22%2C%22name%22%3A%22Flagged%20Rows%22%2C%22columnName%22%3A%22%22%2C%22expression%22%3A%22row.flagged%22%2C%22omitBlank%22%3Afalse%2C%22omitError%22%3Afalse%2C%22selectBlank%22%3Afalse%2C%22selectError%22%3Afalse%2C%22invert%22%3Afalse%7D%2C%22o%22%3A%7B%22scroll%22%3Afalse%2C%22sort%22%3A%22name%22%7D%2C%22s%22%3A%5B%7B%22v%22%3A%7B%22v%22%3Atrue%2C%22l%22%3A%22true%22%7D%7D%5D%7D%5D%7D)
- [ ]  vind  afwijkingen:
  - [ ]  Gebruik dezelfde regex om ISBN uit oude te verwijderen. maar replace met terugvindcode, bijv &weg& (niet $) `value.replace(/ISBN\s?[\d -\/]*X?/, "&weg&")`  
  - [ ]  Fix enkele handmatig + ! remove uit oude column! want regex vindt hem dus niet goed. 
- 
- In welk formaat slaan jullie ISBN op? 
- Opschonen: 
- 
- [Oude ](http://localhost:3333/project?project=1830991407554&ui=%7B%22facets%22%3A%5B%7B%22c%22%3A%7B%22type%22%3A%22list%22%2C%22name%22%3A%22Flagged%20Rows%22%2C%22columnName%22%3A%22%22%2C%22expression%22%3A%22row.flagged%22%2C%22omitBlank%22%3Afalse%2C%22omitError%22%3Afalse%2C%22selectBlank%22%3Afalse%2C%22selectError%22%3Afalse%2C%22invert%22%3Afalse%7D%2C%22o%22%3A%7B%22scroll%22%3Afalse%2C%22sort%22%3A%22name%22%7D%2C%22s%22%3A%5B%7B%22v%22%3A%7B%22v%22%3Atrue%2C%22l%22%3A%22true%22%7D%7D%5D%7D%5D%7D)

