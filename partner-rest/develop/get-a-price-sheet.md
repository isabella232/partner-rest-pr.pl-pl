---
title: Pobieranie arkusza cen
description: Uzyskaj arkusz cen dla danego rynku i widoku. Obsługuje filtry, aby uzyskać historię według miesiąca.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5195ebed6559bd71a7832a667e63ee801be1c82f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770516"
---
# <a name="get-a-price-sheet"></a>Pobieranie arkusza cen

Dotyczy:

- Interfejs API partnera

W tym temacie wyjaśniono, jak uzyskać arkusz cen dla danego rynku i widoku. Ta metoda obsługuje filtry w celu uzyskania historii według miesiąca.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie użytkownika aplikacji. Aplikacja-tylko nie jest jeszcze obsługiwana.
- Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą mieć jedną z następujących ról: Administrator globalny, Agent administracyjny lub agent sprzedaży.

## <a name="details"></a>Szczegóły

- Bieżąca zwraca dane tylko w przypadku użycia planu platformy Azure i produktów rezerwacji.
- Bieżące [ceny](pricing.md) obejmują wszystkie liczniki i produkty dostępne w bieżącym miesiącu w dniu, w którym wywoływany jest interfejs API. Poprzednie miesiące obejmują wszystkie liczniki i produkty dostępne w danym miesiącu.
- Ceny licznika zużycia są dostępne tylko w USD, partnerzy korzystają z interfejsu API kursów wymiany walut w celu obliczenia kosztów lokalnych.
- Ceny licznika zużycia to szacowane ceny detaliczne. Rabaty partnerów są dostępne za pośrednictwem środków [partnerów](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).
- Ceny licznika rezerwacji obejmują rabaty partnerów programu CSP. Szacowane ceny detaliczne dla rezerwacji można znaleźć w temacie rezerwacja udostępnionych usług do pobrania z poziomu strony Cennik i oferty w centrum partnerskim.
- Więcej informacji o cenach planu platformy Azure można znaleźć w [dokumentacji cennika planu platformy Azure](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- Cennik partnerski i interfejsy API wymiany walut obcych nie są częścią [zestawu SDK Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/get-started).
- Ta metoda zwraca listę cen jako strumień pliku. Strumień plików to plik CSV lub skompresowana wersja pliku CSV. Poniżej znajdują się szczegółowe informacje dotyczące sposobu żądania skompresowanych plików.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Pobierz** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market="{Marketo}", PricesheetView = "{View}")/$value                                     |

### <a name="uri-required-parameters"></a>Parametry wymagane przez identyfikator URI

Użyj następujących parametrów ścieżki, aby zażądać danego rynku i typu arkusza cen.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Do                      | ciąg   | Tak       | Dwuliterowy kod kraju dla żądanego rynku       |
|PricesheetView | ciąg   | Tak       | Typ żądanego arkusza cen może być azure_consumption lub azure_reservations       |

### <a name="uri-filter-parameters"></a>Parametry filtru identyfikatora URI

Użyj następujących parametrów filtru.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Oś czasu| ciąg   | Nie| Wartość domyślna to Current, jeśli nie została przeniesiona. Możliwe wartości to History, Current i Future.       |
|Month (Miesiąc)| ciąg   | Nie| Wymagane tylko wtedy, gdy wymagana jest historia, musi być zgodna z YYYYMM dla żądanego arkusza cen.       |

### <a name="request-headers"></a>Nagłówki żądań

- Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .

Oprócz powyższych nagłówków pliki cen można pobrać jako skompresowane zmniejszenie przepustowości i czas pobierania. Domyślnie pliki nie są skompresowane. Aby uzyskać skompresowane wersje plików, można uwzględnić poniżej wartość nagłówka. Należy pamiętać, że skompresowane arkusze są dostępne tylko od 2020 kwietnia, a wszystkie arkusze przed 2020 kwietnia są dostępne tylko jako nieskompresowane.

| Nagłówek                   | Typ wartości     | Wartość | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| ciąg   | Wklęśnięcie| Opcjonalny. Jeśli pominięty strumień plików nie jest skompresowany.       |

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca listę cen jako strumień pliku. Strumień plików to plik CSV lub skompresowana wersja pliku CSV.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```
