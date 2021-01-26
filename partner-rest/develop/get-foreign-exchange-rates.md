---
title: Pobieranie kursów wymiany walut
description: Uzyskaj kursy wymiany walut dla danego miesiąca.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770521"
---
# <a name="get-foreign-exchange-rates"></a><span data-ttu-id="dab0f-103">Pobieranie kursów wymiany walut</span><span class="sxs-lookup"><span data-stu-id="dab0f-103">Get foreign exchange rates</span></span>

<span data-ttu-id="dab0f-104">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="dab0f-104">Applies to:</span></span>

- <span data-ttu-id="dab0f-105">Interfejs API partnera</span><span class="sxs-lookup"><span data-stu-id="dab0f-105">Partner API</span></span>

<span data-ttu-id="dab0f-106">W tym temacie wyjaśniono, jak uzyskać kursy wymiany walut w danym miesiącu.</span><span class="sxs-lookup"><span data-stu-id="dab0f-106">This topic explains how to get foreign exchange rates for a given month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dab0f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dab0f-107">Prerequisites</span></span>

- <span data-ttu-id="dab0f-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dab0f-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="dab0f-109">Ten scenariusz obsługuje tylko uwierzytelnianie użytkownika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dab0f-109">This scenario only supports application user authentication.</span></span> <span data-ttu-id="dab0f-110">Tylko aplikacja nie jest jeszcze obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="dab0f-110">Application-only is not yet supported.</span></span>
- <span data-ttu-id="dab0f-111">Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą mieć jedną z następujących ról: Administrator globalny, Agent administracyjny lub agent sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="dab0f-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>


## <a name="details"></a><span data-ttu-id="dab0f-112">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="dab0f-112">Details</span></span>

