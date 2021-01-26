---
title: Pobieranie listy potencjalnych klientów i szans sprzedaży
description: Jak uzyskać listę potencjalnych klientów i możliwości przy użyciu interfejsu API partnera.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 46243f8484a8068827e24e1d03f39ffddade1dbf
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770528"
---
# <a name="get-the-list-of-leads-and-opportunities"></a>Pobieranie listy potencjalnych klientów i szans sprzedaży

Dotyczy:

- Interfejs API partnera

 W tym temacie wyjaśniono, jak uzyskać listę potencjalnych klientów otrzymanych od strony dostawcy rozwiązań firmy Microsoft i od innych partnerów otrzymywać możliwości wspólnej sprzedaży. Spowoduje to również pobranie listy możliwości wspólnej sprzedaży lub potoku utworzonych przez organizację.

> [!Note]
> Potencjalni klienci z komercyjnego rynku firmy Microsoft (Azure Marketplace i AppSource) nie są obsługiwani.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.
- Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą znajdować się w jednej z następujących ról: Administrator globalny, administrator odwołania lub użytkownik referencyjny.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                    |
|:--------|:---------------------------------------------------------------|
| **Pobierz** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a>Obsługiwane operacje OData

| Nazwa     | Opis     | Wymagane    | Przykład                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| $select  | Wybiera pola  | Nie          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| $filter  | Wyniki filtrów | Zalecane | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| $orderby | Wyniki zamówień  | Zalecane | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a>Obsługiwane parametry OrderBy

Użyj następujących $orderby parametrów, aby posortować listę potencjalnych klientów i szans

| Nazwa            | Typ     | Opis                                       |
|:----------------|:---------|:--------------------------------------------------|
| createdDateTime | DateTime | Data i godzina utworzenia potencjalnego klienta lub szansy sprzedaży |
| updatedDateTime | DateTime | Aktualizuj datę i godzinę potencjalnego klienta lub szansy sprzedaży   |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [potencjalnych klientów i/lub szanse sprzedaży](referral-resources.md).

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera [kod stanu HTTP](error-codes.md) , który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.

### <a name="response-example"></a>Przykład odpowiedzi

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
  "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
  "@odata.count": 1,
  "value": [
    {
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
        "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
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
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
          "method": "GET"
        },
        "self": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
          "method": "GET"
        }
      }
    }
  ],
  "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxX"
}
```

Użyj, `@odata.nextLink` Aby uzyskać następną stronę wyników.

> [!Note]
> Pola w powyższym przykładzie illustratration nie są wyczerpujące. Rzeczywista odpowiedź interfejsu API zawiera więcej pól, takich jak zespoły klienta i partnera. Aby uzyskać pełną listę obsługiwanych pól, zobacz [odwołania do zasobów](referral-resources.md).

## <a name="sample-requests"></a>Przykładowe żądania

1. Pobiera 10 najważniejszych możliwości przychodzącego współsprzedaży. Żądanie będzie pobierać możliwości zainicjowane przez przedstawiciela handlowego firmy Microsoft lub innego partnera, zapraszając swoją organizację do wzięcia udziału w obsprzedaży.
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. Pobiera najnowsze potencjalni klienci i szanse, do których nie udzielono odpowiedzi.  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > Jeśli nie odpowiadasz na potencjalnego klienta lub szansę sprzedaży w wyznaczonym czasie (obecnie 14 dni), będziemy archiwizować ją jako wygasłą i powiadomić firmę Microsoft lub partnera, który wysłał tę możliwość.

3. Pobiera najnowsze aktywne możliwości wspólnej sprzedaży inicjowane przez Twoją organizację i pracujące nad nim przez określonego sprzedającego.
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```