---
title: Nagłówki REST interfejsu API partnera
description: Następujące nagłówki żądania HTTP i odpowiedzi są obsługiwane przez interfejs API REST partnera.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 955cab07da7f3a386690e18042165015906d864a
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770481"
---
# <a name="partner-rest-api-headers"></a>Nagłówki interfejsu API REST partnera

Interfejs API REST partnera obsługuje następujące nagłówki żądań i odpowiedzi HTTP.

> [!NOTE]
> Nie wszystkie wywołania interfejsu API akceptują wszystkie nagłówki.

## <a name="request-headers"></a>Nagłówki żądań

Następujące nagłówki żądania HTTP są obsługiwane przez interfejs API REST partnera.

| Nagłówek                       | Typ wartości | Opis                                                                            |
|------------------------------|------------|----------------------------------------------------------------------------------------|
| Autoryzacja           | ciąg     | Wymagane. Token autoryzacji w postaci &lt; tokenu okaziciela &gt; .                    |
| Zaakceptuj                  | ciąg     | Określa typ żądania i odpowiedzi "Application/JSON".                           |
| Identyfikator żądania klienta         | GUID       | Wymagane. Unikatowy identyfikator wywołania, przydatny w dziennikach i śladach sieci do rozwiązywania problemów z błędami. Wartość powinna być resetowana dla każdego wywołania. Wszystkie operacje powinny zawierać ten nagłówek. |
| If-Match:                    | ciąg     | Używany na potrzeby kontroli współbieżności. Niektóre wywołania interfejsu API wymagają przekazania elementu ETag za pośrednictwem nagłówka If-Match. Element ETag zazwyczaj znajduje się na tym samym zasobie i w związku z tym wymaga uzyskania najnowszej wersji. |

## <a name="response-headers"></a>Nagłówki odpowiedzi

Interfejs API REST partnera może zwrócić następujące nagłówki odpowiedzi HTTP.

| Nagłówek                    | Typ wartości | Opis                                                                                                               |
|-------------------|------------|--------------------------------------------------------------------------------------------------|
| Zaakceptuj                | ciąg     | Określa typ żądania i odpowiedzi "Application/JSON".                                     |
| Identyfikator żądania        | GUID       | Unikatowy identyfikator wywołania, używany do zapewnienia działania dotyczącego identyfikatora. W przypadku przekroczenia limitu czasu połączenie ponawiania powinno zawierać tę samą wartość. Po odebraniu odpowiedzi (sukces lub błąd biznesowy) należy zresetować wartość dla następnego wywołania. |
| Identyfikator żądania klienta| GUID| Unikatowy identyfikator wywołania, przydatne dzienniki i ślady sieci do rozwiązywania problemów. Wartość powinna być resetowana dla każdego wywołania. Wszystkie operacje powinny zawierać ten nagłówek.                                                |
| x-MS-AGS-Diagnostic   | ciąg | Ciąg, który zawiera informacje diagnostyczne z usługi.
| sygnatura czasowa|ciąg | Sygnatura czasowa żądania po osiągnięciu interfejsu API.
|Element ETag |ciąg | Element ETag zasobu.
