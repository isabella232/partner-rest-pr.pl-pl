---
title: Aktualizowanie potencjalnego klienta lub szansy sprzedaży (przestarzałe)
description: Umożliwia zaktualizowanie szczegółów potencjalnego klienta lub szansy sprzedaży. Ta metoda aktualizowania potencjalnego klienta lub szansy sprzedaży jest przestarzała i recommmend zamiast tego użycie wywołania PATCH.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770545"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a><span data-ttu-id="5c6a9-104">Aktualizowanie potencjalnego klienta lub szansy sprzedaży (przestarzałe)</span><span class="sxs-lookup"><span data-stu-id="5c6a9-104">Update a lead or opportunity (Obsolete)</span></span>

<span data-ttu-id="5c6a9-105">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="5c6a9-105">Applies to:</span></span>

- <span data-ttu-id="5c6a9-106">Interfejs API partnera</span><span class="sxs-lookup"><span data-stu-id="5c6a9-106">Partner API</span></span>

<span data-ttu-id="5c6a9-107">W tym temacie wyjaśniono, jak zaktualizować szczegóły potencjalnego klienta lub szansy sprzedaży, takie jak wartość transakcji, Szacowana data zamknięcia lub zarządzać etapami sprzedaży między innymi szczegółami.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-107">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span> 


> [!IMPORTANT]
<span data-ttu-id="5c6a9-108">Ta metoda aktualizowania potencjalnego klienta lub szansy sprzedaży jest przestarzała i recommmend zamiast tego użycie wywołania [patch](patch-a-referral.md) .</span><span class="sxs-lookup"><span data-stu-id="5c6a9-108">This method of updating a lead or opportunity is obsolete and we recommmend using the [PATCH](patch-a-referral.md) call instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c6a9-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5c6a9-109">Prerequisites</span></span>

- <span data-ttu-id="5c6a9-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5c6a9-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="5c6a9-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="5c6a9-112">Ten interfejs API obecnie obsługuje tylko dostęp użytkownika, w którym partnerzy muszą znajdować się w jednej z następujących ról: Administrator globalny, administrator odwołania lub użytkownik referencyjny.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5c6a9-113">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5c6a9-113">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5c6a9-114">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5c6a9-114">Request syntax</span></span>

| <span data-ttu-id="5c6a9-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="5c6a9-115">Method</span></span>  | <span data-ttu-id="5c6a9-116">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5c6a9-116">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="5c6a9-117">**PUT**</span><span class="sxs-lookup"><span data-stu-id="5c6a9-117">**PUT**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a><span data-ttu-id="5c6a9-118">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5c6a9-118">Request headers</span></span>

