---
title: Utworzenie polecenia
description: Utwórz niezależne lub udostępnione odwołania w interfejsie API partnera.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770492"
---
# <a name="create-a-referral"></a><span data-ttu-id="666b0-103">Utworzenie polecenia</span><span class="sxs-lookup"><span data-stu-id="666b0-103">Create a referral</span></span>

<span data-ttu-id="666b0-104">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="666b0-104">Applies to:</span></span>

- <span data-ttu-id="666b0-105">Interfejs API partnera</span><span class="sxs-lookup"><span data-stu-id="666b0-105">Partner API</span></span>

<span data-ttu-id="666b0-106">W tym temacie wyjaśniono, jak utworzyć odwołanie.</span><span class="sxs-lookup"><span data-stu-id="666b0-106">This topic explains how to create a referral.</span></span> <span data-ttu-id="666b0-107">Istnieją dwa typy [odwołań](referral-resources.md#referraltype):</span><span class="sxs-lookup"><span data-stu-id="666b0-107">There are two types of [ReferralType](referral-resources.md#referraltype):</span></span>

1. <span data-ttu-id="666b0-108">Niezależne: gdzie odwołanie jest widoczne dla jednego partnera.</span><span class="sxs-lookup"><span data-stu-id="666b0-108">Independent: Where a referral is visible to one partner.</span></span>
2. <span data-ttu-id="666b0-109">Udostępnione: gdzie odwołanie jest widoczne dla dwóch stron, które współpracują ze sobą.</span><span class="sxs-lookup"><span data-stu-id="666b0-109">Shared: Where a referral is visible to two parties that are working together.</span></span> <span data-ttu-id="666b0-110">Na przykład jeśli firma Microsoft i partner współpracują ze sobą w ramach transakcji współsprzedaży, odwołanie może być współużytkowane przez obie strony.</span><span class="sxs-lookup"><span data-stu-id="666b0-110">For example, if Microsoft and a partner are working together in a co-selling deal, a referral can be shared between both parties.</span></span> <span data-ttu-id="666b0-111">Aby uzyskać więcej informacji, zobacz sekcję [Tworzenie udostępnionej referencji](#create-a-shared-referral).</span><span class="sxs-lookup"><span data-stu-id="666b0-111">For more information, see the section [Creating a shared referral](#create-a-shared-referral).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="666b0-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="666b0-112">Prerequisites</span></span>

- <span data-ttu-id="666b0-113">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie interfejsu API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="666b0-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="666b0-114">Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="666b0-114">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="666b0-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="666b0-115">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="666b0-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="666b0-116">Request syntax</span></span>

| <span data-ttu-id="666b0-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="666b0-117">Method</span></span>  | <span data-ttu-id="666b0-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="666b0-118">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="666b0-119">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="666b0-119">**POST**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a><span data-ttu-id="666b0-120">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="666b0-120">Request headers</span></span>

- <span data-ttu-id="666b0-121">Aby uzyskać więcej informacji, zobacz [nagłówki REST interfejsu API partnera](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="666b0-121">See [Partner API REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="666b0-122">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="666b0-122">Request body</span></span>

<span data-ttu-id="666b0-123">W tej tabeli opisano właściwości [odwołania](referral-resources.md) w treści żądania dla zupełnie nowego odwołania.</span><span class="sxs-lookup"><span data-stu-id="666b0-123">This table describes the [Referral](referral-resources.md) properties in the request body for a brand new referral.</span></span>

| <span data-ttu-id="666b0-124">Właściwość</span><span class="sxs-lookup"><span data-stu-id="666b0-124">Property</span></span>            | <span data-ttu-id="666b0-125">Typ</span><span class="sxs-lookup"><span data-stu-id="666b0-125">Type</span></span>                                                                 | <span data-ttu-id="666b0-126">Opis</span><span class="sxs-lookup"><span data-stu-id="666b0-126">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="666b0-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="666b0-127">Name</span></span>                | <span data-ttu-id="666b0-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="666b0-128">string</span></span>                                                               | <span data-ttu-id="666b0-129">Nazwa odwołania.</span><span class="sxs-lookup"><span data-stu-id="666b0-129">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="666b0-130">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="666b0-130">ExternalReferenceId</span></span> | <span data-ttu-id="666b0-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="666b0-131">string</span></span>                                                               | <span data-ttu-id="666b0-132">Zewnętrzny identyfikator odwołania.</span><span class="sxs-lookup"><span data-stu-id="666b0-132">An external identifier for the referral.</span></span> <span data-ttu-id="666b0-133">Na przykład Twój własny identyfikator klienta Dynamics 365 lub identyfikatora szansy sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="666b0-133">For example, your own Dynamics 365 lead or opportunity ID.</span></span>                   |
| <span data-ttu-id="666b0-134">Stan</span><span class="sxs-lookup"><span data-stu-id="666b0-134">Status</span></span>              | [<span data-ttu-id="666b0-135">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="666b0-135">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="666b0-136">[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan odwołania.</span><span class="sxs-lookup"><span data-stu-id="666b0-136">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="666b0-137">Substatus</span><span class="sxs-lookup"><span data-stu-id="666b0-137">Substatus</span></span>           | [<span data-ttu-id="666b0-138">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="666b0-138">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="666b0-139">[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi podstan odwołania.</span><span class="sxs-lookup"><span data-stu-id="666b0-139">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral substatus.</span></span>       |
| <span data-ttu-id="666b0-140">StatusReason</span><span class="sxs-lookup"><span data-stu-id="666b0-140">StatusReason</span></span>        | <span data-ttu-id="666b0-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="666b0-141">string</span></span>                                                               | <span data-ttu-id="666b0-142">Opisowy komunikat o stanie.</span><span class="sxs-lookup"><span data-stu-id="666b0-142">A descriptive message about the status.</span></span> <span data-ttu-id="666b0-143">Na przykład Wyjaśnij, dlaczego odwołanie zostało utracone.</span><span class="sxs-lookup"><span data-stu-id="666b0-143">For example, explain why the referral was lost.</span></span>                            |
| <span data-ttu-id="666b0-144">— Odwołanie</span><span class="sxs-lookup"><span data-stu-id="666b0-144">ReferralType</span></span>        | [<span data-ttu-id="666b0-145">— Odwołanie</span><span class="sxs-lookup"><span data-stu-id="666b0-145">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="666b0-146">Reprezentuje typ odwołania.</span><span class="sxs-lookup"><span data-stu-id="666b0-146">Represents the referral type.</span></span> <span data-ttu-id="666b0-147">**Wymagane.**</span><span class="sxs-lookup"><span data-stu-id="666b0-147">**Required.**</span></span>                                                                                        |
| <span data-ttu-id="666b0-148">Kwalifikacja</span><span class="sxs-lookup"><span data-stu-id="666b0-148">Qualification</span></span>       | [<span data-ttu-id="666b0-149">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="666b0-149">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="666b0-150">Reprezentuje jakość odwołania.</span><span class="sxs-lookup"><span data-stu-id="666b0-150">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="666b0-151">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="666b0-151">CustomerProfile</span></span>     | [<span data-ttu-id="666b0-152">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="666b0-152">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="666b0-153">Informacje kontaktowe klienta.</span><span class="sxs-lookup"><span data-stu-id="666b0-153">Customer contact information.</span></span>  <span data-ttu-id="666b0-154">**Wymagane.**</span><span class="sxs-lookup"><span data-stu-id="666b0-154">**Required.**</span></span>                                                                                      |
| <span data-ttu-id="666b0-155">Wyrażanie zgody</span><span class="sxs-lookup"><span data-stu-id="666b0-155">Consent</span></span>             | [<span data-ttu-id="666b0-156">Wyrażanie zgody</span><span class="sxs-lookup"><span data-stu-id="666b0-156">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="666b0-157">Flagi zgody na udostępnianie informacji innym organizacjom i Zezwalanie na kontakt z użytkownikami. **Wymagane.**</span><span class="sxs-lookup"><span data-stu-id="666b0-157">Consent flags around sharing information with other organizations and allowing them to contact users.**Required.**</span></span>               |
| <span data-ttu-id="666b0-158">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="666b0-158">Details</span></span>             | [<span data-ttu-id="666b0-159">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="666b0-159">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="666b0-160">Szczegóły klienta, notatki, wartość transakcji, Data zamknięcia waluty.</span><span class="sxs-lookup"><span data-stu-id="666b0-160">Customer details, notes, deal value, currency closing date.</span></span> <span data-ttu-id="666b0-161">**Wymagane.**</span><span class="sxs-lookup"><span data-stu-id="666b0-161">**Required.**</span></span>                                                           |
| <span data-ttu-id="666b0-162">Zespół</span><span class="sxs-lookup"><span data-stu-id="666b0-162">Team</span></span>                | [<span data-ttu-id="666b0-163">Członek</span><span class="sxs-lookup"><span data-stu-id="666b0-163">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="666b0-164">Reprezentuje użytkowników w organizacjach, które są zaangażowane w zaangażowanie partnerskie.</span><span class="sxs-lookup"><span data-stu-id="666b0-164">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="666b0-165">InviteContext</span><span class="sxs-lookup"><span data-stu-id="666b0-165">InviteContext</span></span>       | [<span data-ttu-id="666b0-166">InviteContext</span><span class="sxs-lookup"><span data-stu-id="666b0-166">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="666b0-167">Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera.</span><span class="sxs-lookup"><span data-stu-id="666b0-167">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="666b0-168">Cel</span><span class="sxs-lookup"><span data-stu-id="666b0-168">Target</span></span>         | [<span data-ttu-id="666b0-169">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="666b0-169">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="666b0-170">Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera.</span><span class="sxs-lookup"><span data-stu-id="666b0-170">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

#### <a name="status--substatus-transition-states"></a><span data-ttu-id="666b0-171">Stan przejścia & stanu Substatus</span><span class="sxs-lookup"><span data-stu-id="666b0-171">Status & Substatus transition states</span></span>

| <span data-ttu-id="666b0-172">Stan</span><span class="sxs-lookup"><span data-stu-id="666b0-172">Status</span></span> | <span data-ttu-id="666b0-173">Dozwolone przejście stanu</span><span class="sxs-lookup"><span data-stu-id="666b0-173">Allowed status transition</span></span> | <span data-ttu-id="666b0-174">Dozwolony stan Substatus</span><span class="sxs-lookup"><span data-stu-id="666b0-174">Allowed substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="666b0-175">Nowy</span><span class="sxs-lookup"><span data-stu-id="666b0-175">New</span></span>    | <span data-ttu-id="666b0-176">Nowy, aktywny, zamknięty</span><span class="sxs-lookup"><span data-stu-id="666b0-176">New, Active, Closed</span></span>       | <span data-ttu-id="666b0-177">Oczekiwanie, odebrano</span><span class="sxs-lookup"><span data-stu-id="666b0-177">Pending, Received</span></span>            |
| <span data-ttu-id="666b0-178">Aktywna</span><span class="sxs-lookup"><span data-stu-id="666b0-178">Active</span></span> | <span data-ttu-id="666b0-179">Aktywne, zamknięte</span><span class="sxs-lookup"><span data-stu-id="666b0-179">Active, Closed</span></span>            | <span data-ttu-id="666b0-180">Zaakceptowano</span><span class="sxs-lookup"><span data-stu-id="666b0-180">Accepted</span></span>                     |
| <span data-ttu-id="666b0-181">Zamknięty</span><span class="sxs-lookup"><span data-stu-id="666b0-181">Closed</span></span> | <span data-ttu-id="666b0-182">Zamknięty</span><span class="sxs-lookup"><span data-stu-id="666b0-182">Closed</span></span>                    | <span data-ttu-id="666b0-183">Wygrane, utracone, odrzucone, wygasłe</span><span class="sxs-lookup"><span data-stu-id="666b0-183">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="666b0-184">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="666b0-184">Request example</span></span>

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="666b0-185">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="666b0-185">REST Response</span></span>

<span data-ttu-id="666b0-186">Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [odwołania](referral-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="666b0-186">If successful, this method returns the populated [Referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="666b0-187">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="666b0-187">Response success and error codes</span></span>

<span data-ttu-id="666b0-188">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="666b0-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="666b0-189">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="666b0-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="666b0-190">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="666b0-190">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="666b0-191">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="666b0-191">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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

## <a name="create-a-shared-referral"></a><span data-ttu-id="666b0-192">Utwórz odwołanie udostępnione</span><span class="sxs-lookup"><span data-stu-id="666b0-192">Create a shared referral</span></span>

<span data-ttu-id="666b0-193">Istnieją dwa kroki umożliwiające utworzenie odwołania do **udostępnionego** [typu odwołania](referral-resources.md#referraltype).</span><span class="sxs-lookup"><span data-stu-id="666b0-193">There are two steps to create a referral of the **Shared** [referral type](referral-resources.md#referraltype).</span></span>

1. [<span data-ttu-id="666b0-194">Utwórz udostępnione odwołanie</span><span class="sxs-lookup"><span data-stu-id="666b0-194">Create your shared referral</span></span>](#create-your-referral)
2. [<span data-ttu-id="666b0-195">Utwórz połączone odwołanie dla drugiej strony</span><span class="sxs-lookup"><span data-stu-id="666b0-195">Create a connected referral for the second party</span></span>](#create-a-connected-referral)

<span data-ttu-id="666b0-196">Poniższy wykres przepływu ilustruje te dwa kroki tworzenia udostępnionego odwołania.</span><span class="sxs-lookup"><span data-stu-id="666b0-196">The following flow chart illustrates these two steps in creating a shared referral.</span></span>

![Wykres przepływu przedstawiający udostępnione odwołanie z 2 odwołaniami połączonymi za pomocą interfejsu API partnera firmy Microsoft](../images/SharedReferral.png)

### <a name="create-your-referral"></a><span data-ttu-id="666b0-198">Utwórz odwołanie</span><span class="sxs-lookup"><span data-stu-id="666b0-198">Create your referral</span></span>

1. <span data-ttu-id="666b0-199">Utwórz odwołanie z atrybutem [Referrtype](referral-resources.md#referraltype) ustawionym na wartość Shared.</span><span class="sxs-lookup"><span data-stu-id="666b0-199">Create a referral with [ReferralType](referral-resources.md#referraltype) set to shared.</span></span>
2. <span data-ttu-id="666b0-200">Skopiuj **engagementId** z odpowiedzi zwracanej.</span><span class="sxs-lookup"><span data-stu-id="666b0-200">Copy the **engagementId** from the return response.</span></span>

<span data-ttu-id="666b0-201">Przykład [ReferralTarget](referral-resources.md#target) do odwołania</span><span class="sxs-lookup"><span data-stu-id="666b0-201">[ReferralTarget](referral-resources.md#target) sample for referral</span></span>

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a><span data-ttu-id="666b0-202">Utwórz połączone odwołanie</span><span class="sxs-lookup"><span data-stu-id="666b0-202">Create a connected referral</span></span>

1. <span data-ttu-id="666b0-203">Utwórz inne odwołanie do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="666b0-203">Create another referral for Microsoft.</span></span>
2. <span data-ttu-id="666b0-204">Uwzględnij **enagementId** z odwołania, aby były powiązane ze sobą.</span><span class="sxs-lookup"><span data-stu-id="666b0-204">Include the **enagementId** from your referral so they are tied together.</span></span>

<span data-ttu-id="666b0-205">Przykład [ReferralTarget](referral-resources.md#target) dla odwołania firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="666b0-205">[ReferralTarget](referral-resources.md#target) sample for Microsoft referral</span></span>

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```