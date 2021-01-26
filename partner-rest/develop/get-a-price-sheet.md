---
title: Pobieranie arkusza cen
description: Uzyskaj arkusz cen dla danego rynku i widoku. Obsługuje filtry, aby uzyskać historię według miesiąca.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5195ebed6559bd71a7832a667e63ee801be1c82f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770516"
---
# <a name="get-a-price-sheet"></a><span data-ttu-id="fdecc-104">Pobieranie arkusza cen</span><span class="sxs-lookup"><span data-stu-id="fdecc-104">Get a price sheet</span></span>

<span data-ttu-id="fdecc-105">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="fdecc-105">Applies to:</span></span>

- <span data-ttu-id="fdecc-106">Interfejs API partnera</span><span class="sxs-lookup"><span data-stu-id="fdecc-106">Partner API</span></span>

<span data-ttu-id="fdecc-107">W tym temacie wyjaśniono, jak uzyskać arkusz cen dla danego rynku i widoku.</span><span class="sxs-lookup"><span data-stu-id="fdecc-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="fdecc-108">Ta metoda obsługuje filtry w celu uzyskania historii według miesiąca.</span><span class="sxs-lookup"><span data-stu-id="fdecc-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdecc-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fdecc-109">Prerequisites</span></span>

- <span data-ttu-id="fdecc-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fdecc-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="fdecc-111">Ten scenariusz obsługuje tylko uwierzytelnianie użytkownika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fdecc-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="fdecc-112">Aplikacja-tylko nie jest jeszcze obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="fdecc-112">Application-ony is not yet supported.</span></span>
- <span data-ttu-id="fdecc-113">Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą mieć jedną z następujących ról: Administrator globalny, Agent administracyjny lub agent sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="fdecc-113">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="fdecc-114">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="fdecc-114">Details</span></span>

