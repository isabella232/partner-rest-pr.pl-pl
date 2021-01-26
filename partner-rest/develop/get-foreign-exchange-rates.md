---
title: Pobieranie kursów wymiany walut
description: Uzyskaj kursy wymiany walut dla danego miesiąca.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770521"
---
# <a name="get-foreign-exchange-rates"></a>Pobieranie kursów wymiany walut

Dotyczy:

- Interfejs API partnera

W tym temacie wyjaśniono, jak uzyskać kursy wymiany walut w danym miesiącu.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie użytkownika aplikacji. Tylko aplikacja nie jest jeszcze obsługiwana.
- Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą mieć jedną z następujących ról: Administrator globalny, Agent administracyjny lub agent sprzedaży.


## <a name="details"></a>Szczegóły

- Obecnie używany z [interfejsem API uzyskiwania arkusza cen](get-a-price-sheet.md) do obliczania oczekiwanych opłat za walutę lokalną dostawcy CSP planu platformy Azure.
- Stawki za wymianę walut obcych są spełnione przez cały miesiąc, w którym są one wysyłane.
- Więcej informacji o [cenach](pricing.md) planu platformy Azure można znaleźć w [dokumentacji cennika planu platformy Azure](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- Cennik partnerski i interfejsy API wymiany walut obcych nie są częścią [zestawu SDK Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/get-started).
- Ta metoda zwraca wyniki jako strumień pliku. Strumień plików to plik CSV lub skompresowana wersja pliku CSV. Poniżej znajdują się szczegółowe informacje dotyczące sposobu żądania skompresowanych plików.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Pobierz** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month="{Month}")/$value                                  |

### <a name="uri-required-parameters"></a>Parametry wymagane przez identyfikator URI

Użyj następujących parametrów ścieżki, aby zażądać pożądanego miesiąca kursów wymiany walut.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Month (Miesiąc)                      | ciąg   | Tak       | Musi być w formacie YYYMM. W przypadku pominięcia wartości domyślnych w bieżącym miesiącu.       |

### <a name="request-headers"></a>Nagłówki żądań

- Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .

Oprócz powyższych nagłówków pliki można pobrać jako skompresowane zmniejszenie przepustowości i czas pobierania. Domyślnie pliki nie są skompresowane. Aby uzyskać skompresowane wersje plików, można uwzględnić poniżej wartość nagłówka. Należy pamiętać, że skompresowane arkusze są dostępne tylko od 2020 kwietnia, a wszystkie żądania przed 2020 kwietnia są dostępne tylko jako nieskompresowane.

| Nagłówek                   | Typ wartości     | Wartość | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| ciąg   | Wklęśnięcie| Opcjonalny. Jeśli pominięty strumień plików nie jest skompresowany.       |

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca obce kursy wymiany jako strumień pliku. Strumień plików to plik CSV lub skompresowana wersja pliku CSV.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
