---
title: Programowe zarządzanie potencjalnymi klientami i szansami sprzedaży w centrum partnerskim
description: W tej sekcji opisano, w jaki sposób partnerzy mogą używać interfejsów API partnera do programistycznego zarządzania potencjalnymi klientami i możliwościami wspólnej sprzedaży.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0da725c9b2459a6c5631b7cc7e21b46e9a7191b8
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770534"
---
# <a name="programmatically-manage-leads-and-co-sell-opportunities-in-partner-center"></a><span data-ttu-id="5776d-103">Programowe zarządzanie potencjalnymi klientami i szansami sprzedaży w centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="5776d-103">Programmatically manage leads and co-sell opportunities in Partner Center</span></span>

<span data-ttu-id="5776d-104">Ten artykuł pomoże Ci zrozumieć, jak można programowo zarządzać potencjalnymi klientami otrzymanymi ze strony dostawca rozwiązań firmy Microsoft oraz możliwościami współsprzedaży uzyskanymi od przedstawiciela Microsoft Sales lub innych partnerów.</span><span class="sxs-lookup"><span data-stu-id="5776d-104">This article will help you understand how you can programmatically manage the leads that you receive from Microsoft solution provider page and the co-sell opportunities that you receive from Microsoft sales representative or other partners.</span></span> <span data-ttu-id="5776d-105">Możesz również użyć tych interfejsów API do programistycznego udostępniania potoku sprzedaży firmy lub zapraszać przedstawicieli handlowych firmy Microsoft do współpracy nad potencjalnymi możliwościami.</span><span class="sxs-lookup"><span data-stu-id="5776d-105">You can also use these api's to programmatically share your company's sales pipeline or invite Microsoft sales representatives to collaborate on potential opportunities.</span></span> 

## <a name="manage-leads-and-opportunities"></a><span data-ttu-id="5776d-106">Zarządzanie potencjalnymi klientami i szansami sprzedaży</span><span class="sxs-lookup"><span data-stu-id="5776d-106">Manage leads and opportunities</span></span>

- <span data-ttu-id="5776d-107">[Pobierz listę potencjalnych klientów i szans sprzedaży](get-a-list-of-referrals.md) — pobiera listę potencjalnych klientów ze strony dostawcy rozwiązań firmy Microsoft oraz możliwości wspólnej sprzedaży od sprzedawcy firmy Microsoft lub innych partnerów.</span><span class="sxs-lookup"><span data-stu-id="5776d-107">[Get the list of leads and opportunities](get-a-list-of-referrals.md) - Gets the list of leads from Microsoft solution provider page and co-sell opportunities from Microsoft sellers or other partners.</span></span> <span data-ttu-id="5776d-108">Będzie to również zawierać listę szans sprzedaży utworzonych przez organizację.</span><span class="sxs-lookup"><span data-stu-id="5776d-108">This will also contain the list of opportunities created by your organization.</span></span>
- <span data-ttu-id="5776d-109">[Uzyskaj potencjalny klient lub szansę sprzedaży według identyfikatora](get-a-referral-by-Id.md) — pobiera potencjalnego klienta lub szansę sprzedaży według identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="5776d-109">[Get a lead or opportunity by Id](get-a-referral-by-Id.md) - Gets a lead or opportunity by Id.</span></span>
- <span data-ttu-id="5776d-110">[Aktualizacja potencjalnego klienta lub szansy sprzedaży](patch-a-referral.md) — umożliwia zaktualizowanie szczegółów potencjalnego klienta lub szansy sprzedaży, na przykład wartości transakcji, szacowanej daty zamknięcia lub zarządzania etapami sprzedaży między innymi szczegółami.</span><span class="sxs-lookup"><span data-stu-id="5776d-110">[Update a lead or opportunity](patch-a-referral.md) - Allows you to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>
- <span data-ttu-id="5776d-111">[Tworzenie nowej szansy sprzedaży](create-a-referral.md) — umożliwia utworzenie nowej możliwości współsprzedaży lub prywatnej transakcji.</span><span class="sxs-lookup"><span data-stu-id="5776d-111">[Create a new opportunity](create-a-referral.md) - Enables you to create a new co-sell opportunity or private deal.</span></span>
- [<span data-ttu-id="5776d-112">Zasoby dotyczące poleceń</span><span class="sxs-lookup"><span data-stu-id="5776d-112">Referral resources</span></span>](referral-resources.md)

> [!Note]
> <span data-ttu-id="5776d-113">Potencjalni klienci z komercyjnego rynku firmy Microsoft (Azure Marketplace i AppSource) nie mogą być zarządzani za pomocą interfejsu API Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="5776d-113">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) cannot be managed using Partner Center api's.</span></span>