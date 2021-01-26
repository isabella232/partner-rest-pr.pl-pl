---
title: Pobieranie potencjalnego klienta lub szansy sprzedaży według identyfikatora
description: Uzyskaj potencjalny klient lub szansę sprzedaży według identyfikatora.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcfaea393afc6a9d09946b4c31b7168ba26aa255
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770533"
---
# <a name="get-a-lead-or-opportunity-by-id"></a>Pobieranie potencjalnego klienta lub szansy sprzedaży według identyfikatora

Dotyczy:

- Interfejs API partnera

W tym temacie wyjaśniono, jak uzyskać potencjalną szansę lub okazję do sprzedaży według identyfikatora.

> [!Note]
> Potencjalni klienci z komercyjnego rynku firmy Microsoft (Azure Marketplace i AppSource) nie są obsługiwani. 

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.
- Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą znajdować się w jednej z następujących ról: Administrator globalny, administrator odwołania lub użytkownik referencyjny.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Pobierz** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a>Parametr URI


| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | ciąg   | Tak       | Unikatowy identyfikator dla możliwości potencjalnego klienta lub współsprzedaży       |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id} HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera [potencjalny klient lub szansę](referral-resources.md) pasującą do identyfikatora.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera [kod stanu HTTP](error-codes.md) , który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.

### <a name="response-example"></a>Przykład odpowiedzi

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
    "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",
    "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "createdDateTime": "2020-10-30T21:03:00.0000000Z",
    "updatedDateTime": "2020-10-30T21:03:00.0000000Z",
    "status": "New",
    "substatus": "Pending",
    "qualification": "Direct",
    "type": "Independent",
    "direction": "Incoming",
    "customerProfile": {
      "name": "Fabrikam Customer Inc",
      "address": {
        "addressLine1": "One Microsoft Way",
        "addressLine2": "",
        "city": "Redmond",
        "state": "WA",
        "postalCode": "98052",
        "country": "US"
      }
    },
    "details": {
      "notes": "We are interested in deploying Microsoft 365 and are looking forsupport in training our employees. Can you help?",
      "dealValue": 10000,
      "currency": "USD",
      "closingDateTime": "2020-12-01T00:00:00Z",
      "requirements": {
          "industries": [ { "id": "Education" } ],
          "products": [ { "id": "Microsoft365" } ],
          "services": [ { "id": "LearningAndCertification" } ],
          "solutions": [ { "id": "SOL-Microsoft365", "name": "Microsoft365" }
        ]
      }
    },
    "links": {
      "relatedReferrals": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
        "method": "GET"
      },
      "self": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referralsc5fbb3b6-be74-4795-9fb5-4324c73fed37",
        "method": "GET"
      }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```

> [!Note]
> Pola w powyższym przykładzie illustratration nie są wyczerpujące. Rzeczywista odpowiedź interfejsu API zawiera więcej pól, takich jak zespoły klienta i partnera. Aby uzyskać pełną listę obsługiwanych pól, zobacz [odwołania do zasobów](referral-resources.md).