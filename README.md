![Coders-Lab-1920px-no-background](https://user-images.githubusercontent.com/30623667/104709387-2b7ac180-571f-11eb-9b94-517aa6d501c9.png)

# Kilka ważnych informacji

Przed przystąpieniem do rozwiązywania zadań przeczytaj poniższe wskazówki

## Jak zacząć?

1. Stwórz [*fork*](https://guides.github.com/activities/forking/) repozytorium z zadaniami.
2. Sklonuj fork repozytorium (stworzony w punkcie 1) na swój komputer. Użyj do tego komendy `git clone adres_repozytorium`
Adres możesz znaleźć na stronie forka repozytorium po naciśnięciu w guzik "Clone or download".
3. Rozwiąż zadania i skomituj zmiany do swojego repozytorium. Użyj do tego komend `git add nazwa_pliku`.
Jeżeli chcesz dodać wszystkie zmienione pliki użyj `git add .` 
Pamiętaj że kropka na końcu jest ważna!
Następnie skommituj zmiany komendą `git commit -m "nazwa_commita"`
4. Wypchnij zmiany do swojego repozytorium na GitHubie.  Użyj do tego komendy `git push origin master`
5. Stwórz [*pull request*](https://help.github.com/articles/creating-a-pull-request) do oryginalnego repozytorium, gdy skończysz wszystkie zadania.

Poszczególne zadania rozwiązuj w odpowiednich plikach.

### Poszczególne zadania rozwiązuj w odpowiednich plikach.

**Repozytorium z ćwiczeniami zostanie usunięte 2 tygodnie po zakończeniu kursu. Spowoduje to też usunięcie wszystkich forków, które są zrobione z tego repozytorium.**


# Egzamin &ndash; Zadanie  &ndash; menu (2pkt)

Dodaj widok strony głównej (pusty adres **URL**).
Powinien on zawierać listę linków do poszczególnych stron w aplikacji:
* "Pierwszy wykład" &ndash; `/lecture_details/1/`,
* "Zapisz mnie" &ndash; `/set_username/<twoje imię>/`,
* "Przywitaj mnie" &ndash; `/say_hello/`,
* "Przywitaj mnie 5 razy" &ndash; `/say_hello/5/`,
* "Upiecz ciastko" &ndash; `/create_cookie/cookie/cookie/10/`,
* "Zjedz ciastko" &ndash; `/delete_cookie/cookie/`,
* "Dodaj studenta" &ndash; `/add_student/`.

Poszczególne strony stworzymy w kolejnych zadaniach. Na tę chwilę, będą one prowadzić 
do stron, które nie istnieją. Widok ten, przyda Ci się do testowania kolejnych zadań.  

# Egzamin &ndash; Zadanie 2 &ndash; modele (4pkt)

Napisz następujące modele:

* **Student**, a w nim następujące właściwości:
    * `name`: string, max. 64 znaki, imię powinno być unikalne
    * `year_at_university`: integer,
    * `is_active`: boolean, standardowa wartość `True`,

* **Lecture**, a w nim następujące właściwości:
    * `name`: string, max 64 znaki, imię powinno być unikalne,
    * `lecturer`: string, max. 64 znaki.

Połącz oba modele taką relacją, aby każdy student mógł brać udział w wielu wykładach, 
a w każdym wykładzie mogło brać udział wielu studentów. 
Relacja musi być założona bez dodatkowych danych (**nie** używaj argumentu `through`) oraz ma być zaczepiona w modelu 
`Lecture`. Pole powinno mieć nazwę `students`.
Pamiętaj o wykonaniu migracji!



# Egzamin &ndash; Zadanie 3 &ndash; szczegóły wykładu (3pkt)

Napisz widok, który udostępnisz pod adresem `/lecture_details/{id}/`, gdzie {id} to numer id (klucz główny, liczba) 
danego wykładu. Widok ma wyświetlać na ekranie następujące dane:

* nazwa wykładu (pole `name` z modelu),
* nazwisko wykładowcy (pole `lecturer` z modelu),
* listę studentów biorących w nim udział (wystarczą same imiona).





# Egzamin &ndash; Zadanie 4 &ndash; widoki (6pkt)

Napisz widoki do poszczególnych adresów **URL**:

* `/set_username/{user_name}` &ndash; widok ma:
    * wczytywać dane z parametru **user_name**, 
    * zapisać te dane do sesji pod kluczem **user_name**, 
    * wyświetlić informację o zapisaniu danych,
    * **user_name** powinno składać się z liter i/lub cyfr.
* `/say_hello/{n}` &ndash; gdzie **n** jest liczbą (wartość domyślna to 10). 
    Ten widok powinien:
    * wczytać z sesji zapisane w poprzednim punkcie imię,
    * wyświetlić je **n** razy, 
    * jeżeli w sesji nie ma zapisanego imienia, to powinien wyświetlić napis „Witaj nieznajomy” **n** razy.
* `/say_hello` - widok ma wyświetlić komunikat z poprzedniego punktu dokładnie 10 razy.
* `/create_cookie/{cookie_name}/{cookie_value}/{cookie_time}` – gdzie:
    * **cookie_time** jest liczbą (jest to założenie, które ma się znaleźć w **urls.py**), 
    * **cookie_name** i **cookie_value** powinny składać się z liter i/lub cyfr, 
    * widok ma nastawić ciasteczko o podanej nazwie na podaną wartość, 
    * ciasteczko ma żyć przez **cookie_time** minut.  
* `/delete_cookie/{cookie_name}`:
    * wyświetla zawartość ciasteczka o podanej nazwie,
    * usuwa je,
    * wyświetla komunikat `Ciasteczko zostało usunięte`, 
    * jeżeli takiego ciasteczka nie ma &ndash; powinien wyświetlić komunikat: `Brak takiego ciasteczka`.





# Egzamin &ndash; Zadanie 5 &ndash; formularz (5pkt)

Napisz widok, który udostępnisz pod adresem `/add_student`. Widok powinien zachować się następująco:

* po wejściu metodą GET:
    * wyświetlić formularz, dodania nowego studenta, a w nim następujące pola:
        * `name`,
        * `year_at_university`,
        * `is_active`.
Atrybut `name` dla każdego z pól powinien mieć wartość taką jak nazwa pola tzn: `name='name'`, `name='is_active'`.  
* po wejściu metodą POST:
    * utworzyć instancję klasy **Student**,
    * wypełnić własności utworzonego obiektu,
    * zapisać dane,
    * wyświetlić na ekranie komunikat `Dodano nowego studenta`.



