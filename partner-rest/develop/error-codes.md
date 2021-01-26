---
title: Kody błędów REST interfejsu API partnera
description: Interfejsy API REST partnera zwracają obiekt JSON z kodem stanu dotyczącym sukcesu lub niepowodzenia żądania.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0829f48e5028b4a19e8a6f7b89fbb41d83a50cab
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770498"
---
# <a name="partner-api-rest-error-codes"></a>Kody błędów REST interfejsu API partnera

Dotyczy:

- Interfejs API partnera

Błędy w interfejsie API REST partnera są zwracane przy użyciu standardowych kodów stanu HTTP, a także obiektu odpowiedzi błędu JSON.

## <a name="http-status-codes"></a>Kody stanu HTTP

W poniższej tabeli wymieniono i opisano kody stanu HTTP, które mogą być zwracane.

| Kod stanu | Komunikat o stanie                  | Opis                                                                                                                            |
|:------------|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| 400         | Nieprawidłowe żądanie                     | Nie można przetworzyć żądania, ponieważ jest źle sformułowane lub nieprawidłowe.                                                                       |
| 401         | Brak autoryzacji                    | Brak wymaganych informacji uwierzytelniania lub są one nieprawidłowe dla zasobu.                                                   |
| 403         | Forbidden                       | Odmowa dostępu do żądanego zasobu. Użytkownik może nie mieć wystarczających uprawnień. **Ważne: Jeśli zasady dostępu warunkowego są stosowane do zasobu, `HTTP 403; Forbidden error=insufficent_claims` mogą zostać zwrócone.** Aby uzyskać więcej informacji na temat Microsoft Graph i dostępu warunkowego, zobacz [wskazówki dla deweloperów dotyczące Azure Active Directory dostępu warunkowego](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer)  |
| 404         | Nie znaleziono                       | Żądany zasób nie istnieje.                                                                                                  |
| 405         | Niedozwolona metoda              | Metoda HTTP w żądaniu nie jest dozwolona w zasobie.                                                                         |
| 406         | Nieakceptowalny                  | Ta usługa nie obsługuje formatu żądanego w nagłówku Accept.                                                                |
| 409         | Konflikt                        | Bieżący stan powoduje konflikt z elementem oczekiwanym przez żądanie. Na przykład określony folder nadrzędny może nie istnieć.                   |
| 410         | Procedury                            | Żądany zasób nie jest już dostępny na serwerze.                                               |
| 411         | Wymagana długość                 | W żądaniu jest wymagany nagłówek Content-Length.                                                                                    |
| 412         | Niepowodzenie warunku wstępnego             | Warunek wstępny podany w żądaniu (na przykład nagłówek if-Match) nie jest zgodny z bieżącym stanem zasobu.                       |
| 413         | Jednostka żądania jest zbyt duża        | Rozmiar żądania przekracza maksymalny limit.                                                                                            |
| 415         | Nieobsługiwany typ nośnika          | Typ zawartości żądania to format, który nie jest obsługiwany przez usługę.                                                      |
| 416         | Żądany zakres nie jest niewłaściwego | Określony zakres bajtów jest nieprawidłowy lub niedostępny.                                                                                    |
| 422         | Nieprzetwarzana jednostka            | Nie można przetworzyć żądania, ponieważ jest semantycznie niepoprawna.                                                                        |
| 423         | Zablokowano                          | Zasób, do którego uzyskuje się dostęp, jest zablokowany.                                                                                          |
| 429         | Zbyt wiele żądań               | Aplikacja kliencka została ograniczona i nie powinna próbować powtórzyć żądania przed upływem czasu.                |
| 500         | Wewnętrzny błąd serwera           | Wystąpił wewnętrzny błąd serwera podczas przetwarzania żądania.                                                                       |
| 501         | Nie zaimplementowano                 | Żądana funkcja nie została zaimplementowana.                                                                                               |
| 503         | Usługa jest niedostępna             | Usługa jest tymczasowo niedostępna do konserwacji lub jest przeciążona. Można powtórzyć żądanie po opóźnieniu, długość, która może być określona w nagłówku Retry-After.|
| 504         | Limit czasu bramy                 | Serwer, który działa jako serwer proxy, nie otrzymał czasowo odpowiedzi od nadrzędnego serwera, którego potrzebuje do uzyskania dostępu podczas próby wykonania żądania. Mogą występować razem z 503. |
| 507         | Niewystarczająca ilość miejsca            | Osiągnięto maksymalny limit przydziału miejsca do magazynowania.                                                                                            |
| 509         | Przekroczono limit przepustowości        | Twoja aplikacja została ograniczona przez przekroczenie limitu maksymalnej przepustowości. Aplikacja może ponownie ponowić żądanie po upływie dłuższego czasu. |

