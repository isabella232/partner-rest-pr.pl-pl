---
title: Pobieranie arkusza cen
description: Uzyskaj arkusz cen dla danego rynku i widoku. Obsługuje filtry w celu uzyskania historii według miesięcy.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7571e8fce861dbfe463000a1ac4094115af08ffa
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/01/2021
ms.locfileid: "113125520"
---
# <a name="get-a-price-sheet"></a><span data-ttu-id="8f72f-104">Pobieranie arkusza cen</span><span class="sxs-lookup"><span data-stu-id="8f72f-104">Get a price sheet</span></span>

<span data-ttu-id="8f72f-105">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="8f72f-105">Applies to:</span></span>

- <span data-ttu-id="8f72f-106">interfejs API Partner</span><span class="sxs-lookup"><span data-stu-id="8f72f-106">Partner API</span></span>

<span data-ttu-id="8f72f-107">W tym temacie wyjaśniono, jak uzyskać arkusz cen dla danego rynku i widoku.</span><span class="sxs-lookup"><span data-stu-id="8f72f-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="8f72f-108">Ta metoda obsługuje filtry w celu uzyskania historii według miesięcy.</span><span class="sxs-lookup"><span data-stu-id="8f72f-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f72f-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8f72f-109">Prerequisites</span></span>

