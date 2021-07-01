---
title: Uzyskiwanie macierzy ofert
description: Uzyskiwanie macierzy ofert dla danej daty. Obsługuje filtry w celu uzyskania historii według miesięcy.
ms.date: 02/11/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e53276c1170febab002d35a42c88c1f96f7b7428
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/01/2021
ms.locfileid: "113131303"
---
# <a name="get-an-offer-matrix"></a>Uzyskiwanie macierzy ofert

Dotyczy:

- interfejs API Partner
- Nowe środowisko handlowe M365/D365 w wersji Technical Preview. Poniższe zmiany dotyczące nowego handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego rozwiązania handlowego M365/D365 w wersji Technical Preview.

W tym temacie wyjaśniono, jak uzyskać macierz ofert dla danego miesiąca. Macierz oferty zawiera właściwości i reguły zakupu dla produktów i jednostki SKU. Ta metoda obsługuje filtry w celu uzyskania historii według miesięcy.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [interfejs API Partner uwierzytelniania.](api-authentication.md) Ten scenariusz obsługuje tylko uwierzytelnianie użytkowników aplikacji. Tylko aplikacja nie jest jeszcze obsługiwana. Partnerzy, którzy **doświadczą błędu HTTP:400,** powinni zapoznać się [z dokumentacją interfejs API Partner uwierzytelniania.](api-authentication.md)
- Ten interfejs API obsługuje obecnie tylko dostęp użytkowników, w przypadku których partnerzy muszą pełnić jedną z następujących ról: Administrator globalny, Agent administracyjny lub Agent sprzedaży.

## <a name="details"></a>Szczegóły

- Funkcja Current zwraca tylko dane dotyczące zaktualizowanych nowych produktów opartych na licencjach handlowych.
- Bieżące ceny obejmują produkty dostępne w bieżącym miesiącu do daty wywołania interfejsu API. Poprzednie miesiące zawierają datę ostatniego dnia wybranego miesiąca.
- Ta metoda zwraca dane jako strumień plików. Strumień plików jest plikiem .csv lub skompresowaną wersją pliku zip .csv. Poniżej znajdują się szczegółowe informacje na temat żądania skompresowanych plików.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Pobierz** | https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value |

### <a name="uri-filter-parameters"></a>Parametry filtru URI

Użyj następujących parametrów filtru.

| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Month (Miesiąc)| ciąg   | Nie | Wymagany arkusz cen musi być zgodny z RRRRM. |

### <a name="request-headers"></a>Nagłówki żądań

- Aby uzyskać więcej informacji, zobacz [Nagłówki REST](headers.md) partnerów.

Oprócz powyższych nagłówków pliki cenowe mogą być pobierane jako skompresowane, co skraca czas pobierania i przepustowości. Domyślnie pliki nie są kompresowane. Aby uzyskać skompresowane wersje plików, możesz dołączyć poniżej wartość nagłówka. Należy pamiętać, że skompresowane arkusze są dostępne tylko od kwietnia 2020 r., a wszystkie arkusze sprzed kwietnia 2020 r. są dostępne tylko jako nieskompresowane.

| Nagłówek                   | Typ wartości     | Wartość | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| ciąg   | Deflate| Opcjonalny. Jeśli pominięty strumień plików nie jest kompresowany.       |

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca macierz oferty jako strumień plików. Strumień plików jest plikiem .csv lub skompresowaną wersją pliku zip .csv.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=updatedoffice.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","ProvisioningId","ProvisioningString","MinLicenses","MaxLicenses","AssetOwnershipLimit","AssetOwnershipLimitType","ProductSkuPreRequisites","ProductSkuConversion","Description","AllowedCountries" 
"Microsoft 365 Business Basic","CFQ7TTC0LH18","0001","Microsoft 365 Business Basic","3b555118-da6a-4418-894f-7df1e2096870","O365_BUSINESS_ESSENTIALS","1","300","2","ConcurrentCount","","CFQ7TTC0LDPB/0001,CFQ7TTC0LF8Q/0001","Best for businesses that need professional...","AD;AE;AF;AG;AI;AL;AM;AO..."
======= Truncated ==============

```
