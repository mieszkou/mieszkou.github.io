Błąd -820 w Firebird oznacza niezgodność wersji struktury na dysku (ODS): baza gastro.fdb ma ODS 11.1 (z Firebird 2.x), a klient lub serwer oczekuje ODS 12.2 (Firebird 3.x). Problem возникает w systemie Novitus SOGA po aktualizacji do nowszej wersji programu, która instaluje Firebird 3.x.

Przyczyna
Firebird 3.x nie obsługuje baz z ODS 11.x – wymaga konwersji. Starsza baza z SOGA (prawdopodobnie wersja 3.x) nie działa z nowym silnikiem.

Rozwiązanie 1: Aktualizacja bazy (zalecane)
Zainstaluj starszy Firebird 2.5 (np. z https://github.com/FirebirdSQL/firebird/releases/tag/R2_5_9), aby otworzyć bazę.
​

Zrób backup: gbak -b -user SYSDBA -password masterkey "C:\Program Files\Novitus\SOGA\Baza\gastro.fdb" gastro.gbak
​

Przywróć w Firebird 3.x: gbak -rep -c -user SYSDBA -password masterkey gastro.gbak "C:\Program Files\Novitus\SOGA\Baza\gastro_new.fdb" – to utworzy bazę z ODS 12.x.
​

Zastąp starą bazę nową i uruchom SOGA.
​