- <span data-ttu-id="8f72f-110">Poświadczenia zgodnie z opisem w te [interfejs API Partner uwierzytelniania.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8f72f-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="8f72f-111">Ten scenariusz obsługuje tylko uwierzytelnianie użytkowników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8f72f-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="8f72f-112">Tylko aplikacja nie jest jeszcze obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="8f72f-112">Application-only is not yet supported.</span></span> <span data-ttu-id="8f72f-113">Partnerzy, którzy **doświadczą błędu HTTP:400,** powinni zapoznać się z [dokumentacją interfejs API Partner uwierzytelniania.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8f72f-113">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="8f72f-114">Ten interfejs API obsługuje obecnie tylko dostęp użytkowników, w przypadku którego partnerzy muszą pełnić jedną z następujących ról: administrator globalny, agent administracyjny lub agent sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="8f72f-114">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="8f72f-115">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="8f72f-115">Details</span></span>

- <span data-ttu-id="8f72f-116">Funkcja Current zwraca tylko dane dotyczące użycia planu platformy Azure i produktów rezerwacji.</span><span class="sxs-lookup"><span data-stu-id="8f72f-116">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="8f72f-117">Bieżący [cennik](pricing.md) obejmuje wszystkie mierniki i produkty dostępne w bieżącym miesiącu do daty wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8f72f-117">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="8f72f-118">Poprzednie miesiące obejmują wszystkie mierniki i produkty dostępne dla danego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="8f72f-118">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="8f72f-119">Ceny miernika zużycia są tylko w USD, a partnerzy mają używać interfejsu API kursów wymiany obcej do obliczania kosztów w lokalnej walucie.</span><span class="sxs-lookup"><span data-stu-id="8f72f-119">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="8f72f-120">Ceny miernika zużycia to szacowane ceny detaliczne.</span><span class="sxs-lookup"><span data-stu-id="8f72f-120">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="8f72f-121">Rabaty dla partnerów są dostępne za [pośrednictwem środków uzyskane przez partnera.](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation)</span><span class="sxs-lookup"><span data-stu-id="8f72f-121">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="8f72f-122">Ceny mierników rezerwacji obejmują rabaty dla partnerów programu CSP.</span><span class="sxs-lookup"><span data-stu-id="8f72f-122">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="8f72f-123">Szacowane ceny detaliczne rezerwacji można znaleźć w udostępnionych usługach rezerwacji do pobrania na stronie Partner Center "Ceny i oferty".</span><span class="sxs-lookup"><span data-stu-id="8f72f-123">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="8f72f-124">Więcej informacji na temat cen planu platformy Azure można znaleźć w [dokumentacji cennika planu platformy Azure.](https://docs.microsoft.com/partner-center/azure-plan-price-list)</span><span class="sxs-lookup"><span data-stu-id="8f72f-124">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="8f72f-125">Interfejsy API cen partnerów i kursów wymiany walut nie są częścią [zestaw SDK Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="8f72f-125">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="8f72f-126">Ta metoda zwraca cennik jako strumień plików.</span><span class="sxs-lookup"><span data-stu-id="8f72f-126">This method returns the price list as a file stream.</span></span> <span data-ttu-id="8f72f-127">Strumień plików jest plikiem .csv lub skompresowaną wersją pliku zip .csv.</span><span class="sxs-lookup"><span data-stu-id="8f72f-127">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="8f72f-128">Poniżej znajdują się szczegółowe informacje na temat żądania skompresowanych plików.</span><span class="sxs-lookup"><span data-stu-id="8f72f-128">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="8f72f-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8f72f-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8f72f-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8f72f-130">Request syntax</span></span>

| <span data-ttu-id="8f72f-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="8f72f-131">Method</span></span>   | <span data-ttu-id="8f72f-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8f72f-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f72f-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="8f72f-133">**GET**</span></span> | <span data-ttu-id="8f72f-134"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span><span class="sxs-lookup"><span data-stu-id="8f72f-134">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="8f72f-135">Wymagane parametry URI</span><span class="sxs-lookup"><span data-stu-id="8f72f-135">URI required parameters</span></span>

<span data-ttu-id="8f72f-136">Użyj następujących parametrów ścieżki, aby zażądać rynku i typu arkusza cen.</span><span class="sxs-lookup"><span data-stu-id="8f72f-136">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="8f72f-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8f72f-137">Name</span></span>                   | <span data-ttu-id="8f72f-138">Typ</span><span class="sxs-lookup"><span data-stu-id="8f72f-138">Type</span></span>     | <span data-ttu-id="8f72f-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8f72f-139">Required</span></span> | <span data-ttu-id="8f72f-140">Opis</span><span class="sxs-lookup"><span data-stu-id="8f72f-140">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="8f72f-141">Rynku</span><span class="sxs-lookup"><span data-stu-id="8f72f-141">Market</span></span>                      | <span data-ttu-id="8f72f-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="8f72f-142">string</span></span>   | <span data-ttu-id="8f72f-143">Tak</span><span class="sxs-lookup"><span data-stu-id="8f72f-143">Yes</span></span>       | <span data-ttu-id="8f72f-144">Dwulicieowy kod kraju dla żądanego rynku</span><span class="sxs-lookup"><span data-stu-id="8f72f-144">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="8f72f-145">Widok arkusza cen</span><span class="sxs-lookup"><span data-stu-id="8f72f-145">PricesheetView</span></span> | <span data-ttu-id="8f72f-146">ciąg</span><span class="sxs-lookup"><span data-stu-id="8f72f-146">string</span></span>   | <span data-ttu-id="8f72f-147">Tak</span><span class="sxs-lookup"><span data-stu-id="8f72f-147">Yes</span></span>       | <span data-ttu-id="8f72f-148">Żądany typ arkusza cen może być azure_consumption, azure_reservations lub zaktualizowanylicensena podstawie.</span><span class="sxs-lookup"><span data-stu-id="8f72f-148">The type of price sheet being requested, this can be azure_consumption, azure_reservations or updatedlicensebased.</span></span>  |

> [!Note]
> <span data-ttu-id="8f72f-149">Widok PriceSheetView zaktualizowany na podstawie licencji jest obecnie dostępny tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="8f72f-149">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

### <a name="uri-filter-parameters"></a><span data-ttu-id="8f72f-150">Parametry filtru URI</span><span class="sxs-lookup"><span data-stu-id="8f72f-150">URI filter parameters</span></span>

<span data-ttu-id="8f72f-151">Użyj następujących parametrów filtru.</span><span class="sxs-lookup"><span data-stu-id="8f72f-151">Use the following filter parameters.</span></span>

| <span data-ttu-id="8f72f-152">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8f72f-152">Name</span></span>                   | <span data-ttu-id="8f72f-153">Typ</span><span class="sxs-lookup"><span data-stu-id="8f72f-153">Type</span></span>     | <span data-ttu-id="8f72f-154">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8f72f-154">Required</span></span> | <span data-ttu-id="8f72f-155">Opis</span><span class="sxs-lookup"><span data-stu-id="8f72f-155">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="8f72f-156">Oś czasu</span><span class="sxs-lookup"><span data-stu-id="8f72f-156">Timeline</span></span>| <span data-ttu-id="8f72f-157">ciąg</span><span class="sxs-lookup"><span data-stu-id="8f72f-157">string</span></span>   | <span data-ttu-id="8f72f-158">Nie</span><span class="sxs-lookup"><span data-stu-id="8f72f-158">No</span></span>| <span data-ttu-id="8f72f-159">Wartość domyślna to current, jeśli nie zostanie przekazana.</span><span class="sxs-lookup"><span data-stu-id="8f72f-159">Defaults to current if not passed.</span></span> <span data-ttu-id="8f72f-160">Możliwe wartości to historia, bieżąca i przyszła.</span><span class="sxs-lookup"><span data-stu-id="8f72f-160">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="8f72f-161">Month (Miesiąc)</span><span class="sxs-lookup"><span data-stu-id="8f72f-161">Month</span></span>| <span data-ttu-id="8f72f-162">ciąg</span><span class="sxs-lookup"><span data-stu-id="8f72f-162">string</span></span>   | <span data-ttu-id="8f72f-163">Nie</span><span class="sxs-lookup"><span data-stu-id="8f72f-163">No</span></span>| <span data-ttu-id="8f72f-164">Wymagane tylko w przypadku zażądania historii, muszą być zgodne z RRRR dla żądanego arkusza cen.</span><span class="sxs-lookup"><span data-stu-id="8f72f-164">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="8f72f-165">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8f72f-165">Request headers</span></span>

- <span data-ttu-id="8f72f-166">Aby uzyskać więcej informacji, zobacz [Nagłówki REST](headers.md) partnerów.</span><span class="sxs-lookup"><span data-stu-id="8f72f-166">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="8f72f-167">Oprócz powyższych nagłówków pliki cenowe mogą być pobierane jako skompresowane, co skraca czas pobierania i przepustowości.</span><span class="sxs-lookup"><span data-stu-id="8f72f-167">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="8f72f-168">Domyślnie pliki nie są kompresowane.</span><span class="sxs-lookup"><span data-stu-id="8f72f-168">By default the files are not compressed.</span></span> <span data-ttu-id="8f72f-169">Aby uzyskać skompresowane wersje plików, możesz dołączyć poniżej wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="8f72f-169">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="8f72f-170">Należy pamiętać, że skompresowane arkusze są dostępne tylko od kwietnia 2020 r., a wszystkie arkusze sprzed kwietnia 2020 r. są dostępne tylko jako nieskompresowane.</span><span class="sxs-lookup"><span data-stu-id="8f72f-170">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="8f72f-171">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="8f72f-171">Header</span></span>                   | <span data-ttu-id="8f72f-172">Typ wartości</span><span class="sxs-lookup"><span data-stu-id="8f72f-172">Value Type</span></span>     | <span data-ttu-id="8f72f-173">Wartość</span><span class="sxs-lookup"><span data-stu-id="8f72f-173">Value</span></span> | <span data-ttu-id="8f72f-174">Opis</span><span class="sxs-lookup"><span data-stu-id="8f72f-174">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="8f72f-175">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="8f72f-175">Accept-Encoding</span></span>| <span data-ttu-id="8f72f-176">ciąg</span><span class="sxs-lookup"><span data-stu-id="8f72f-176">string</span></span>   | <span data-ttu-id="8f72f-177">Deflate</span><span class="sxs-lookup"><span data-stu-id="8f72f-177">deflate</span></span>| <span data-ttu-id="8f72f-178">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="8f72f-178">Optional.</span></span> <span data-ttu-id="8f72f-179">Jeśli pominięty strumień plików nie jest kompresowany.</span><span class="sxs-lookup"><span data-stu-id="8f72f-179">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="8f72f-180">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8f72f-180">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a><span data-ttu-id="8f72f-181">Przykład żądania dla nowego handlu</span><span class="sxs-lookup"><span data-stu-id="8f72f-181">Request example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="8f72f-182">Widok PriceSheetView zaktualizowany na podstawie licencji jest obecnie dostępny tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="8f72f-182">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="8f72f-183">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8f72f-183">REST response</span></span>

<span data-ttu-id="8f72f-184">W przypadku powodzenia ta metoda zwraca cennik jako strumień plików.</span><span class="sxs-lookup"><span data-stu-id="8f72f-184">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="8f72f-185">Strumień plików jest plikiem .csv lub skompresowaną wersją pliku zip .csv.</span><span class="sxs-lookup"><span data-stu-id="8f72f-185">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8f72f-186">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8f72f-186">Response success and error codes</span></span>

<span data-ttu-id="8f72f-187">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="8f72f-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8f72f-188">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8f72f-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8f72f-189">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8f72f-189">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8f72f-190">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8f72f-190">Response example</span></span>

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

### <a name="response-example-for-new-commerce"></a><span data-ttu-id="8f72f-191">Przykład odpowiedzi dla nowego handlu</span><span class="sxs-lookup"><span data-stu-id="8f72f-191">Response example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="8f72f-192">Widok PriceSheetView zaktualizowany na podstawie licencji jest obecnie dostępny tylko dla partnerów, którzy są częścią nowego doświadczenia handlowego M365/D365 w wersji Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="8f72f-192">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=sheets.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","BillingPlan","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","Tags","ERP Price“
"Advanced Communications","CFQ7TTC0HDK0","0001","Advanced Communications","Microsoft Corporation","Advanced meetings, calling, workflow integration, and management tools for IT.","","P1Y","Annual","US","USD","115.2","","","2/1/2019 12:00:00 AM","2/4/2021 8:35:31 PM","License","144"
======= Truncated ==============

```
