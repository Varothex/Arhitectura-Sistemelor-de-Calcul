# MIPS
Pentru rezolvarea acestei probleme am folosit un sir alfabet (alf), cu scopul de a nu utiliza codul ASCII. Inițial citim numărul (n) și cele două șiruri. Verificăm dacă numărul este 2, caz tratat separat. Dacă nu este,verificăm să fie prim. Dacă nu este prim afișăm acest lucru și am ascăpat de treabă. Dacă este prim facem generatorul. Pentru a face generatorul punem de fiecare dată în vectorul „g” pe prima poziție 1 (adică numărul la puterea 0) și pe a doua poziție baza (adică puterea 1), pentru a nu lemai calcula de fiecare dată.  După ridicăm baza la mai multeputeri și punem de fiecare dată restul în „g”. Dacă restul este 1, verificăm să fie puterea cu numărul „n-1”. Dacă nu e, înseamnă că resturilese repetă și deci această bază nu poate foiizomorbismul,deci trecem la următoarea bază și repetăm procesul. Dacă este, înseamnă că vectorul „g” conține codurile necesare și deci trecem direct la codat. 
Pentru a coda, căutăm caracterul din șirul de codat în alf pentru a afla numărul lui. Odată aflat, mergem în g pe poziția contorului găsită anterior. Folosindu-ne de ce se află în g, mergem din nou în afl și afisăm noul caracter, reprezentând codul.
Pentru a decoda, căutăm caracterul din șirul de decodat in alf pentru a afla numărul lui. Odată aflat, căutăm inicele caracterului din alf în g, pentru  a afla noul cod. Cu noul cod ne întoarcem în alfși afișăm caracterul de pe poziția noului cod.

Exemple: 
7	=> Generatorul este: 3
ACAD	=> BCBG
BCBG	=> ACAD

2	=> Generatorul este: 1
A	=> B
B	=> A

19	=> Generatorul este: 2
ACAD	=> ACAD
BEBI	=> ACAD