- <span data-ttu-id="5c6a9-119">Aby uzyskać więcej informacji, zobacz [nagłówki REST interfejsu API partnera](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5c6a9-119">For more information, see [Partner API REST headers](headers.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c6a9-120">Pamiętaj, aby ustawić nagłówek **if-Match** .</span><span class="sxs-lookup"><span data-stu-id="5c6a9-120">Be sure to set the **If-Match** header.</span></span>

### <a name="request-body"></a><span data-ttu-id="5c6a9-121">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5c6a9-121">Request body</span></span>

<span data-ttu-id="5c6a9-122">W tej tabeli opisano właściwości [odwołania](referral-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-122">This table describes the [Referral](referral-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="5c6a9-123">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5c6a9-123">Property</span></span>            | <span data-ttu-id="5c6a9-124">Typ</span><span class="sxs-lookup"><span data-stu-id="5c6a9-124">Type</span></span>                                                                 | <span data-ttu-id="5c6a9-125">Opis</span><span class="sxs-lookup"><span data-stu-id="5c6a9-125">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5c6a9-126">Id</span><span class="sxs-lookup"><span data-stu-id="5c6a9-126">Id</span></span>                  | <span data-ttu-id="5c6a9-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="5c6a9-127">string</span></span>                                                               | <span data-ttu-id="5c6a9-128">Identyfikator dla tego odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-128">The ID for this Referral.</span></span>                                                                                            |
| <span data-ttu-id="5c6a9-129">EngagementId</span><span class="sxs-lookup"><span data-stu-id="5c6a9-129">EngagementId</span></span>        | <span data-ttu-id="5c6a9-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="5c6a9-130">string</span></span>                                                               | <span data-ttu-id="5c6a9-131">EngagementID dla tego odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-131">The EngagementID for this Referral.</span></span> <span data-ttu-id="5c6a9-132">Wiele odwołań może być skojarzonych z pojedynczym EngagementID</span><span class="sxs-lookup"><span data-stu-id="5c6a9-132">Multiple referrals can be associated to a single EngagementID</span></span>                    |
| <span data-ttu-id="5c6a9-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5c6a9-133">Name</span></span>                | <span data-ttu-id="5c6a9-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="5c6a9-134">string</span></span>                                                               | <span data-ttu-id="5c6a9-135">Nazwa odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-135">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="5c6a9-136">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="5c6a9-136">ExternalReferenceId</span></span> | <span data-ttu-id="5c6a9-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="5c6a9-137">string</span></span>                                                               | <span data-ttu-id="5c6a9-138">Zewnętrzny identyfikator odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-138">An external identifier for the referral.</span></span> <span data-ttu-id="5c6a9-139">Przykład: Zachowaj własny identyfikator systemu Dynamics 365 potencjalnego klienta/szansy sprzedaży</span><span class="sxs-lookup"><span data-stu-id="5c6a9-139">Example: Store your own Dynamics 365 lead/opportunity ID</span></span>                    |
| <span data-ttu-id="5c6a9-140">CreatedDateTime</span><span class="sxs-lookup"><span data-stu-id="5c6a9-140">CreatedDateTime</span></span>     | <span data-ttu-id="5c6a9-141">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="5c6a9-141">string in UTC date time format</span></span>                                       | <span data-ttu-id="5c6a9-142">Data utworzenia odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-142">The date the referral was created.</span></span>                                                                                   |
| <span data-ttu-id="5c6a9-143">UpdatedDateTime</span><span class="sxs-lookup"><span data-stu-id="5c6a9-143">UpdatedDateTime</span></span>     | <span data-ttu-id="5c6a9-144">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="5c6a9-144">string in UTC date time format</span></span>                                       | <span data-ttu-id="5c6a9-145">Data ostatniej aktualizacji odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-145">The date the referral was last updated.</span></span>                                                                              |
| <span data-ttu-id="5c6a9-146">ExpirationDateTime</span><span class="sxs-lookup"><span data-stu-id="5c6a9-146">ExpirationDateTime</span></span>  | <span data-ttu-id="5c6a9-147">ciąg w formacie daty i godziny czasu UTC</span><span class="sxs-lookup"><span data-stu-id="5c6a9-147">string in UTC date time format</span></span>                                       | <span data-ttu-id="5c6a9-148">Data wygaśnięcia odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-148">The date the referral will expire.</span></span>                                                                                   |
| <span data-ttu-id="5c6a9-149">Stan</span><span class="sxs-lookup"><span data-stu-id="5c6a9-149">Status</span></span>              | [<span data-ttu-id="5c6a9-150">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="5c6a9-150">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="5c6a9-151">[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-151">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="5c6a9-152">Substatus</span><span class="sxs-lookup"><span data-stu-id="5c6a9-152">Substatus</span></span>           | [<span data-ttu-id="5c6a9-153">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="5c6a9-153">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="5c6a9-154">[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan podrzędny odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-154">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status.</span></span>      |
| <span data-ttu-id="5c6a9-155">StatusReason</span><span class="sxs-lookup"><span data-stu-id="5c6a9-155">StatusReason</span></span>        | <span data-ttu-id="5c6a9-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="5c6a9-156">string</span></span>                                                               | <span data-ttu-id="5c6a9-157">Opisowy komunikat o stanie.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-157">A descriptive message about the status.</span></span> <span data-ttu-id="5c6a9-158">Na przykład Wyjaśnij, dlaczego odwołanie zostało utracone.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-158">For example, explain why the referral was lost.</span></span>                              |
| <span data-ttu-id="5c6a9-159">— Odwołanie</span><span class="sxs-lookup"><span data-stu-id="5c6a9-159">ReferralType</span></span>        | [<span data-ttu-id="5c6a9-160">— Odwołanie</span><span class="sxs-lookup"><span data-stu-id="5c6a9-160">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="5c6a9-161">Reprezentuje typ odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-161">Represents the referral type.</span></span>                                                                                        |
| <span data-ttu-id="5c6a9-162">Kwalifikacja</span><span class="sxs-lookup"><span data-stu-id="5c6a9-162">Qualification</span></span>       | [<span data-ttu-id="5c6a9-163">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="5c6a9-163">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="5c6a9-164">Reprezentuje jakość odwołania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-164">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="5c6a9-165">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="5c6a9-165">CustomerProfile</span></span>     | [<span data-ttu-id="5c6a9-166">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="5c6a9-166">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="5c6a9-167">Informacje kontaktowe klienta.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-167">Customer contact information.</span></span>                                                                                        |
| <span data-ttu-id="5c6a9-168">Wyrażanie zgody</span><span class="sxs-lookup"><span data-stu-id="5c6a9-168">Consent</span></span>             | [<span data-ttu-id="5c6a9-169">Wyrażanie zgody</span><span class="sxs-lookup"><span data-stu-id="5c6a9-169">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="5c6a9-170">Flagi zgody na udostępnianie informacji innym organizacjom i Zezwalanie na kontakt z użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-170">Consent flags around sharing information with other organizations and allowing them to contact users.</span></span>                |
| <span data-ttu-id="5c6a9-171">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="5c6a9-171">Details</span></span>             | [<span data-ttu-id="5c6a9-172">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="5c6a9-172">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="5c6a9-173">Szczegóły klienta, notatki, wartość transakcji, Data zamknięcia waluty.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-173">Customer details, notes, deal value, currency closing date.</span></span>                                                          |
| <span data-ttu-id="5c6a9-174">Zespół</span><span class="sxs-lookup"><span data-stu-id="5c6a9-174">Team</span></span>                | [<span data-ttu-id="5c6a9-175">Członek</span><span class="sxs-lookup"><span data-stu-id="5c6a9-175">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="5c6a9-176">Reprezentuje użytkowników w organizacjach, które są zaangażowane w zaangażowanie partnerskie.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-176">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="5c6a9-177">InviteContext</span><span class="sxs-lookup"><span data-stu-id="5c6a9-177">InviteContext</span></span>       | [<span data-ttu-id="5c6a9-178">InviteContext</span><span class="sxs-lookup"><span data-stu-id="5c6a9-178">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="5c6a9-179">Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-179">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="5c6a9-180">Cel</span><span class="sxs-lookup"><span data-stu-id="5c6a9-180">Target</span></span>         | [<span data-ttu-id="5c6a9-181">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="5c6a9-181">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="5c6a9-182">Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-182">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

### <a name="status-and-substatus-transition-states"></a><span data-ttu-id="5c6a9-183">Stany przejścia stanu i podstanu</span><span class="sxs-lookup"><span data-stu-id="5c6a9-183">Status and substatus transition states</span></span>

| <span data-ttu-id="5c6a9-184">Stan</span><span class="sxs-lookup"><span data-stu-id="5c6a9-184">Status</span></span> | <span data-ttu-id="5c6a9-185">Dozwolone przejście stanu</span><span class="sxs-lookup"><span data-stu-id="5c6a9-185">Allowed Status Transition</span></span> | <span data-ttu-id="5c6a9-186">Dozwolony stan Substatus</span><span class="sxs-lookup"><span data-stu-id="5c6a9-186">Allowed Substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="5c6a9-187">Nowy</span><span class="sxs-lookup"><span data-stu-id="5c6a9-187">New</span></span>    | <span data-ttu-id="5c6a9-188">Nowy, aktywny, zamknięty</span><span class="sxs-lookup"><span data-stu-id="5c6a9-188">New, Active, Closed</span></span>       | <span data-ttu-id="5c6a9-189">Oczekiwanie, odebrano</span><span class="sxs-lookup"><span data-stu-id="5c6a9-189">Pending, Received</span></span>            |
| <span data-ttu-id="5c6a9-190">Aktywna</span><span class="sxs-lookup"><span data-stu-id="5c6a9-190">Active</span></span> | <span data-ttu-id="5c6a9-191">Aktywne, zamknięte</span><span class="sxs-lookup"><span data-stu-id="5c6a9-191">Active, Closed</span></span>            | <span data-ttu-id="5c6a9-192">Zaakceptowano</span><span class="sxs-lookup"><span data-stu-id="5c6a9-192">Accepted</span></span>                     |
| <span data-ttu-id="5c6a9-193">Zamknięty</span><span class="sxs-lookup"><span data-stu-id="5c6a9-193">Closed</span></span> | <span data-ttu-id="5c6a9-194">Zamknięty</span><span class="sxs-lookup"><span data-stu-id="5c6a9-194">Closed</span></span>                    | <span data-ttu-id="5c6a9-195">Wygrane, utracone, odrzucone, wygasłe</span><span class="sxs-lookup"><span data-stu-id="5c6a9-195">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="5c6a9-196">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5c6a9-196">Request example</span></span>

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> <span data-ttu-id="5c6a9-197">Usuń `"links": { }` obiekt z zasobu Put.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-197">Remove the `"links": { }` object from the PUT resource.</span></span>

## <a name="rest-response"></a><span data-ttu-id="5c6a9-198">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5c6a9-198">REST Response</span></span>

<span data-ttu-id="5c6a9-199">Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [odwołania](referral-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-199">If successful, this method returns the populated [referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5c6a9-200">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5c6a9-200">Response success and error codes</span></span>

<span data-ttu-id="5c6a9-201">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-201">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5c6a9-202">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5c6a9-202">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5c6a9-203">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5c6a9-203">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5c6a9-204">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5c6a9-204">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```