- <span data-ttu-id="fdecc-115">Bieżąca zwraca dane tylko w przypadku użycia planu platformy Azure i produktów rezerwacji.</span><span class="sxs-lookup"><span data-stu-id="fdecc-115">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="fdecc-116">Bieżące [ceny](pricing.md) obejmują wszystkie liczniki i produkty dostępne w bieżącym miesiącu w dniu, w którym wywoływany jest interfejs API.</span><span class="sxs-lookup"><span data-stu-id="fdecc-116">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="fdecc-117">Poprzednie miesiące obejmują wszystkie liczniki i produkty dostępne w danym miesiącu.</span><span class="sxs-lookup"><span data-stu-id="fdecc-117">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="fdecc-118">Ceny licznika zużycia są dostępne tylko w USD, partnerzy korzystają z interfejsu API kursów wymiany walut w celu obliczenia kosztów lokalnych.</span><span class="sxs-lookup"><span data-stu-id="fdecc-118">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="fdecc-119">Ceny licznika zużycia to szacowane ceny detaliczne.</span><span class="sxs-lookup"><span data-stu-id="fdecc-119">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="fdecc-120">Rabaty partnerów są dostępne za pośrednictwem środków [partnerów](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span><span class="sxs-lookup"><span data-stu-id="fdecc-120">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="fdecc-121">Ceny licznika rezerwacji obejmują rabaty partnerów programu CSP.</span><span class="sxs-lookup"><span data-stu-id="fdecc-121">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="fdecc-122">Szacowane ceny detaliczne dla rezerwacji można znaleźć w temacie rezerwacja udostępnionych usług do pobrania z poziomu strony Cennik i oferty w centrum partnerskim.</span><span class="sxs-lookup"><span data-stu-id="fdecc-122">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="fdecc-123">Więcej informacji o cenach planu platformy Azure można znaleźć w [dokumentacji cennika planu platformy Azure](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="fdecc-123">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="fdecc-124">Cennik partnerski i interfejsy API wymiany walut obcych nie są częścią [zestawu SDK Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="fdecc-124">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="fdecc-125">Ta metoda zwraca listę cen jako strumień pliku.</span><span class="sxs-lookup"><span data-stu-id="fdecc-125">This method returns the price list as a file stream.</span></span> <span data-ttu-id="fdecc-126">Strumień plików to plik CSV lub skompresowana wersja pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="fdecc-126">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="fdecc-127">Poniżej znajdują się szczegółowe informacje dotyczące sposobu żądania skompresowanych plików.</span><span class="sxs-lookup"><span data-stu-id="fdecc-127">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="fdecc-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fdecc-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fdecc-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fdecc-129">Request syntax</span></span>

| <span data-ttu-id="fdecc-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="fdecc-130">Method</span></span>   | <span data-ttu-id="fdecc-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fdecc-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fdecc-132">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="fdecc-132">**GET**</span></span> | <span data-ttu-id="fdecc-133"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market="{Marketo}", PricesheetView = "{View}")/$value</span><span class="sxs-lookup"><span data-stu-id="fdecc-133">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="fdecc-134">Parametry wymagane przez identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="fdecc-134">URI required parameters</span></span>

<span data-ttu-id="fdecc-135">Użyj następujących parametrów ścieżki, aby zażądać danego rynku i typu arkusza cen.</span><span class="sxs-lookup"><span data-stu-id="fdecc-135">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="fdecc-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fdecc-136">Name</span></span>                   | <span data-ttu-id="fdecc-137">Typ</span><span class="sxs-lookup"><span data-stu-id="fdecc-137">Type</span></span>     | <span data-ttu-id="fdecc-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fdecc-138">Required</span></span> | <span data-ttu-id="fdecc-139">Opis</span><span class="sxs-lookup"><span data-stu-id="fdecc-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="fdecc-140">Do</span><span class="sxs-lookup"><span data-stu-id="fdecc-140">Market</span></span>                      | <span data-ttu-id="fdecc-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="fdecc-141">string</span></span>   | <span data-ttu-id="fdecc-142">Tak</span><span class="sxs-lookup"><span data-stu-id="fdecc-142">Yes</span></span>       | <span data-ttu-id="fdecc-143">Dwuliterowy kod kraju dla żądanego rynku</span><span class="sxs-lookup"><span data-stu-id="fdecc-143">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="fdecc-144">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="fdecc-144">PricesheetView</span></span> | <span data-ttu-id="fdecc-145">ciąg</span><span class="sxs-lookup"><span data-stu-id="fdecc-145">string</span></span>   | <span data-ttu-id="fdecc-146">Tak</span><span class="sxs-lookup"><span data-stu-id="fdecc-146">Yes</span></span>       | <span data-ttu-id="fdecc-147">Typ żądanego arkusza cen może być azure_consumption lub azure_reservations</span><span class="sxs-lookup"><span data-stu-id="fdecc-147">The type of price sheet being requested, this can be azure_consumption or azure_reservations</span></span>       |

### <a name="uri-filter-parameters"></a><span data-ttu-id="fdecc-148">Parametry filtru identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="fdecc-148">URI filter parameters</span></span>

<span data-ttu-id="fdecc-149">Użyj następujących parametrów filtru.</span><span class="sxs-lookup"><span data-stu-id="fdecc-149">Use the following filter parameters.</span></span>

| <span data-ttu-id="fdecc-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fdecc-150">Name</span></span>                   | <span data-ttu-id="fdecc-151">Typ</span><span class="sxs-lookup"><span data-stu-id="fdecc-151">Type</span></span>     | <span data-ttu-id="fdecc-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fdecc-152">Required</span></span> | <span data-ttu-id="fdecc-153">Opis</span><span class="sxs-lookup"><span data-stu-id="fdecc-153">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="fdecc-154">Oś czasu</span><span class="sxs-lookup"><span data-stu-id="fdecc-154">Timeline</span></span>| <span data-ttu-id="fdecc-155">ciąg</span><span class="sxs-lookup"><span data-stu-id="fdecc-155">string</span></span>   | <span data-ttu-id="fdecc-156">Nie</span><span class="sxs-lookup"><span data-stu-id="fdecc-156">No</span></span>| <span data-ttu-id="fdecc-157">Wartość domyślna to Current, jeśli nie została przeniesiona.</span><span class="sxs-lookup"><span data-stu-id="fdecc-157">Defaults to current if not passed.</span></span> <span data-ttu-id="fdecc-158">Możliwe wartości to History, Current i Future.</span><span class="sxs-lookup"><span data-stu-id="fdecc-158">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="fdecc-159">Month (Miesiąc)</span><span class="sxs-lookup"><span data-stu-id="fdecc-159">Month</span></span>| <span data-ttu-id="fdecc-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="fdecc-160">string</span></span>   | <span data-ttu-id="fdecc-161">Nie</span><span class="sxs-lookup"><span data-stu-id="fdecc-161">No</span></span>| <span data-ttu-id="fdecc-162">Wymagane tylko wtedy, gdy wymagana jest historia, musi być zgodna z YYYYMM dla żądanego arkusza cen.</span><span class="sxs-lookup"><span data-stu-id="fdecc-162">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="fdecc-163">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fdecc-163">Request headers</span></span>

- <span data-ttu-id="fdecc-164">Aby uzyskać więcej informacji, zobacz [nagłówki REST partnera](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="fdecc-164">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="fdecc-165">Oprócz powyższych nagłówków pliki cen można pobrać jako skompresowane zmniejszenie przepustowości i czas pobierania.</span><span class="sxs-lookup"><span data-stu-id="fdecc-165">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="fdecc-166">Domyślnie pliki nie są skompresowane.</span><span class="sxs-lookup"><span data-stu-id="fdecc-166">By default the files are not compressed.</span></span> <span data-ttu-id="fdecc-167">Aby uzyskać skompresowane wersje plików, można uwzględnić poniżej wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="fdecc-167">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="fdecc-168">Należy pamiętać, że skompresowane arkusze są dostępne tylko od 2020 kwietnia, a wszystkie arkusze przed 2020 kwietnia są dostępne tylko jako nieskompresowane.</span><span class="sxs-lookup"><span data-stu-id="fdecc-168">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="fdecc-169">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="fdecc-169">Header</span></span>                   | <span data-ttu-id="fdecc-170">Typ wartości</span><span class="sxs-lookup"><span data-stu-id="fdecc-170">Value Type</span></span>     | <span data-ttu-id="fdecc-171">Wartość</span><span class="sxs-lookup"><span data-stu-id="fdecc-171">Value</span></span> | <span data-ttu-id="fdecc-172">Opis</span><span class="sxs-lookup"><span data-stu-id="fdecc-172">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="fdecc-173">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="fdecc-173">Accept-Encoding</span></span>| <span data-ttu-id="fdecc-174">ciąg</span><span class="sxs-lookup"><span data-stu-id="fdecc-174">string</span></span>   | <span data-ttu-id="fdecc-175">Wklęśnięcie</span><span class="sxs-lookup"><span data-stu-id="fdecc-175">deflate</span></span>| <span data-ttu-id="fdecc-176">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="fdecc-176">Optional.</span></span> <span data-ttu-id="fdecc-177">Jeśli pominięty strumień plików nie jest skompresowany.</span><span class="sxs-lookup"><span data-stu-id="fdecc-177">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="fdecc-178">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fdecc-178">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="fdecc-179">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fdecc-179">REST response</span></span>

<span data-ttu-id="fdecc-180">Jeśli to się powiedzie, ta metoda zwraca listę cen jako strumień pliku.</span><span class="sxs-lookup"><span data-stu-id="fdecc-180">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="fdecc-181">Strumień plików to plik CSV lub skompresowana wersja pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="fdecc-181">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fdecc-182">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fdecc-182">Response success and error codes</span></span>

<span data-ttu-id="fdecc-183">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="fdecc-183">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fdecc-184">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fdecc-184">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fdecc-185">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fdecc-185">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fdecc-186">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fdecc-186">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```
