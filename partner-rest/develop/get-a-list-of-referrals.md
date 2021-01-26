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
# <a name="get-the-list-of-leads-and-opportunities"></a><span data-ttu-id="6aa78-103">Pobieranie listy potencjalnych klientów i szans sprzedaży</span><span class="sxs-lookup"><span data-stu-id="6aa78-103">Get the list of leads and opportunities</span></span>

<span data-ttu-id="6aa78-104">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="6aa78-104">Applies to:</span></span>

- <span data-ttu-id="6aa78-105">Interfejs API partnera</span><span class="sxs-lookup"><span data-stu-id="6aa78-105">Partner API</span></span>

 <span data-ttu-id="6aa78-106">W tym temacie wyjaśniono, jak uzyskać listę potencjalnych klientów otrzymanych od strony dostawcy rozwiązań firmy Microsoft i od innych partnerów otrzymywać możliwości wspólnej sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="6aa78-106">This topic explains how to get the list of leads received from Microsoft solution provider page and co-sell opportunities received from Microsoft sellers or other partners.</span></span> <span data-ttu-id="6aa78-107">Spowoduje to również pobranie listy możliwości wspólnej sprzedaży lub potoku utworzonych przez organizację.</span><span class="sxs-lookup"><span data-stu-id="6aa78-107">This will also fetch the list of co-sell opportunities or pipeline deals created by your organization.</span></span>

> [!Note]
> <span data-ttu-id="6aa78-108">Potencjalni klienci z komercyjnego rynku firmy Microsoft (Azure Marketplace i AppSource) nie są obsługiwani.</span><span class="sxs-lookup"><span data-stu-id="6aa78-108">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6aa78-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6aa78-109">Prerequisites</span></span>

- <span data-ttu-id="6aa78-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6aa78-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="6aa78-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6aa78-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="6aa78-112">Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą znajdować się w jednej z następujących ról: Administrator globalny, administrator odwołania lub użytkownik referencyjny.</span><span class="sxs-lookup"><span data-stu-id="6aa78-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="6aa78-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6aa78-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6aa78-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6aa78-114">Request syntax</span></span>

| <span data-ttu-id="6aa78-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="6aa78-115">Method</span></span>  | <span data-ttu-id="6aa78-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6aa78-116">Request URI</span></span>                                                    |
|:--------|:---------------------------------------------------------------|
| <span data-ttu-id="6aa78-117">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="6aa78-117">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a><span data-ttu-id="6aa78-118">Obsługiwane operacje OData</span><span class="sxs-lookup"><span data-stu-id="6aa78-118">Supported OData operations</span></span>

| <span data-ttu-id="6aa78-119">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6aa78-119">Name</span></span>     | <span data-ttu-id="6aa78-120">Opis</span><span class="sxs-lookup"><span data-stu-id="6aa78-120">Description</span></span>     | <span data-ttu-id="6aa78-121">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6aa78-121">Required</span></span>    | <span data-ttu-id="6aa78-122">Przykład</span><span class="sxs-lookup"><span data-stu-id="6aa78-122">Example</span></span>                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6aa78-123">$select</span><span class="sxs-lookup"><span data-stu-id="6aa78-123">$select</span></span>  | <span data-ttu-id="6aa78-124">Wybiera pola</span><span class="sxs-lookup"><span data-stu-id="6aa78-124">Selects fields</span></span>  | <span data-ttu-id="6aa78-125">Nie</span><span class="sxs-lookup"><span data-stu-id="6aa78-125">No</span></span>          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| <span data-ttu-id="6aa78-126">$filter</span><span class="sxs-lookup"><span data-stu-id="6aa78-126">$filter</span></span>  | <span data-ttu-id="6aa78-127">Wyniki filtrów</span><span class="sxs-lookup"><span data-stu-id="6aa78-127">Filters results</span></span> | <span data-ttu-id="6aa78-128">Zalecane</span><span class="sxs-lookup"><span data-stu-id="6aa78-128">Recommended</span></span> | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| <span data-ttu-id="6aa78-129">$orderby</span><span class="sxs-lookup"><span data-stu-id="6aa78-129">$orderby</span></span> | <span data-ttu-id="6aa78-130">Wyniki zamówień</span><span class="sxs-lookup"><span data-stu-id="6aa78-130">Orders results</span></span>  | <span data-ttu-id="6aa78-131">Zalecane</span><span class="sxs-lookup"><span data-stu-id="6aa78-131">Recommended</span></span> | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a><span data-ttu-id="6aa78-132">Obsługiwane parametry OrderBy</span><span class="sxs-lookup"><span data-stu-id="6aa78-132">Supported orderby parameters</span></span>

<span data-ttu-id="6aa78-133">Użyj następujących $orderby parametrów, aby posortować listę potencjalnych klientów i szans</span><span class="sxs-lookup"><span data-stu-id="6aa78-133">Use the following $orderby parameters to sort the list of leads and opportunities</span></span>

