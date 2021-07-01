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
# <a name="get-an-offer-matrix"></a><span data-ttu-id="1bc00-104">Uzyskiwanie macierzy ofert</span><span class="sxs-lookup"><span data-stu-id="1bc00-104">Get an offer matrix</span></span>

<span data-ttu-id="1bc00-105">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="1bc00-105">Applies to:</span></span>

- <span data-ttu-id="1bc00-106">interfejs API Partner</span><span class="sxs-lookup"><span data-stu-id="1bc00-106">Partner API</span></span>
- <span data-ttu-id="1bc00-107">Nowe środowisko handlowe M365/D365 w wersji Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="1bc00-107">The M365/D365 New Commerce experience technical preview.</span></span> <span data-ttu-id="1bc00-108">Poniższe zmiany dotyczące nowego handlu są obecnie dostępne tylko dla partnerów, którzy są częścią nowego rozwiązania handlowego M365/D365 w wersji Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="1bc00-108">The below New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

<span data-ttu-id="1bc00-109">W tym temacie wyjaśniono, jak uzyskać macierz ofert dla danego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="1bc00-109">This topic explains how to get an offer matrix for a given month.</span></span> <span data-ttu-id="1bc00-110">Macierz oferty zawiera właściwości i reguły zakupu dla produktów i jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="1bc00-110">The offer matrix includes properties and purchase rules for the products and skus.</span></span> <span data-ttu-id="1bc00-111">Ta metoda obsługuje filtry w celu uzyskania historii według miesięcy.</span><span class="sxs-lookup"><span data-stu-id="1bc00-111">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bc00-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1bc00-112">Prerequisites</span></span>

