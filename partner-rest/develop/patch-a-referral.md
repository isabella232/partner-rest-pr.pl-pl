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
# <a name="update-a-lead-or-opportunity"></a><span data-ttu-id="d65c7-103">Aktualizowanie potencjalnego klienta lub szansy sprzedaży</span><span class="sxs-lookup"><span data-stu-id="d65c7-103">Update a lead or opportunity</span></span>

<span data-ttu-id="d65c7-104">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="d65c7-104">Applies to:</span></span>

- <span data-ttu-id="d65c7-105">Interfejs API partnera</span><span class="sxs-lookup"><span data-stu-id="d65c7-105">Partner API</span></span>

<span data-ttu-id="d65c7-106">W tym temacie wyjaśniono, jak zaktualizować szczegóły potencjalnego klienta lub szansy sprzedaży, takie jak wartość transakcji, Szacowana data zamknięcia lub zarządzać etapami sprzedaży między innymi szczegółami.</span><span class="sxs-lookup"><span data-stu-id="d65c7-106">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d65c7-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d65c7-107">Prerequisites</span></span>

- <span data-ttu-id="d65c7-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d65c7-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="d65c7-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d65c7-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="d65c7-110">Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą znajdować się w jednej z następujących ról: Administrator globalny, administrator odwołania lub użytkownik referencyjny.</span><span class="sxs-lookup"><span data-stu-id="d65c7-110">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="d65c7-111">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d65c7-111">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d65c7-112">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d65c7-112">Request syntax</span></span>

| <span data-ttu-id="d65c7-113">Metoda</span><span class="sxs-lookup"><span data-stu-id="d65c7-113">Method</span></span>  | <span data-ttu-id="d65c7-114">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d65c7-114">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="d65c7-115">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="d65c7-115">**PATCH**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a><span data-ttu-id="d65c7-116">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d65c7-116">URI parameter</span></span>


| <span data-ttu-id="d65c7-117">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d65c7-117">Name</span></span>                   | <span data-ttu-id="d65c7-118">Typ</span><span class="sxs-lookup"><span data-stu-id="d65c7-118">Type</span></span>     | <span data-ttu-id="d65c7-119">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d65c7-119">Required</span></span> | <span data-ttu-id="d65c7-120">Opis</span><span class="sxs-lookup"><span data-stu-id="d65c7-120">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="d65c7-121">Id</span><span class="sxs-lookup"><span data-stu-id="d65c7-121">Id</span></span>                      | <span data-ttu-id="d65c7-122">ciąg</span><span class="sxs-lookup"><span data-stu-id="d65c7-122">string</span></span>   | <span data-ttu-id="d65c7-123">Tak</span><span class="sxs-lookup"><span data-stu-id="d65c7-123">Yes</span></span>       | <span data-ttu-id="d65c7-124">Unikatowy identyfikator dla możliwości potencjalnego klienta lub współsprzedaży</span><span class="sxs-lookup"><span data-stu-id="d65c7-124">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="d65c7-125">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d65c7-125">Request headers</span></span>

<span data-ttu-id="d65c7-126">Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="d65c7-126">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="d65c7-127">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d65c7-127">Request body</span></span>