Odpowiedź na błąd jest pojedynczym obiektem JSON, który zawiera pojedynczą właściwość o nazwie **Error**. Ten obiekt zawiera wszystkie szczegóły błędu. Możesz użyć informacji zwróconych w tym miejscu zamiast lub oprócz kodu stanu HTTP. Poniżej znajduje się przykład pełnej treści błędu JSON.

## <a name="error-resource-type"></a>Typ zasobu błędu

Odpowiedź na błąd jest pojedynczym obiektem JSON, który zawiera pojedynczą właściwość o nazwie **Error**. Ten obiekt zawiera wszystkie szczegóły błędu. Możesz użyć informacji zwróconych w tym miejscu zamiast lub oprócz kodu stanu HTTP. Poniżej znajduje się przykład pełnej treści błędu JSON.

W poniższej tabeli i kodzie przedstawiono schemat odpowiedzi na błąd.

| Nazwa        | Typ   | Opis                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| kod        | ciąg | Zawsze zwracana. Wskazuje rodzaj błędu, który wystąpił. Wartość inna niż null.                          |
| message | ciąg | Zawsze zwracana. Opisuje błąd szczegółowo i zawiera dodatkowe informacje o debugowaniu. Wartość inna niż null, niepusta. Maksymalna długość to 1024 znaków. |
| innerError        | object  | Opcjonalny. Dodatkowy obiekt błędu, który może być bardziej szczegółowy niż błąd najwyższego poziomu.                                   |
| obiektów      | ciąg | Obiekt docelowy, z którego pochodzi błąd.                                                      |

### <a name="code-property"></a>Właściwość Code

`code`Właściwość zawiera jedną z następujących możliwych wartości. Aplikacje powinny być przygotowane do obsługi jednego z tych błędów.

| Kod                      | Opis
|:--------------------------|:--------------
| **accessDenied**          | Obiekt wywołujący nie ma uprawnień do wykonania tej akcji.
| **ogólnaexception**      | Wystąpił nieokreślony błąd.
| **invalidRequest**        | Żądanie jest źle sformułowane lub nieprawidłowe.
| **itemNotFound**          | Nie można znaleźć zasobu.
|**preconditionFailed**     | Warunek wstępny podany w żądaniu (na przykład nagłówek if-Match) nie jest zgodny z bieżącym stanem zasobu.
| **resourceModified**      | Aktualizowany zasób został zmieniony od czasu ostatniego odczytu przez obiekt wywołujący, zazwyczaj jest niezgodny z elementem eTag.
| **serviceNotAvailable**   | Usługa jest niedostępna. Spróbuj ponownie wykonać żądanie po opóźnieniu. Może istnieć Retry-After nagłówek.
| **nieuwierzytelnione**       | Obiekt wywołujący nie jest uwierzytelniony.

### <a name="message-property"></a>Message — właściwość

`message`Właściwość w katalogu głównym zawiera komunikat o błędzie, który ma zostać odczytany przez dewelopera. Komunikaty o błędach nie są zlokalizowane i nie powinny być wyświetlane bezpośrednio dla użytkownika. W przypadku obsługi błędów kod nie powinien sprawdzać `message` wartości, ponieważ mogą one ulec zmianie w dowolnym momencie i często zawierają informacje dynamiczne specyficzne dla żądania zakończonego niepowodzeniem. Należy tylko kod dla kodów błędów zwracanych we `code` właściwościach.

### <a name="innererror-object"></a>Obiekt InnerError

`innererror`Obiekt może rekursywnie zawierać więcej `innererror` obiektów z dodatkowymi, bardziej szczegółowymi kodami błędów. W przypadku obsługi błędu aplikacje powinny przechodzić przez wszystkie dostępne kody błędów i korzystać z najbardziej szczegółowych informacji, które są przez nie zrozumiałe.

Niektóre dodatkowe błędy mogą wystąpić w aplikacji w zagnieżdżonych `innererror` obiektach. Aplikacje nie są wymagane do obsługi tych aplikacji, ale mogą je wybrać. Usługa może dodawać nowe kody błędów lub przestać zwracać starych w dowolnym momencie, dlatego ważne jest, aby wszystkie aplikacje mogły obsłużyć [podstawowe kody błędów]

```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}
```
