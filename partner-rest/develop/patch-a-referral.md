---
title: Aktualizowanie potencjalnego klienta lub szansy sprzedaży
description: Umożliwia zaktualizowanie szczegółów potencjalnego klienta lub szansy sprzedaży.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: abfe7308f46cd65b9358b369f6fa05bcca4c1df2
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770540"
---
# <a name="update-a-lead-or-opportunity"></a>Aktualizowanie potencjalnego klienta lub szansy sprzedaży

Dotyczy:

- Interfejs API partnera

W tym temacie wyjaśniono, jak zaktualizować szczegóły potencjalnego klienta lub szansy sprzedaży, takie jak wartość transakcji, Szacowana data zamknięcia lub zarządzać etapami sprzedaży między innymi szczegółami.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md). Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.
- Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą znajdować się w jednej z następujących ról: Administrator globalny, administrator odwołania lub użytkownik referencyjny.

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                       |
|---------|-------------------------------------------------------------------|
| **WYSŁANA** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a>Parametr URI


| Nazwa                   | Typ     | Wymagane | Opis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | ciąg   | Tak       | Unikatowy identyfikator dla możliwości potencjalnego klienta lub współsprzedaży       |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .

### <a name="request-body"></a>Treść żądania

Treść żądania jest zgodna z formatem [poprawki JSON](https://tools.ietf.org/html/rfc6902) . Dokument poprawki JSON zawiera tablicę operacji. Każda operacja identyfikuje określony typ zmiany. Przykłady takich zmian obejmują dodanie elementu tablicy lub zastępowanie wartości właściwości.

> [!Important]
> Interfejs API obecnie obsługuje tylko `replace` operacje i `add` .

### <a name="request-example"></a>Przykład żądania

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> Jeśli zostanie przesłany nagłówek **if-Match** , będzie on używany na potrzeby kontroli współbieżności.

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera zaktualizowany [potencjalny klient lub szansę sprzedaży](referral-resources.md).


### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera [kod stanu HTTP](error-codes.md) , który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.

### <a name="response-example"></a>Przykład odpowiedzi

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> Treść odpowiedzi zależy od **preferowanego** nagłówka. W przypadku pominięcia wartości nagłówka w żądaniu treść odpowiedzi jest pusta z kodem stanu HTTP 204. Dodaj `Prefer: return=representation` do nagłówka, aby uzyskać zaktualizowany potencjalny klient lub szansę sprzedaży.

## <a name="sample-requests"></a>Przykładowe żądania

1. Aktualizuje wartość transakcji dla szansy sprzedaży do 10000 i aktualizuje uwagi. Brak kontroli współbieżności ze względu na absense `If-Match` nagłówka.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. Aktualizuje stan potencjalnego klienta lub szansy sprzedaży.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > `status`Pola i `substatus` powinny być zgodne z dozwolonym zestawem wartości przejścia, zgodnie z opisem w [tym miejscu](referral-resources.md).

3. Dodaje nowego członka z organizacji do zespołu potencjalny klient lub szansa sprzedaży. Odpowiedź będzie zawierać zaktualizowany potencjalny klient lub szansę z powodu obecności `Prefer: return=representation` nagłówka.

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```