- <span data-ttu-id="dab0f-113">Obecnie używany z [interfejsem API uzyskiwania arkusza cen](get-a-price-sheet.md) do obliczania oczekiwanych opłat za walutę lokalną dostawcy CSP planu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dab0f-113">Currently used with [get price sheet API](get-a-price-sheet.md) to calculate expected charges for Azure plan CSP local currencies.</span></span>
- <span data-ttu-id="dab0f-114">Stawki za wymianę walut obcych są spełnione przez cały miesiąc, w którym są one wysyłane.</span><span class="sxs-lookup"><span data-stu-id="dab0f-114">Foreign exchange rates hold true for the entire month they are posted.</span></span>
- <span data-ttu-id="dab0f-115">Więcej informacji o [cenach](pricing.md) planu platformy Azure można znaleźć w [dokumentacji cennika planu platformy Azure](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="dab0f-115">More information about Azure plan [pricing](pricing.md) can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="dab0f-116">Cennik partnerski i interfejsy API wymiany walut obcych nie są częścią [zestawu SDK Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="dab0f-116">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="dab0f-117">Ta metoda zwraca wyniki jako strumień pliku.</span><span class="sxs-lookup"><span data-stu-id="dab0f-117">This method returns results as a file stream.</span></span> <span data-ttu-id="dab0f-118">Strumień plików to plik CSV lub skompresowana wersja pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="dab0f-118">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="dab0f-119">Poniżej znajdują się szczegółowe informacje dotyczące sposobu żądania skompresowanych plików.</span><span class="sxs-lookup"><span data-stu-id="dab0f-119">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="dab0f-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="dab0f-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dab0f-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="dab0f-121">Request syntax</span></span>

| <span data-ttu-id="dab0f-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="dab0f-122">Method</span></span>   | <span data-ttu-id="dab0f-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="dab0f-123">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dab0f-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="dab0f-124">**GET**</span></span> | <span data-ttu-id="dab0f-125"> https://api.partner.microsoft.com/v1.0/sales/fxrates(Month="{Month}")/$value</span><span class="sxs-lookup"><span data-stu-id="dab0f-125">https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='{month}')/$value</span></span>                                  |

### <a name="uri-required-parameters"></a><span data-ttu-id="dab0f-126">Parametry wymagane przez identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="dab0f-126">URI required parameters</span></span>

<span data-ttu-id="dab0f-127">Użyj następujących parametrów ścieżki, aby zażądać pożądanego miesiąca kursów wymiany walut.</span><span class="sxs-lookup"><span data-stu-id="dab0f-127">Use the following path parameters to request the month of foreign exchange rates you want.</span></span>

| <span data-ttu-id="dab0f-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dab0f-128">Name</span></span>                   | <span data-ttu-id="dab0f-129">Typ</span><span class="sxs-lookup"><span data-stu-id="dab0f-129">Type</span></span>     | <span data-ttu-id="dab0f-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dab0f-130">Required</span></span> | <span data-ttu-id="dab0f-131">Opis</span><span class="sxs-lookup"><span data-stu-id="dab0f-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="dab0f-132">Month (Miesiąc)</span><span class="sxs-lookup"><span data-stu-id="dab0f-132">Month</span></span>                      | <span data-ttu-id="dab0f-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="dab0f-133">string</span></span>   | <span data-ttu-id="dab0f-134">Tak</span><span class="sxs-lookup"><span data-stu-id="dab0f-134">Yes</span></span>       | <span data-ttu-id="dab0f-135">Musi być w formacie YYYMM.</span><span class="sxs-lookup"><span data-stu-id="dab0f-135">Must be in YYYMM format.</span></span> <span data-ttu-id="dab0f-136">W przypadku pominięcia wartości domyślnych w bieżącym miesiącu.</span><span class="sxs-lookup"><span data-stu-id="dab0f-136">If omitted defaults to current month.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="dab0f-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="dab0f-137">Request headers</span></span>

- <span data-ttu-id="dab0f-138">Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="dab0f-138">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="dab0f-139">Oprócz powyższych nagłówków pliki można pobrać jako skompresowane zmniejszenie przepustowości i czas pobierania.</span><span class="sxs-lookup"><span data-stu-id="dab0f-139">In addition to the above headers, files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="dab0f-140">Domyślnie pliki nie są skompresowane.</span><span class="sxs-lookup"><span data-stu-id="dab0f-140">By default the files are not compressed.</span></span> <span data-ttu-id="dab0f-141">Aby uzyskać skompresowane wersje plików, można uwzględnić poniżej wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="dab0f-141">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="dab0f-142">Należy pamiętać, że skompresowane arkusze są dostępne tylko od 2020 kwietnia, a wszystkie żądania przed 2020 kwietnia są dostępne tylko jako nieskompresowane.</span><span class="sxs-lookup"><span data-stu-id="dab0f-142">Realize that compressed sheets are only available from April 2020 onward, all requests prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="dab0f-143">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="dab0f-143">Header</span></span>                   | <span data-ttu-id="dab0f-144">Typ wartości</span><span class="sxs-lookup"><span data-stu-id="dab0f-144">Value Type</span></span>     | <span data-ttu-id="dab0f-145">Wartość</span><span class="sxs-lookup"><span data-stu-id="dab0f-145">Value</span></span> | <span data-ttu-id="dab0f-146">Opis</span><span class="sxs-lookup"><span data-stu-id="dab0f-146">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="dab0f-147">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="dab0f-147">Accept-Encoding</span></span>| <span data-ttu-id="dab0f-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="dab0f-148">string</span></span>   | <span data-ttu-id="dab0f-149">Wklęśnięcie</span><span class="sxs-lookup"><span data-stu-id="dab0f-149">deflate</span></span>| <span data-ttu-id="dab0f-150">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="dab0f-150">Optional.</span></span> <span data-ttu-id="dab0f-151">Jeśli pominięty strumień plików nie jest skompresowany.</span><span class="sxs-lookup"><span data-stu-id="dab0f-151">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="dab0f-152">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="dab0f-152">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="dab0f-153">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="dab0f-153">REST response</span></span>

<span data-ttu-id="dab0f-154">Jeśli to się powiedzie, ta metoda zwraca obce kursy wymiany jako strumień pliku.</span><span class="sxs-lookup"><span data-stu-id="dab0f-154">If successful, this method returns foreign exchange rates as a file stream.</span></span> <span data-ttu-id="dab0f-155">Strumień plików to plik CSV lub skompresowana wersja pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="dab0f-155">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dab0f-156">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dab0f-156">Response success and error codes</span></span>

<span data-ttu-id="dab0f-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="dab0f-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dab0f-158">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="dab0f-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dab0f-159">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dab0f-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dab0f-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="dab0f-160">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
