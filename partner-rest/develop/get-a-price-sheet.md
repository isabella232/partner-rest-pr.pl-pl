---
title: Pobieranie arkusza cen
description: Uzyskaj arkusz cen dla danego rynku i widoku. Obsługuje filtry w celu uzyskania historii według miesięcy.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0185a61ef0a3747aee1b06f88a7a8d6f1279f9e3
ms.sourcegitcommit: 1a183f9b37d646be240a48fc60e5902f409e8ac1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/26/2021
ms.locfileid: "122989702"
---
# <a name="get-a-price-sheet"></a>Pobieranie arkusza cen

Dotyczy:

- interfejs API Partner

W tym temacie wyjaśniono, jak uzyskać arkusz cen dla danego rynku i widoku. Ta metoda obsługuje filtry w celu uzyskania historii według miesięcy.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [interfejs API Partner uwierzytelniania.](api-authentication.md) Ten scenariusz obsługuje tylko uwierzytelnianie użytkowników aplikacji. Tylko aplikacja nie jest jeszcze obsługiwana. Partnerzy, którzy **doświadczą błędu HTTP:400,** powinni zapoznać się z [interfejs API Partner uwierzytelniania.](api-authentication.md)
- Ten interfejs API obsługuje obecnie tylko dostęp użytkowników, w przypadku których partnerzy muszą pełnić jedną z następujących ról: Administrator globalny, Agent administracyjny lub Agent sprzedaży.

## <a name="details"></a>Szczegóły

- Funkcja Current zwraca tylko dane dotyczące użycia planu platformy Azure i produktów rezerwacji.
- Bieżące [ceny](pricing.md) obejmują wszystkie mierniki i produkty dostępne w bieżącym miesiącu do daty wywołania interfejsu API. Poprzednie miesiące obejmują wszystkie mierniki i produkty dostępne dla danego miesiąca.
- Ceny miernika zużycia są tylko w USD, a partnerzy mają używać interfejsu API kursów wymiany walut obcych do obliczania kosztów w lokalnej walucie.
- Ceny miernika zużycia to szacowane ceny detaliczne. Rabaty dla partnerów są dostępne za [pośrednictwem środków uzyskane przez partnera.](/partner-center/partner-earned-credit-explanation)
- Ceny miernika rezerwacji obejmują rabaty dla partnerów programu CSP. Szacowane ceny detaliczne rezerwacji można znaleźć w udostępnionych usługach rezerwacji do pobrania na stronie Partner Center "Ceny i oferty".
- Więcej informacji na temat cen planu platformy Azure można znaleźć w [dokumentacji cennika planu platformy Azure.](/partner-center/azure-plan-price-list)
- Interfejsy API cen partnera i kursów wymiany walut nie są częścią [zestaw SDK Centrum partnerskiego](get-started.md).
- Ta metoda zwraca cennik jako strumień plików. Strumień plików jest plikiem .csv lub skompresowaną wersją pliku zip .csv. Poniżej znajdują się szczegółowe informacje na temat żądania skompresowanych plików.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POBIERZ** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value                                     |

### <a name="uri-required-parameters"></a>Wymagane parametry URI

Użyj następujących parametrów ścieżki, aby zażądać rynku i typu arkusza cen.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Rynku                      | ciąg   | Tak       | Dwulitowy kod kraju dla żądanego rynku       |
|PricesheetView | ciąg   | Tak       | Żądany typ arkusza cen może być azure_consumption, azure_reservations lub zaktualizowanylicencję.  |

> [!Note]
> Element updatedlicensebased PriceSheetView jest obecnie dostępny tylko dla partnerów, którzy są częścią nowego rozwiązania handlowego M365/D365 w wersji Technical Preview.

### <a name="uri-filter-parameters"></a>Parametry filtru URI

Użyj następujących parametrów filtru.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Oś czasu| ciąg   | Nie| Wartość domyślna to current, jeśli nie zostanie przekazana. Możliwe wartości to historia, bieżąca i przyszłość.       |
|Month (Miesiąc)| ciąg   | Nie| Wymagane tylko w przypadku zażądania historii muszą być zgodne z RRRRM dla żądanego arkusza cen.       |

### <a name="request-headers"></a>Nagłówki żądań

- Aby uzyskać więcej informacji, zobacz [Nagłówki REST](headers.md) partnerów.

Oprócz powyższych nagłówków pliki cenowe mogą być pobierane jako skompresowane, co skraca czas pobierania i przepustowości. Domyślnie pliki nie są kompresowane. Aby uzyskać skompresowane wersje plików, możesz dołączyć poniżej wartość nagłówka. Należy pamiętać, że skompresowane arkusze są dostępne tylko od kwietnia 2020 r., a wszystkie arkusze sprzed kwietnia 2020 r. są dostępne tylko jako nieskompresowane.

| Nagłówek                   | Typ wartości     | Wartość | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| ciąg   | Deflate| Opcjonalny. Jeśli pominięty strumień plików nie jest skompresowany.       |

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a>Żądanie przykładu dla nowego handlu

> [!Note]
> Element updatedlicensebased PriceSheetView jest obecnie dostępny tylko dla partnerów, którzy są częścią nowego rozwiązania handlowego M365/D365 w wersji Technical Preview.

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca cennik jako strumień plików. Strumień plików jest plikiem .csv lub skompresowaną wersją pliku zip .csv.

### <a name="response-example-for-new-commerce"></a>Przykład odpowiedzi dla nowego handlu

> [!Note]
> Element updatedlicensebased PriceSheetView jest obecnie dostępny tylko dla partnerów, którzy są częścią nowego rozwiązania handlowego M365/D365 w wersji Technical Preview.

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=sheets.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","BillingPlan","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","Tags","ERP Price“
"Advanced Communications","CFQ7TTC0HDK0","0001","Advanced Communications","Microsoft Corporation","Advanced meetings, calling, workflow integration, and management tools for IT.","","P1Y","Annual","US","USD","115.2","","","2/1/2019 12:00:00 AM","2/4/2021 8:35:31 PM","License","144"
======= Truncated ==============

```

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).
