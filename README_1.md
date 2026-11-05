# Alkmie Payments Sync

Wewnętrzna aplikacja do pobierania informacji o płatnościach z konta Allegro w celu ich rozliczania w zewnętrznym systemie księgowo-finansowym. Aplikacja jest przeznaczona wyłącznie do użytku własnego właściciela konta i nie jest udostępniana innym sprzedawcom.

**Aktualna wersja:** 1.0.0

## Właściciel aplikacji

ALKEMIE GROUP BODNAR spółka komandytowa
ul. Inżynierska 13, 81-512 Gdynia
NIP: 8943060126 · REGON: 360952167 · KRS: 0000962940
Sklep internetowy: [alkmie.com](https://alkmie.com)

## Opis aplikacji

Aplikacja pobiera z Allegro REST API dane o płatnościach powiązanych z zamówieniami na koncie właściciela aplikacji i przekazuje je do zewnętrznego systemu, w którym prowadzone są rozliczenia (uzgadnianie wpłat z zamówieniami). Aplikacja działa wyłącznie w trybie odczytu: nie modyfikuje ofert, zamówień ani żadnych innych danych na koncie Allegro.

## Zakres funkcjonalny

- pobieranie listy płatności i ich statusów,
- pobieranie szczegółów pojedynczej płatności (kwota, data, status, powiązane zamówienie),
- przekazywanie pobranych danych do zewnętrznego systemu rozliczeniowego właściciela konta.

Aplikacja nie udostępnia danych osobom trzecim ani nie publikuje ich publicznie. Dane trafiają wyłącznie do systemu rozliczeniowego właściciela konta.

## Przepływ OAuth

Aplikacja korzysta z autoryzacji OAuth 2.0 (Authorization Code Flow).

1. Właściciel konta loguje się na konto Allegro i wyraża zgodę na wskazane niżej uprawnienia.
2. Allegro przekierowuje na adres zwrotny aplikacji z kodem autoryzacyjnym.
3. Aplikacja wymienia kod na access token i refresh token.
4. Access token jest odświeżany automatycznie za pomocą refresh tokena.

## Wykorzystywane scope'y

| Scope | Uzasadnienie |
|---|---|
| `allegro:api:payments:read` | Odczyt informacji o płatnościach na własnym koncie, niezbędny do rozliczania płatności w zewnętrznym systemie. |

Aplikacja nie żąda żadnych uprawnień zapisu.

## Bezpieczeństwo danych

- Tokeny (access i refresh) oraz Client Secret są przechowywane po stronie serwera, w zmiennych środowiskowych lub menedżerze sekretów, i nie są umieszczane w kodzie ani w repozytorium.
- Dostęp do aplikacji i przechowywanych danych mają wyłącznie upoważnione osoby.
- Cała komunikacja z API oraz z systemem rozliczeniowym odbywa się przez HTTPS.
- Każde wywołanie API zawiera nagłówek User-Agent zgodny z wymaganiami Allegro.

## Kontakt

W sprawach dotyczących aplikacji: **hello@alkmie.com**

## User-Agent

```
AlkmiePaymentsSync/1.0.0 (+https://github.com/tpinczewski-lab/alkmie-payments-sync)
```
