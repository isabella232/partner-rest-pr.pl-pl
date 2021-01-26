---
title: Utworzenie polecenia
description: Utwórz niezależne lub udostępnione odwołania w interfejsie API partnera.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770492"
---
# <a name="create-a-referral"></a>Utworzenie polecenia

Dotyczy:

- Interfejs API partnera

W tym temacie wyjaśniono, jak utworzyć odwołanie. Istnieją dwa typy [odwołań](referral-resources.md#referraltype):

1. Niezależne: gdzie odwołanie jest widoczne dla jednego partnera.
2. Udostępnione: gdzie odwołanie jest widoczne dla dwóch stron, które współpracują ze sobą. Na przykład jeśli firma Microsoft i partner współpracują ze sobą w ramach transakcji współsprzedaży, odwołanie może być współużytkowane przez obie strony. Aby uzyskać więcej informacji, zobacz sekcję [Tworzenie udostępnionej referencji](#create-a-shared-referral).

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                  |
|---------|--------------------------------------------------------------|
| **POUBOJOWEGO** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a>Nagłówki żądań

- Aby uzyskać więcej informacji, zobacz [nagłówki REST interfejsu API partnera](headers.md) .

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano właściwości [odwołania](referral-resources.md) w treści żądania dla zupełnie nowego odwołania.

| Właściwość            | Typ                                                                 | Opis                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Nazwa                | ciąg                                                               | Nazwa odwołania.                                                                                            |
| ExternalReferenceId | ciąg                                                               | Zewnętrzny identyfikator odwołania. Na przykład Twój własny identyfikator klienta Dynamics 365 lub identyfikatora szansy sprzedaży.                   |
| Stan              | [ReferralStatus](referral-resources.md#referralstatus)               | [Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan odwołania.          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | [Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi podstan odwołania.       |
| StatusReason        | ciąg                                                               | Opisowy komunikat o stanie. Na przykład Wyjaśnij, dlaczego odwołanie zostało utracone.                            |
| — Odwołanie        | [— Odwołanie](referral-resources.md#referraltype)                   | Reprezentuje typ odwołania. **Wymagane.**                                                                                        |
| Kwalifikacja       | [ReferralQualification](referral-resources.md#referralqualification) | Reprezentuje jakość odwołania.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Informacje kontaktowe klienta.  **Wymagane.**                                                                                      |
| Wyrażanie zgody             | [Wyrażanie zgody](referral-resources.md#consent)                             | Flagi zgody na udostępnianie informacji innym organizacjom i Zezwalanie na kontakt z użytkownikami. **Wymagane.**               |
| Szczegóły             | [ReferralDetails](referral-resources.md#referraldetails)             | Szczegóły klienta, notatki, wartość transakcji, Data zamknięcia waluty. **Wymagane.**                                                           |
| Zespół                | [Członek](referral-resources.md#member)                               | Reprezentuje użytkowników w organizacjach, które są zaangażowane w zaangażowanie partnerskie.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera. |
| Cel         | [ReferralTarget](referral-resources.md#target)        | Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera.  |

#### <a name="status--substatus-transition-states"></a>Stan przejścia & stanu Substatus

| Stan | Dozwolone przejście stanu | Dozwolony stan Substatus            |
|--------|---------------------------|------------------------------|
| Nowy    | Nowy, aktywny, zamknięty       | Oczekiwanie, odebrano            |
| Aktywna | Aktywne, zamknięte            | Zaakceptowano                     |
| Zamknięty | Zamknięty                    | Wygrane, utracone, odrzucone, wygasłe |

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [odwołania](referral-resources.md) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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

## <a name="create-a-shared-referral"></a>Utwórz odwołanie udostępnione

Istnieją dwa kroki umożliwiające utworzenie odwołania do **udostępnionego** [typu odwołania](referral-resources.md#referraltype).

1. [Utwórz udostępnione odwołanie](#create-your-referral)
2. [Utwórz połączone odwołanie dla drugiej strony](#create-a-connected-referral)

Poniższy wykres przepływu ilustruje te dwa kroki tworzenia udostępnionego odwołania.

![Wykres przepływu przedstawiający udostępnione odwołanie z 2 odwołaniami połączonymi za pomocą interfejsu API partnera firmy Microsoft](../images/SharedReferral.png)

### <a name="create-your-referral"></a>Utwórz odwołanie

1. Utwórz odwołanie z atrybutem [Referrtype](referral-resources.md#referraltype) ustawionym na wartość Shared.
2. Skopiuj **engagementId** z odpowiedzi zwracanej.

Przykład [ReferralTarget](referral-resources.md#target) do odwołania

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a>Utwórz połączone odwołanie

1. Utwórz inne odwołanie do firmy Microsoft.
2. Uwzględnij **enagementId** z odwołania, aby były powiązane ze sobą.

Przykład [ReferralTarget](referral-resources.md#target) dla odwołania firmy Microsoft

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```