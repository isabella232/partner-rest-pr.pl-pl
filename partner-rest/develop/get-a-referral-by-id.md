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
# <a name="get-a-lead-or-opportunity-by-id"></a><span data-ttu-id="51803-103">Pobieranie potencjalnego klienta lub szansy sprzedaży według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="51803-103">Get a lead or opportunity by Id</span></span>

<span data-ttu-id="51803-104">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="51803-104">Applies to:</span></span>

- <span data-ttu-id="51803-105">Interfejs API partnera</span><span class="sxs-lookup"><span data-stu-id="51803-105">Partner API</span></span>

<span data-ttu-id="51803-106">W tym temacie wyjaśniono, jak uzyskać potencjalną szansę lub okazję do sprzedaży według identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="51803-106">This topic explains how to get a lead or co-sell opportunity by Id.</span></span>

> [!Note]
> <span data-ttu-id="51803-107">Potencjalni klienci z komercyjnego rynku firmy Microsoft (Azure Marketplace i AppSource) nie są obsługiwani.</span><span class="sxs-lookup"><span data-stu-id="51803-107">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="51803-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="51803-108">Prerequisites</span></span>

- <span data-ttu-id="51803-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="51803-109">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="51803-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="51803-110">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="51803-111">Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą znajdować się w jednej z następujących ról: Administrator globalny, administrator odwołania lub użytkownik referencyjny.</span><span class="sxs-lookup"><span data-stu-id="51803-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="51803-112">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="51803-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="51803-113">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="51803-113">Request syntax</span></span>

| <span data-ttu-id="51803-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="51803-114">Method</span></span>   | <span data-ttu-id="51803-115">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="51803-115">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="51803-116">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="51803-116">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a><span data-ttu-id="51803-117">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="51803-117">URI parameter</span></span>


| <span data-ttu-id="51803-118">Nazwa</span><span class="sxs-lookup"><span data-stu-id="51803-118">Name</span></span>                   | <span data-ttu-id="51803-119">Typ</span><span class="sxs-lookup"><span data-stu-id="51803-119">Type</span></span>     | <span data-ttu-id="51803-120">Wymagane</span><span class="sxs-lookup"><span data-stu-id="51803-120">Required</span></span> | <span data-ttu-id="51803-121">Opis</span><span class="sxs-lookup"><span data-stu-id="51803-121">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="51803-122">Id</span><span class="sxs-lookup"><span data-stu-id="51803-122">Id</span></span>                      | <span data-ttu-id="51803-123">ciąg</span><span class="sxs-lookup"><span data-stu-id="51803-123">string</span></span>   | <span data-ttu-id="51803-124">Tak</span><span class="sxs-lookup"><span data-stu-id="51803-124">Yes</span></span>       | <span data-ttu-id="51803-125">Unikatowy identyfikator dla możliwości potencjalnego klienta lub współsprzedaży</span><span class="sxs-lookup"><span data-stu-id="51803-125">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="51803-126">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="51803-126">Request headers</span></span>

<span data-ttu-id="51803-127">Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="51803-127">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="51803-128">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="51803-128">Request body</span></span>

<span data-ttu-id="51803-129">Brak.</span><span class="sxs-lookup"><span data-stu-id="51803-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="51803-130">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="51803-130">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id} HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="51803-131">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="51803-131">REST response</span></span>

<span data-ttu-id="51803-132">Jeśli to się powiedzie, treść odpowiedzi zawiera [potencjalny klient lub szansę](referral-resources.md) pasującą do identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="51803-132">If successful, the response body contains the [lead or opportunity](referral-resources.md) matching the Id.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="51803-133">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="51803-133">Response success and error codes</span></span>

<span data-ttu-id="51803-134">Każda odpowiedź zawiera [kod stanu HTTP](error-codes.md) , który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="51803-134">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="51803-135">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="51803-135">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="51803-136">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="51803-136">Response example</span></span>

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
> <span data-ttu-id="51803-137">Pola w powyższym przykładzie illustratration nie są wyczerpujące.</span><span class="sxs-lookup"><span data-stu-id="51803-137">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="51803-138">Rzeczywista odpowiedź interfejsu API zawiera więcej pól, takich jak zespoły klienta i partnera.</span><span class="sxs-lookup"><span data-stu-id="51803-138">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="51803-139">Aby uzyskać pełną listę obsługiwanych pól, zobacz [odwołania do zasobów](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="51803-139">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>