CIUREA ROBERT-MIHAI 313CB
                        
                        The Emperor's New Sudoku

    Task1:

Scopul Task-ului 1 il constituie citirea unui fisier JSON, iar pe baza
datelor retinute din fiecare fisier in parte, construirea unei imagini BMP
care constituie un joc de sudoku complet sau partial completat. Pentru a putea
utiliza informatiile din fisierele JSON, a fost nevoie de introducerea unui
header specific, respectiv cJSON.h. Am ales utilizarea acestuia intrucat ne-a
fost recomandat, iar documentatia acestuia a fost extrem de concludenta, astfel
ca am avut acces la o multitudine de functii care sa ma ajute la parsarea,
obtinerea si prelucrarea informatiie. Pentru salvarea bitmap-ului, am ales
salvarea acestora intr-un array pentru a-mi fi mai usor sa le scriu ulterior
in fisierul BMP pentru a forma imaginea. Structurile file_header, respectiv
info_header au putut fi scrise in fisier in exact in ordinea in care au fost
citite, insa pentru bitmap a fost nevoie sa ma folosesc de un pointer al carui
scop il constituie crearea imaginii propriu-zise linie cu linie, tinand cont de
padding. Pentru ca scrierea sa nu fie eronata, specificam ca fiecare linie sa
constina cata 220 numere, primele 219 numere reprezentand componentele pixelilor
utilizati, iar ultimulm numar reprezentand padding-ul.

    Task2:

Scopul Task-ului 2 il constituie reconstruirea imaginii initiale, tinand cont
de faptul ca de aceasta data nmumerele trebuie scrise corect, nu in oglinda.
Pentru a fi posibil asa ceva au fost necesare prelucrari la nivelul bitmap-ului.
Tinand cont de faptul ca elementele bitmap-ului au fost stocate intr-un vector,
a fost necesara o formula pentru a ajunge la elementele menite sa fie modificate.
Am constatat ca daca am analiza o matrice de 5x15 ce reprezinta totalitatea
numerelor ce formeaza pixelii necesari pentru un numar, se observa faptul ca daca
se inverseaza primele 3 numere cu ultimele 3 numere, respectiv urmatorul set de 3
numere cu penultimul set de numere, are loc si rescierea numarului pentru a arata
corespunzator. Acest lucru este posibil intrucat de fapt se face inversarea
pixelilor de culoare, tinand cont de faptul ca avand numar impar de pixeli pe o
linie, setul din mijloc ramane identic, fata de el facandu-se simetria.

    Task3:

Scopul Task-ului 3 il constituie analizarea board-ului creat la task-ul
precedent si indicarea intr-un fisier JSON daca board-ul este unul castigator
sau nu. Pentru a face aceasta constatare a fost necesar analizarea board-ului
pentru a stabili daca are sau nu spatii goale, respectiv observarea pentru
board-urile complete daca se repete vreun numar pe o linie, coloana sau in
interiorul unui patrat de 9x9 delimitat de liniile negre de marginire.
Pentru a analiza daca board-ul are casute albe sau nu, a fost suficient
identificarea unei singure linii din componenta unei casute de 5x15 care
reprezinta pixelii pentru formarea unui numar. Astfel ca daca o linie avea 15
succesiune de valori de 255, acest lucru inseamna ca se aflau 5 pixeli albi ce
formau o linie complet alba, criteriu incompatibil cu orice alt caz in care in
acea casuta s-ar fi aflat vreun numar. Daca se constata ca exista un spatiu gol,
acest lucru ducea implicit la pierderea jocului. Mai departe, daca board-ul
totusi este complet, pentru analiza liniilor, coloanelor si a matricilor de 9x9
am creat o masca care retine toate numerele din board, masca stocand totalitatea
numerelor din board, tinand cont ca fiecare succesiune de 9 numere reprezinta
cate o coloana din board. Am constat ca fiecare numar are un pattern specific
ce a dus la construirea in board a imaginii numerelor. Acest pattern consta in
analiza unor pixeli ce au dus la identificarea exacta a numerelor. La numerele
1, 4, 7, 8 a fost relativ usor identificarea numerelor pe baza numararii
pixelilor intrucat acestea au avut numere diferite de pixeli. Insa numerele
2, 3, 5; resppectiv 6, 9 aveau fiecare grupare acelas numar de pixeli, astfel
ca a fost necesara analiza pozitiilor anumitor pixeli din cauta pentru a stabili
 ce numar respectiv se afla acolo. La final, daca se repetau 2 numere, jocul era
 pierdut, in caz contrar jocul era unul castigator, iar in fisierul JSON s-a
 scris output-ul aferent cazului.

    Task4:
    
Task4 consta in primirea ca input a unui fisier BMP astfel incat acesta sa
fie completat cu numerele necesare pentru ca board-ul sa fie unul catsigator.
Pentru acest lucru ne-am utilizat din nou de masca, insa de aceasta data am
utilizat o matrice patratica de 9x9 in care am retinut toate numerele din board,
iar daca nu se afla nici un numar in board, masca era completata cu valoarea 0
pentru ca ulterior sa se completeze cu numarul necesar. Pentru a completa
board-ul, luam fiecare spatiu gol si introducem in acesta cate un numar de la
1 la 9, pe care il comparam cu toate elementele de pe linia, coloana, respectiv
patratul de 3x3 din care face parte. Odata ce completam intreaga matrice,
urmeaza modificarea in bitmap a numerelor ce compun pixelii necesari colorarii
spatiilor goale pentru a forma numerele aferente. Pentru acest lucru a fost
necesara o formula ce tine cont de fiecare linie din board, iar fiecare numar
are o colorare specifica a pixelilor in functie de linia ce urmeaza a fi
completata