# Trening klienta w innej lokalizacji (2026-11-17)

Zmiana zachowania backendu, bez nowych pól i endpointów.

- Klient z pakietem **osobistym lub semi** z jednej lokalizacji może okazjonalnie trenować w sesji w drugiej lokalizacji.
  Przy zakończeniu sesji (ręcznie, automatycznie i przez `count-from-package`) CRM odlicza wejście z jego aktywnego pakietu,
  nawet gdy pakiet jest przypisany do innej lokalizacji.
- Gdy klient ma pakiety w kilku lokalizacjach, pierwszeństwo ma pakiet ważny w lokalizacji sesji.
- Typ sesji liczy się jak dotąd z liczby uczestników, więc wszystkim uczestnikom sesja rozlicza się jako semi z tą osobą
  (np. 1:3 zamiast 1:2). Różnicę salda wylicza stawka lokalizacji pakietu klienta (ma znaczenie tylko dla 1:1).
- **Pakiety grupowe** bez zmian: odliczają się tylko w swojej lokalizacji.
- W CRM klienta z innej lokalizacji do sesji dodaje Owner. Trener w panelu nadal może dodawać tylko swoich klientów.
- Z Outlooka: kalendarz Ownera rozpoznaje każdego klienta organizacji, a kalendarz trenera klientów ze wszystkich
  lokalizacji, w których trener pracuje (przy nowym wydarzeniu i przy dopisaniu osoby do istniejącego). Klient musi być
  zaproszony na swój adres kalendarzowy, czyli kontakt z synchronizacji kontaktów.
