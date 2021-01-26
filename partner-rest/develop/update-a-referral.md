---
title: Aktualizowanie potencjalnego klienta lub szansy sprzedaży (przestarzałe)
description: Umożliwia zaktualizowanie szczegółów potencjalnego klienta lub szansy sprzedaży. Ta metoda aktualizowania potencjalnego klienta lub szansy sprzedaży jest przestarzała i recommmend zamiast tego użycie wywołania PATCH.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770545"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a>Aktualizowanie potencjalnego klienta lub szansy sprzedaży (przestarzałe)

Dotyczy:

- Interfejs API partnera

W tym temacie wyjaśniono, jak zaktualizować szczegóły potencjalnego klienta lub szansy sprzedaży, takie jak wartość transakcji, Szacowana data zamknięcia lub zarządzać etapami sprzedaży między innymi szczegółami. 


> [!IMPORTANT]
Ta metoda aktualizowania potencjalnego klienta lub szansy sprzedaży jest przestarzała i recommmend zamiast tego użycie wywołania [patch](patch-a-referral.md) .

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.
- Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą znajdować się w jednej z następujących ról: Administrator globalny, administrator odwołania lub użytkownik referencyjny.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                       |
|---------|-------------------------------------------------------------------|
| **PUT** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a>Nagłówki żądań

- Aby uzyskać więcej informacji, zobacz [nagłówki REST interfejsu API partnera](headers.md).

> [!IMPORTANT]
> Pamiętaj, aby ustawić nagłówek **if-Match** .

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano właściwości [odwołania](referral-resources.md) w treści żądania.

| Właściwość            | Typ                                                                 | Opis                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Id                  | ciąg                                                               | Identyfikator dla tego odwołania.                                                                                            |
| EngagementId        | ciąg                                                               | EngagementID dla tego odwołania. Wiele odwołań może być skojarzonych z pojedynczym EngagementID                    |
| Nazwa                | ciąg                                                               | Nazwa odwołania.                                                                                            |
| ExternalReferenceId | ciąg                                                               | Zewnętrzny identyfikator odwołania. Przykład: Zachowaj własny identyfikator systemu Dynamics 365 potencjalnego klienta/szansy sprzedaży                    |
| CreatedDateTime     | ciąg w formacie daty i godziny czasu UTC                                       | Data utworzenia odwołania.                                                                                   |
| UpdatedDateTime     | ciąg w formacie daty i godziny czasu UTC                                       | Data ostatniej aktualizacji odwołania.                                                                              |
| ExpirationDateTime  | ciąg w formacie daty i godziny czasu UTC                                       | Data wygaśnięcia odwołania.                                                                                   |
| Stan              | [ReferralStatus](referral-resources.md#referralstatus)               | [Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan odwołania.          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | [Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan podrzędny odwołania.      |
| StatusReason        | ciąg                                                               | Opisowy komunikat o stanie. Na przykład Wyjaśnij, dlaczego odwołanie zostało utracone.                              |
| — Odwołanie        | [— Odwołanie](referral-resources.md#referraltype)                   | Reprezentuje typ odwołania.                                                                                        |
| Kwalifikacja       | [ReferralQualification](referral-resources.md#referralqualification) | Reprezentuje jakość odwołania.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Informacje kontaktowe klienta.                                                                                        |
| Wyrażanie zgody             | [Wyrażanie zgody](referral-resources.md#consent)                             | Flagi zgody na udostępnianie informacji innym organizacjom i Zezwalanie na kontakt z użytkownikami.                |
| Szczegóły             | [ReferralDetails](referral-resources.md#referraldetails)             | Szczegóły klienta, notatki, wartość transakcji, Data zamknięcia waluty.                                                          |
| Zespół                | [Członek](referral-resources.md#member)                               | Reprezentuje użytkowników w organizacjach, które są zaangażowane w zaangażowanie partnerskie.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera. |
| Cel         | [ReferralTarget](referral-resources.md#target)        | Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera.  |

### <a name="status-and-substatus-transition-states"></a>Stany przejścia stanu i podstanu

| Stan | Dozwolone przejście stanu | Dozwolony stan Substatus            |
|--------|---------------------------|------------------------------|
| Nowy    | Nowy, aktywny, zamknięty       | Oczekiwanie, odebrano            |
| Aktywna | Aktywne, zamknięte            | Zaakceptowano                     |
| Zamknięty | Zamknięty                    | Wygrane, utracone, odrzucone, wygasłe |

### <a name="request-example"></a>Przykład żądania

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> Usuń `"links": { }` obiekt z zasobu Put.

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [odwołania](referral-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```