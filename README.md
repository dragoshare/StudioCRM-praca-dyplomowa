# StudioCRM – warstwa backendowa

Kod źródłowy stanowiący projekt bazowy pracy inżynierskiej:

> **Projekt i implementacja warstwy backendowej aplikacji internetowej wspomagającej zarządzanie studiem treningowym**
> Szymon Gorzula, Uniwersytet DSW Ideis, Wydział Studiów Stosowanych w Krakowie, kierunek Informatyka stosowana, 2027.

StudioCRM to backend systemu CRM dla studiów treningowych: klienci, trenerzy, lokalizacje, grafik sesji, treningi indywidualne, półindywidualne i grupowe, pakiety wejść, rozliczenia, płatności, portale klienta i trenera oraz synchronizacja grafiku z kalendarzem Microsoft Outlook.

## O tym repozytorium

- Repozytorium jest migawką kodu z gałęzi produkcyjnej z 18.11.2026, opublikowaną na potrzeby pracy dyplomowej. Rozwój odbywa się w osobnym, prywatnym repozytorium, dlatego ta kopia nie zawiera historii zmian.
- Z kopii usunięto wewnętrzną dokumentację operacyjną (wdrożenia, audyty, konfiguracja produkcji). Adresy usług produkcyjnych i firmowe adresy e-mail w danych startowych zastąpiono wartościami przykładowymi.
- Repozytorium nie zawiera haseł, kluczy ani danych osobowych klientów. Konfiguracja wymaga własnych sekretów (patrz niżej).
- Frontend aplikacji jest osobnym projektem i nie jest przedmiotem pracy.

## Technologie

- C#, .NET 8, ASP.NET Core Web API
- Entity Framework Core 8, PostgreSQL (Npgsql)
- Uwierzytelnianie JWT, Swagger/OpenAPI
- Integracje: Microsoft Graph (Outlook), Tpay, Resend, Cloudflare R2
- Testy: xUnit (testy jednostkowe i integracyjne na PostgreSQL)

## Struktura rozwiązania

| Projekt | Zawartość |
| --- | --- |
| `StudioCRM.Domain` | encje i enumy domenowe |
| `StudioCRM.Application` | interfejsy usług, DTO, ustawienia i wspólne reguły biznesowe |
| `StudioCRM.Infrastructure` | implementacje usług, EF Core, migracje, dane startowe i integracje |
| `StudioCRM.Api` | kontrolery REST, uwierzytelnianie, middleware, zadania w tle, konfiguracja DI |
| `StudioCRM.Tests` | testy jednostkowe i integracyjne |
| `docs` | kontrakty API i opisy wybranych obszarów dla aplikacji frontendowej |

Zależności: Application → Domain; Infrastructure → Application + Domain; Api → Application + Infrastructure.

## Uruchomienie lokalne

Wymagane: .NET 8 SDK oraz lokalna baza PostgreSQL.

```bash
dotnet restore StudioCRM.sln
dotnet build StudioCRM.sln --no-restore
```

Sekrety ustaw przez `dotnet user-secrets` (projekt `StudioCRM.Api`) lub zmienne środowiskowe, np. `ConnectionStrings__TestConnection`, `ConnectionStrings__DefaultConnection` i `Jwt__Key` (co najmniej 32 bajty). Środowisko Development domyślnie używa `TestConnection`.

```bash
dotnet run --project StudioCRM.Api --launch-profile https
```

Swagger jest dostępny pod `/swagger`, kontrola działania pod `/health`.

## Testy

```bash
dotnet test StudioCRM.Tests/StudioCRM.Tests.csproj
```

Testy oznaczone `PostgresFact` wymagają zmiennej `TPAY_TEST_DB` z connection stringiem osobnej bazy testowej. Bez niej są pomijane. Każdy taki test tworzy i usuwa losowy schemat `crm_test_*`.

## Prawa autorskie

© 2026 Szymon Gorzula. Wszelkie prawa zastrzeżone. Kod udostępniono wyłącznie do wglądu w związku z pracą dyplomową. Jego kopiowanie, modyfikowanie i dalsze wykorzystanie wymaga zgody autora.