<span data-ttu-id="d65c7-128">Treść żądania jest zgodna z formatem [poprawki JSON](https://tools.ietf.org/html/rfc6902) .</span><span class="sxs-lookup"><span data-stu-id="d65c7-128">The request body follows the [Json Patch](https://tools.ietf.org/html/rfc6902) format.</span></span> <span data-ttu-id="d65c7-129">Dokument poprawki JSON zawiera tablicę operacji.</span><span class="sxs-lookup"><span data-stu-id="d65c7-129">A JSON Patch document has an array of operations.</span></span> <span data-ttu-id="d65c7-130">Każda operacja identyfikuje określony typ zmiany.</span><span class="sxs-lookup"><span data-stu-id="d65c7-130">Each operation identifies a particular type of change.</span></span> <span data-ttu-id="d65c7-131">Przykłady takich zmian obejmują dodanie elementu tablicy lub zastępowanie wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="d65c7-131">Examples of such changes include adding an array element or replacing a property value.</span></span>

> [!Important]
> <span data-ttu-id="d65c7-132">Interfejs API obecnie obsługuje tylko `replace` operacje i `add` .</span><span class="sxs-lookup"><span data-stu-id="d65c7-132">The API currently only supports the `replace` and `add` operations.</span></span>

### <a name="request-example"></a><span data-ttu-id="d65c7-133">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d65c7-133">Request example</span></span>

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
> <span data-ttu-id="d65c7-134">Jeśli zostanie przesłany nagłówek **if-Match** , będzie on używany na potrzeby kontroli współbieżności.</span><span class="sxs-lookup"><span data-stu-id="d65c7-134">If the **If-Match** header is passed, it will be used for concurrency control.</span></span>

## <a name="rest-response"></a><span data-ttu-id="d65c7-135">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d65c7-135">REST Response</span></span>

<span data-ttu-id="d65c7-136">Jeśli to się powiedzie, treść odpowiedzi zawiera zaktualizowany [potencjalny klient lub szansę sprzedaży](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d65c7-136">If successful, the response body contains the updated [lead or opportunity](referral-resources.md).</span></span>


### <a name="response-success-and-error-codes"></a><span data-ttu-id="d65c7-137">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d65c7-137">Response success and error codes</span></span>

<span data-ttu-id="d65c7-138">Każda odpowiedź zawiera [kod stanu HTTP](error-codes.md) , który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="d65c7-138">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d65c7-139">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d65c7-139">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="d65c7-140">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d65c7-140">Response example</span></span>

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> <span data-ttu-id="d65c7-141">Treść odpowiedzi zależy od **preferowanego** nagłówka.</span><span class="sxs-lookup"><span data-stu-id="d65c7-141">The response body depends on the **Prefer** header.</span></span> <span data-ttu-id="d65c7-142">W przypadku pominięcia wartości nagłówka w żądaniu treść odpowiedzi jest pusta z kodem stanu HTTP 204.</span><span class="sxs-lookup"><span data-stu-id="d65c7-142">If the header value is omitted in the request, the response body is empty with a HTTP Status code 204.</span></span> <span data-ttu-id="d65c7-143">Dodaj `Prefer: return=representation` do nagłówka, aby uzyskać zaktualizowany potencjalny klient lub szansę sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="d65c7-143">Add `Prefer: return=representation` to the header to get the updated lead or opportunity.</span></span>

## <a name="sample-requests"></a><span data-ttu-id="d65c7-144">Przykładowe żądania</span><span class="sxs-lookup"><span data-stu-id="d65c7-144">Sample requests</span></span>

1. <span data-ttu-id="d65c7-145">Aktualizuje wartość transakcji dla szansy sprzedaży do 10000 i aktualizuje uwagi.</span><span class="sxs-lookup"><span data-stu-id="d65c7-145">Updates the deal value for the opportunity to 10000 and updates the notes.</span></span> <span data-ttu-id="d65c7-146">Brak kontroli współbieżności ze względu na absense `If-Match` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="d65c7-146">There are no concurrency checks because of the absense of the `If-Match` header.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. <span data-ttu-id="d65c7-147">Aktualizuje stan potencjalnego klienta lub szansy sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="d65c7-147">Updates the status of a lead or opportunity to Won.</span></span>
    
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
    > <span data-ttu-id="d65c7-148">`status`Pola i `substatus` powinny być zgodne z dozwolonym zestawem wartości przejścia, zgodnie z opisem w [tym miejscu](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d65c7-148">The `status` and `substatus` fields should conform to the allowed set of transition values as described [here](referral-resources.md).</span></span>

3. <span data-ttu-id="d65c7-149">Dodaje nowego członka z organizacji do zespołu potencjalny klient lub szansa sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="d65c7-149">Adds a new member from your organization to the lead or opportunity team.</span></span> <span data-ttu-id="d65c7-150">Odpowiedź będzie zawierać zaktualizowany potencjalny klient lub szansę z powodu obecności `Prefer: return=representation` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="d65c7-150">The response will contain the updated lead or opportunity because of the presence of the `Prefer: return=representation` header.</span></span>

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
