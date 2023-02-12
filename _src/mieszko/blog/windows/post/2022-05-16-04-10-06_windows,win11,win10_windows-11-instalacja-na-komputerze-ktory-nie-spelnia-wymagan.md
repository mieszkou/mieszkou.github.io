<!--t Windows 11: instalacja na komputerze który nie spełnia wymagań t-->
<!--d ## Wariant 1 Przegrywam zawartość płytki instalacyjnej **Windows 10** do jakiegoś katalogu na komputerze. W katalogu sources podmieniam plik d-->
<!--tag windows,win11,win10 tag-->

## Wariant 1

Przegrywam zawartość płytki instalacyjnej **Windows 10** do jakiegoś katalogu na komputerze.
W katalogu sources podmieniam plik `install.wim` na ten w płyty Windows 11.


## Wariant 2

Przegrywam zawartość płytki instalacyjnej **Windows 11** do jakiegoś katalogu na komputerze. 
W katalogu `sources` podmieniam pliki: 
```
appraiser.sdb, 
appraiserdatasha1.cat, 
appraiserres.dll, 
appraiserwc.dll 
```
na te same z najnowszego obrazu Windows 10.  Uruchamiam `setup.exe` i instaluje Windows 11