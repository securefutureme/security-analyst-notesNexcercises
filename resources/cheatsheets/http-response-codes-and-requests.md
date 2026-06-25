![alt](/resources/cheatsheets/Attachments/1-image.png)

Szybka ściąga przedstawiająca najczęściej używane metody HTTP, kody odpowiedzi oraz podstawowe pola nagłówków.

## Spis treści
 
- [Najczęściej używane metody HTTP](#najczesciej-uzywane-metody-http)
- [[#Pozostałe metody HTTP]]
- [[#Porównanie metod HTTP]]
- [[#Kody odpowiedzi HTTP]]
- [[#Kategorie kodów HTTP]]
- [[#Budowa żądania HTTP]]
- [[#Najważniejsze nagłówki HTTP]]
- [[#Uwagi bezpieczeństwa]]
---

# najczesciej-uzywane-metody-http

## GET

Służy do pobierania zasobu lub kolekcji zasobów.

```http
GET /users/15 HTTP/1.1
```

Najważniejsze cechy:

- zwykle nie zawiera body,
- nie powinien zmieniać danych po stronie serwera,
- parametry mogą być przesyłane w adresie URL,
- odpowiedź może być przechowywana w pamięci podręcznej,
- metoda jest bezpieczna i idempotentna.

> Dane poufne, takie jak hasła i tokeny, nie powinny być umieszczane w adresie URL, ponieważ mogą zostać zapisane w logach, historii przeglądarki lub nagłówku `Referer`.

---

## POST

Służy najczęściej do utworzenia nowego zasobu lub przesłania danych do serwera.

```http
POST /users HTTP/1.1
Content-Type: application/json

{
  "username": "analyst"
}
```

Najważniejsze cechy:

- zazwyczaj zawiera nagłówki oraz body,
- może utworzyć nowy zasób,
- może uruchomić operację po stronie serwera,
- kolejne identyczne żądania mogą wywołać operację wielokrotnie,
- metoda nie jest idempotentna,
- odpowiedź może być cache’owana tylko przy odpowiedniej konfiguracji.

Przykład:

```text
POST /users
```

może utworzyć użytkownika o nowym, unikalnym identyfikatorze.

---

## PUT

Służy do utworzenia lub pełnej aktualizacji zasobu pod konkretnym adresem URI.

```http
PUT /users/15 HTTP/1.1
Content-Type: application/json

{
  "username": "analyst",
  "role": "user"
}
```

Najważniejsze cechy:

- zazwyczaj zawiera body,
- zastępuje pełną reprezentację wskazanego zasobu,
- klient zwykle zna identyfikator zasobu,
- metoda jest idempotentna.

Wielokrotne wysłanie tego samego żądania powinno prowadzić do tego samego stanu zasobu.

---

## PATCH

Służy do częściowej aktualizacji istniejącego zasobu.

```http
PATCH /users/15 HTTP/1.1
Content-Type: application/json

{
  "role": "admin"
}
```

Najważniejsze cechy:

- modyfikuje tylko wskazane pola,
- nie wymaga przesyłania całego zasobu,
- zazwyczaj zawiera body,
- nie zawsze jest idempotentna — zależy to od sposobu implementacji.

---

## DELETE

Służy do usunięcia wskazanego zasobu.

```http
DELETE /users/15 HTTP/1.1
```

Najważniejsze cechy:

- identyfikator zasobu najczęściej znajduje się w URI,
- body zwykle nie jest wymagane,
- usuwa wskazaną reprezentację zasobu,
- metoda jest idempotentna.

Ponowne usunięcie tego samego zasobu nie powinno powodować dodatkowych zmian stanu.

---

# Pozostałe metody HTTP

## HEAD

Działa podobnie do `GET`, ale serwer nie zwraca body odpowiedzi.

```http
HEAD /report.pdf HTTP/1.1
```

Zastosowanie:

- sprawdzenie, czy zasób istnieje,
- odczyt nagłówków odpowiedzi,
- sprawdzenie typu i rozmiaru pliku,
- weryfikacja daty ostatniej modyfikacji,
- kontrola cache bez pobierania całej zawartości.

---

## OPTIONS

Zwraca informacje o sposobach komunikacji obsługiwanych przez serwer lub konkretny zasób.

```http
OPTIONS /users HTTP/1.1
```

Może zwrócić nagłówek:

```http
Allow: GET, POST, PUT, DELETE, OPTIONS
```

Metoda jest również używana podczas obsługi mechanizmu CORS, np. w żądaniach preflight.

---

## CONNECT

Tworzy tunel do wskazanego serwera.

```http
CONNECT example.com:443 HTTP/1.1
```

Najczęstsze zastosowanie:

- zestawianie tunelu HTTPS przez serwer proxy,
- przekazywanie zaszyfrowanego ruchu TLS.

---

## TRACE

Zwraca do klienta treść otrzymanego żądania.

```http
TRACE / HTTP/1.1
```

Zastosowanie:

- diagnostyka trasy żądania,
- sprawdzanie zmian wprowadzanych przez serwery pośredniczące.

### Ryzyko bezpieczeństwa

Metoda `TRACE` może ujawniać przesyłane nagłówki, w tym dane uwierzytelniające lub cookies. Historycznie była kojarzona z atakami typu **Cross-Site Tracing (XST)**.

Jeżeli nie jest potrzebna, powinna zostać wyłączona w konfiguracji serwera.

---

# Porównanie metod HTTP

|Metoda|Główne zastosowanie|Body żądania|Bezpieczna|Idempotentna|Cache|
|---|---|:-:|:-:|:-:|:-:|
|`GET`|Pobieranie danych|Zwykle nie|Tak|Tak|Tak|
|`POST`|Tworzenie zasobu / przesyłanie danych|Zwykle tak|Nie|Nie|Warunkowo|
|`PUT`|Pełna aktualizacja zasobu|Tak|Nie|Tak|Zwykle nie|
|`PATCH`|Częściowa aktualizacja zasobu|Tak|Nie|Zależy|Zwykle nie|
|`DELETE`|Usunięcie zasobu|Zwykle nie|Nie|Tak|Nie|
|`HEAD`|Pobranie samych nagłówków|Zwykle nie|Tak|Tak|Tak|
|`OPTIONS`|Sprawdzenie dostępnych metod|Opcjonalnie|Tak|Tak|Zwykle nie|
|`CONNECT`|Utworzenie tunelu|Zależy|Nie|Nie|Nie|
|`TRACE`|Diagnostyka żądania|Zwykle nie|Tak|Tak|Nie|

### Znaczenie pojęć

- **Bezpieczna metoda** — nie powinna zmieniać stanu zasobu.
- **Idempotentna metoda** — wielokrotne wykonanie tego samego żądania powinno mieć taki sam efekt jak wykonanie go jeden raz.

---

# Kody odpowiedzi HTTP

|Kod|Nazwa|Znaczenie|
|--:|---|---|
|`100`|Continue|Klient może kontynuować wysyłanie żądania|
|`200`|OK|Żądanie zostało poprawnie wykonane|
|`201`|Created|Utworzono nowy zasób|
|`202`|Accepted|Żądanie zostało przyjęte do przetworzenia|
|`204`|No Content|Operacja zakończona sukcesem, ale odpowiedź nie zawiera body|
|`301`|Moved Permanently|Zasób został trwale przeniesiony|
|`302`|Found|Zasób znajduje się tymczasowo pod innym adresem|
|`303`|See Other|Wynik operacji należy pobrać z innego URI metodą GET|
|`304`|Not Modified|Zasób nie zmienił się i może zostać użyty z cache|
|`400`|Bad Request|Żądanie ma niepoprawną składnię lub zawiera błędne dane|
|`401`|Unauthorized|Wymagane jest poprawne uwierzytelnienie|
|`402`|Payment Required|Kod zarezerwowany dla mechanizmów płatności|
|`403`|Forbidden|Serwer rozumie żądanie, ale odmawia dostępu|
|`404`|Not Found|Zasób nie został znaleziony|
|`405`|Method Not Allowed|Użyta metoda nie jest obsługiwana dla danego zasobu|
|`408`|Request Timeout|Serwer zbyt długo czekał na zakończenie żądania|
|`429`|Too Many Requests|Klient wysłał zbyt wiele żądań|
|`500`|Internal Server Error|Wewnętrzny błąd serwera|
|`502`|Bad Gateway|Serwer pośredniczący otrzymał niepoprawną odpowiedź|
|`503`|Service Unavailable|Usługa jest tymczasowo niedostępna|
|`504`|Gateway Timeout|Serwer pośredniczący nie otrzymał odpowiedzi na czas|

---

# Kategorie kodów HTTP

|Zakres|Kategoria|Znaczenie|
|--:|---|---|
|`1xx`|Informacyjne|Żądanie zostało odebrane i jest dalej przetwarzane|
|`2xx`|Sukces|Żądanie zakończyło się powodzeniem|
|`3xx`|Przekierowanie|Klient musi wykonać dodatkową akcję|
|`4xx`|Błąd klienta|Problem znajduje się po stronie żądania|
|`5xx`|Błąd serwera|Serwer nie był w stanie poprawnie obsłużyć żądania|

## Kod 418

```http
418 I'm a teapot
```

Kod `418` powstał jako żart primaaprilisowy w 1998 roku i oznacza:

> „Jestem czajnikiem”.

Nie jest standardowym kodem używanym w typowych aplikacjach produkcyjnych. 🍵

> Serwery mogą zwracać niestandardowe kody odpowiedzi, jednak aplikacje powinny przede wszystkim korzystać ze standardowych kodów HTTP.

---

# Budowa żądania HTTP

Przykładowe żądanie:

```http
GET /hello.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

## Omówienie

### Linia żądania

```http
GET /hello.html HTTP/1.1
```

Zawiera:

- metodę HTTP: `GET`,
- URI zasobu: `/hello.html`,
- wersję protokołu: `HTTP/1.1`.

### Nagłówek Host

```http
Host: www.example.com
```

Określa domenę i opcjonalnie port serwera, do którego kierowane jest żądanie.

Przykład z portem:

```http
Host: www.example.com:8080
```

### Nagłówek User-Agent

```http
User-Agent: Mozilla/5.0
```

Przekazuje informacje o kliencie wysyłającym żądanie, np.:

- przeglądarce,
- systemie operacyjnym,
- bibliotece HTTP,
- narzędziu automatyzującym.

> Wartość `User-Agent` może zostać łatwo zmieniona lub sfałszowana.

### Nagłówek Accept-Encoding

```http
Accept-Encoding: gzip, deflate
```

Informuje serwer, jakie sposoby kompresji odpowiedzi obsługuje klient.

### Nagłówek Connection

```http
Connection: keep-alive
```

Informuje, że połączenie TCP może zostać ponownie wykorzystane do przesłania kolejnych żądań.

Takie połączenie nazywane jest **trwałym połączeniem HTTP**.

Korzyści:

- mniejsza liczba nowych połączeń TCP,
- niższe opóźnienia,
- mniejsze obciążenie klienta i serwera.

---

# Najważniejsze nagłówki HTTP

## Nagłówki żądania

|Nagłówek|Znaczenie|
|---|---|
|`Host`|Domena i port serwera docelowego|
|`User-Agent`|Informacje o kliencie|
|`Accept`|Typy treści akceptowane przez klienta|
|`Accept-Encoding`|Obsługiwane metody kompresji|
|`Authorization`|Dane uwierzytelniające lub token|
|`Cookie`|Cookies przesyłane do serwera|
|`Referer`|Adres strony, z której wykonano przejście|
|`Origin`|Źródło żądania używane m.in. przez CORS|
|`Content-Type`|Format danych znajdujących się w body|
|`Content-Length`|Długość body w bajtach|
|`Connection`|Sposób zarządzania połączeniem|

## Nagłówki odpowiedzi

|Nagłówek|Znaczenie|
|---|---|
|`Content-Type`|Typ zwracanej zawartości|
|`Content-Length`|Rozmiar odpowiedzi|
|`Set-Cookie`|Ustawienie cookie po stronie klienta|
|`Location`|Adres docelowy przekierowania|
|`Server`|Informacja o oprogramowaniu serwera|
|`Cache-Control`|Zasady przechowywania odpowiedzi w cache|
|`WWW-Authenticate`|Wymagana metoda uwierzytelnienia|
|`Access-Control-Allow-Origin`|Określa dozwolone źródła CORS|
|`Strict-Transport-Security`|Wymusza korzystanie z HTTPS|
|`Content-Security-Policy`|Ogranicza źródła ładowanych zasobów|

---

# Uwagi bezpieczeństwa

- Nie umieszczaj haseł, tokenów ani innych danych poufnych w adresach URL.
- Używaj HTTPS do przesyłania danych uwierzytelniających.
- Wyłącz metodę `TRACE`, jeżeli nie jest potrzebna.
- Ograniczaj dostępne metody HTTP do rzeczywiście wymaganych.
- Waliduj i filtruj dane przesyłane w parametrach oraz body.
- Nie ufaj wartości `User-Agent` — może zostać sfałszowana.
- Monitoruj kody `401`, `403`, `404`, `429` i `5xx` pod kątem anomalii.
- Stosuj bezpieczne atrybuty cookies: `HttpOnly`, `Secure` i `SameSite`.
- Nie ujawniaj szczegółowych informacji o serwerze w nagłówku `Server`.
- Zwracaj poprawne kody HTTP, ponieważ ułatwia to monitoring i analizę incydentów.