- <span data-ttu-id="1bc00-113">Poświadczenia zgodnie z opisem w te [interfejs API Partner uwierzytelniania.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1bc00-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="1bc00-114">Ten scenariusz obsługuje tylko uwierzytelnianie użytkowników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1bc00-114">This scenario only supports application user authentication.</span></span> <span data-ttu-id="1bc00-115">Tylko aplikacja nie jest jeszcze obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="1bc00-115">Application-only is not yet supported.</span></span> <span data-ttu-id="1bc00-116">Partnerzy, którzy **doświadczą błędu HTTP:400,** powinni zapoznać się [z dokumentacją interfejs API Partner uwierzytelniania.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1bc00-116">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="1bc00-117">Ten interfejs API obsługuje obecnie tylko dostęp użytkowników, w przypadku których partnerzy muszą pełnić jedną z następujących ról: Administrator globalny, Agent administracyjny lub Agent sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="1bc00-117">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="1bc00-118">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="1bc00-118">Details</span></span>

- <span data-ttu-id="1bc00-119">Funkcja Current zwraca tylko dane dotyczące zaktualizowanych nowych produktów opartych na licencjach handlowych.</span><span class="sxs-lookup"><span data-stu-id="1bc00-119">Current returns data only for updated new commerce license-based products.</span></span>
- <span data-ttu-id="1bc00-120">Bieżące ceny obejmują produkty dostępne w bieżącym miesiącu do daty wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1bc00-120">Current pricing includes products available during the current month to the date the API is called.</span></span> <span data-ttu-id="1bc00-121">Poprzednie miesiące zawierają datę ostatniego dnia wybranego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="1bc00-121">Previous months include date as of the last day of the selected month.</span></span>
- <span data-ttu-id="1bc00-122">Ta metoda zwraca dane jako strumień plików.</span><span class="sxs-lookup"><span data-stu-id="1bc00-122">This method returns data as a file stream.</span></span> <span data-ttu-id="1bc00-123">Strumień plików jest plikiem .csv lub skompresowaną wersją pliku zip .csv.</span><span class="sxs-lookup"><span data-stu-id="1bc00-123">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="1bc00-124">Poniżej znajdują się szczegółowe informacje na temat żądania skompresowanych plików.</span><span class="sxs-lookup"><span data-stu-id="1bc00-124">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="1bc00-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1bc00-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1bc00-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1bc00-126">Request syntax</span></span>

| <span data-ttu-id="1bc00-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="1bc00-127">Method</span></span>   | <span data-ttu-id="1bc00-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1bc00-128">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1bc00-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1bc00-129">**GET**</span></span> | <span data-ttu-id="1bc00-130"> https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value</span><span class="sxs-lookup"><span data-stu-id="1bc00-130">https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value</span></span> |

### <a name="uri-filter-parameters"></a><span data-ttu-id="1bc00-131">Parametry filtru URI</span><span class="sxs-lookup"><span data-stu-id="1bc00-131">URI filter parameters</span></span>

<span data-ttu-id="1bc00-132">Użyj następujących parametrów filtru.</span><span class="sxs-lookup"><span data-stu-id="1bc00-132">Use the following filter parameters.</span></span>

| <span data-ttu-id="1bc00-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1bc00-133">Name</span></span>                   | <span data-ttu-id="1bc00-134">Typ</span><span class="sxs-lookup"><span data-stu-id="1bc00-134">Type</span></span>     | <span data-ttu-id="1bc00-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1bc00-135">Required</span></span> | <span data-ttu-id="1bc00-136">Opis</span><span class="sxs-lookup"><span data-stu-id="1bc00-136">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="1bc00-137">Month (Miesiąc)</span><span class="sxs-lookup"><span data-stu-id="1bc00-137">Month</span></span>| <span data-ttu-id="1bc00-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="1bc00-138">string</span></span>   | <span data-ttu-id="1bc00-139">Nie</span><span class="sxs-lookup"><span data-stu-id="1bc00-139">No</span></span> | <span data-ttu-id="1bc00-140">Wymagany arkusz cen musi być zgodny z RRRRM.</span><span class="sxs-lookup"><span data-stu-id="1bc00-140">Must adhere to YYYYMM for the price sheet being requested.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1bc00-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1bc00-141">Request headers</span></span>

- <span data-ttu-id="1bc00-142">Aby uzyskać więcej informacji, zobacz [Nagłówki REST](headers.md) partnerów.</span><span class="sxs-lookup"><span data-stu-id="1bc00-142">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="1bc00-143">Oprócz powyższych nagłówków pliki cenowe mogą być pobierane jako skompresowane, co skraca czas pobierania i przepustowości.</span><span class="sxs-lookup"><span data-stu-id="1bc00-143">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="1bc00-144">Domyślnie pliki nie są kompresowane.</span><span class="sxs-lookup"><span data-stu-id="1bc00-144">By default the files are not compressed.</span></span> <span data-ttu-id="1bc00-145">Aby uzyskać skompresowane wersje plików, możesz dołączyć poniżej wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="1bc00-145">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="1bc00-146">Należy pamiętać, że skompresowane arkusze są dostępne tylko od kwietnia 2020 r., a wszystkie arkusze sprzed kwietnia 2020 r. są dostępne tylko jako nieskompresowane.</span><span class="sxs-lookup"><span data-stu-id="1bc00-146">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="1bc00-147">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="1bc00-147">Header</span></span>                   | <span data-ttu-id="1bc00-148">Typ wartości</span><span class="sxs-lookup"><span data-stu-id="1bc00-148">Value Type</span></span>     | <span data-ttu-id="1bc00-149">Wartość</span><span class="sxs-lookup"><span data-stu-id="1bc00-149">Value</span></span> | <span data-ttu-id="1bc00-150">Opis</span><span class="sxs-lookup"><span data-stu-id="1bc00-150">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="1bc00-151">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="1bc00-151">Accept-Encoding</span></span>| <span data-ttu-id="1bc00-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="1bc00-152">string</span></span>   | <span data-ttu-id="1bc00-153">Deflate</span><span class="sxs-lookup"><span data-stu-id="1bc00-153">deflate</span></span>| <span data-ttu-id="1bc00-154">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="1bc00-154">Optional.</span></span> <span data-ttu-id="1bc00-155">Jeśli pominięty strumień plików nie jest kompresowany.</span><span class="sxs-lookup"><span data-stu-id="1bc00-155">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="1bc00-156">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1bc00-156">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="1bc00-157">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1bc00-157">REST response</span></span>

<span data-ttu-id="1bc00-158">W przypadku powodzenia ta metoda zwraca macierz oferty jako strumień plików.</span><span class="sxs-lookup"><span data-stu-id="1bc00-158">If successful, this method returns an offer matrix as a file stream.</span></span> <span data-ttu-id="1bc00-159">Strumień plików jest plikiem .csv lub skompresowaną wersją pliku zip .csv.</span><span class="sxs-lookup"><span data-stu-id="1bc00-159">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1bc00-160">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1bc00-160">Response success and error codes</span></span>

<span data-ttu-id="1bc00-161">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1bc00-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1bc00-162">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1bc00-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1bc00-163">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1bc00-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1bc00-164">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1bc00-164">Response example</span></span>

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
