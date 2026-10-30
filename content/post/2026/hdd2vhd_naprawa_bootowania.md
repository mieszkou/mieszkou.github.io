# Naprawa Bootowania (HDD to VHD)

**Problem:** Błąd `Failure when attempting to copy boot files` przy użyciu komendy `bcdboot`. **Przyczyna:** Partycja systemowa (EFI) po klonowaniu/konwersji straciła system plików (widoczna jako **RAW** w `diskpart`), co uniemożliwia zapisanie na niej plików rozruchowych.

------

## 1. Identyfikacja struktury (Diskpart)

Uruchom wiersz poleceń z nośnika instalacyjnego Windows i sprawdź wolumeny:

DOS

```
diskpart
list volume
```

*Szukaj małej partycji (~100-500 MB), która w kolumnie "Fs" ma wpis **RAW** lub jest ukryta.*

## 2. Naprawa partycji EFI

Należy sformatować uszkodzoną partycję na system plików FAT32 i przypisać jej literę, aby stała się dostępna dla narzędzi naprawczych.

DOS

```
select volume X          -- Gdzie X to numer partycji RAW (np. 99 MB)
format fs=fat32 quick    -- Przywrócenie systemu plików FAT32
assign letter=S          -- Przypisanie tymczasowej litery 'S'
exit
```

## 3. Generowanie plików rozruchowych (BCD)

Gdy partycja `S:` jest już gotowa, wgraj na nią pliki startowe wskazując folder Windows (zazwyczaj na dysku `C:`):

DOS

```
bcdboot C:\Windows /s S: /f UEFI
```

### Wyjaśnienie przełączników:

- `/s S:` – Wskazuje partycję docelową dla plików bootloadera.
- `/f UEFI` – Wymusza tworzenie plików dla trybu UEFI (zamiast Legacy/BIOS).