| <span data-ttu-id="6aa78-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6aa78-134">Name</span></span>            | <span data-ttu-id="6aa78-135">Typ</span><span class="sxs-lookup"><span data-stu-id="6aa78-135">Type</span></span>     | <span data-ttu-id="6aa78-136">Opis</span><span class="sxs-lookup"><span data-stu-id="6aa78-136">Description</span></span>                                       |
|:----------------|:---------|:--------------------------------------------------|
| <span data-ttu-id="6aa78-137">createdDateTime</span><span class="sxs-lookup"><span data-stu-id="6aa78-137">createdDateTime</span></span> | <span data-ttu-id="6aa78-138">DateTime</span><span class="sxs-lookup"><span data-stu-id="6aa78-138">DateTime</span></span> | <span data-ttu-id="6aa78-139">Data i godzina utworzenia potencjalnego klienta lub szansy sprzedaży</span><span class="sxs-lookup"><span data-stu-id="6aa78-139">Creation date and time of the lead or opportunity</span></span> |
| <span data-ttu-id="6aa78-140">updatedDateTime</span><span class="sxs-lookup"><span data-stu-id="6aa78-140">updatedDateTime</span></span> | <span data-ttu-id="6aa78-141">DateTime</span><span class="sxs-lookup"><span data-stu-id="6aa78-141">DateTime</span></span> | <span data-ttu-id="6aa78-142">Aktualizuj datę i godzinę potencjalnego klienta lub szansy sprzedaży</span><span class="sxs-lookup"><span data-stu-id="6aa78-142">Update date and time of the lead or opportunity</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="6aa78-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6aa78-143">Request headers</span></span>

<span data-ttu-id="6aa78-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="6aa78-144">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="6aa78-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6aa78-145">Request body</span></span>

<span data-ttu-id="6aa78-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="6aa78-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6aa78-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6aa78-147">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="6aa78-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6aa78-148">REST response</span></span>

<span data-ttu-id="6aa78-149">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [potencjalnych klientów i/lub szanse sprzedaży](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6aa78-149">If successful, the response body contains a collection of [leads and/or opportunities](referral-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6aa78-150">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6aa78-150">Response success and error codes</span></span>

<span data-ttu-id="6aa78-151">Każda odpowiedź zawiera [kod stanu HTTP](error-codes.md) , który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="6aa78-151">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6aa78-152">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6aa78-152">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="6aa78-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6aa78-153">Response example</span></span>

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

<span data-ttu-id="6aa78-154">Użyj, `@odata.nextLink` Aby uzyskać następną stronę wyników.</span><span class="sxs-lookup"><span data-stu-id="6aa78-154">Use the `@odata.nextLink` to get the next page of results.</span></span>

> [!Note]
> <span data-ttu-id="6aa78-155">Pola w powyższym przykładzie illustratration nie są wyczerpujące.</span><span class="sxs-lookup"><span data-stu-id="6aa78-155">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="6aa78-156">Rzeczywista odpowiedź interfejsu API zawiera więcej pól, takich jak zespoły klienta i partnera.</span><span class="sxs-lookup"><span data-stu-id="6aa78-156">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="6aa78-157">Aby uzyskać pełną listę obsługiwanych pól, zobacz [odwołania do zasobów](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6aa78-157">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>

## <a name="sample-requests"></a><span data-ttu-id="6aa78-158">Przykładowe żądania</span><span class="sxs-lookup"><span data-stu-id="6aa78-158">Sample requests</span></span>

1. <span data-ttu-id="6aa78-159">Pobiera 10 najważniejszych możliwości przychodzącego współsprzedaży.</span><span class="sxs-lookup"><span data-stu-id="6aa78-159">Gets the top 10 most recent inbound co-sell opportunities.</span></span> <span data-ttu-id="6aa78-160">Żądanie będzie pobierać możliwości zainicjowane przez przedstawiciela handlowego firmy Microsoft lub innego partnera, zapraszając swoją organizację do wzięcia udziału w obsprzedaży.</span><span class="sxs-lookup"><span data-stu-id="6aa78-160">The request will fetch opportunities initiated by a Microsoft sales representative or another partner, inviting your organization to participate in a co-selling activity.</span></span>
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. <span data-ttu-id="6aa78-161">Pobiera najnowsze potencjalni klienci i szanse, do których nie udzielono odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6aa78-161">Gets the most recent inbound leads and opportunities that have not been responded to.</span></span>  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > <span data-ttu-id="6aa78-162">Jeśli nie odpowiadasz na potencjalnego klienta lub szansę sprzedaży w wyznaczonym czasie (obecnie 14 dni), będziemy archiwizować ją jako wygasłą i powiadomić firmę Microsoft lub partnera, który wysłał tę możliwość.</span><span class="sxs-lookup"><span data-stu-id="6aa78-162">If you don't respond to a lead or opportunity within the allotted time (currently 14 days), we'll archive it as Expired and notify either Microsoft or the partner who sent you this opportunity.</span></span>

3. <span data-ttu-id="6aa78-163">Pobiera najnowsze aktywne możliwości wspólnej sprzedaży inicjowane przez Twoją organizację i pracujące nad nim przez określonego sprzedającego.</span><span class="sxs-lookup"><span data-stu-id="6aa78-163">Gets the most recent active co-sell opportunities initiated by your organization and being worked on by a specific seller.</span></span>
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```