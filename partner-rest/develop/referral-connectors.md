---
title: Łączniki odwołań.
description: Synchronizuj odwołania partnerów z klientami Dynamics 365 CRM przy użyciu Microsoft Flow.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0a62023feb03114bb7ba1136b7700875f24c2e01
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770474"
---
# <a name="referral-connectors"></a><span data-ttu-id="47184-103">Łączniki odwołań</span><span class="sxs-lookup"><span data-stu-id="47184-103">Referral connectors</span></span>

<span data-ttu-id="47184-104">Łączników odwołań można używać do synchronizowania odwołań partnerów z klientami zarządzania relacjami z klientami (CRM).</span><span class="sxs-lookup"><span data-stu-id="47184-104">You can use referral connectors to synchronize partner referrals with customer relationship management (CRM) leads.</span></span> <span data-ttu-id="47184-105">Łącznik odwołań można utworzyć za pomocą [Microsoft Flow](https://flow.microsoft.com) jako punkt końcowy HTTPS do odbierania odwołań partnerów.</span><span class="sxs-lookup"><span data-stu-id="47184-105">You can create a referral connector using [Microsoft Flow](https://flow.microsoft.com) as the HTTPS endpoint to receive partner referrals.</span></span> <span data-ttu-id="47184-106">Następnie można napisać odwołanie otrzymane przez przepływ do systemu CRM jako potencjalnego klienta.</span><span class="sxs-lookup"><span data-stu-id="47184-106">You can then write the referral received by the flow to a CRM system as a lead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47184-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47184-107">Prerequisites</span></span>

* <span data-ttu-id="47184-108">Subskrypcja Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="47184-108">Microsoft Flow subscription</span></span>
  * <span data-ttu-id="47184-109">Konto z dostępem administratorów do tej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="47184-109">Account with administrator access to this subscription</span></span>
* <span data-ttu-id="47184-110">Azure Active Directory (Azure AD) identyfikator aplikacji, identyfikator użytkownika, hasło i identyfikator dzierżawy (używane do uzyskiwania dostępu do interfejsu API partnera).</span><span class="sxs-lookup"><span data-stu-id="47184-110">Azure Active Directory (Azure AD) application ID, user id, password and tenant ID (used to access the Partner API).</span></span> <span data-ttu-id="47184-111">Instrukcje dotyczące instalacji znajdują się w temacie [uwierzytelnianie partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="47184-111">For setup instructions, see [Partner authentication](api-authentication.md).</span></span>
* <span data-ttu-id="47184-112">Subskrypcja [aplikacji funkcji platformy Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) .</span><span class="sxs-lookup"><span data-stu-id="47184-112">[Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) subscription.</span></span>
* <span data-ttu-id="47184-113">Subskrypcja [zdarzeń elementu webhook Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) w celu [utworzenia odwołania](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) i [odwołania do zaktualizowanych](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="47184-113">[Partner Center webhook event](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) events.</span></span>
* <span data-ttu-id="47184-114">Subskrypcja [systemu Microsoft Dynamics 365](https://dynamics.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="47184-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) subscription</span></span>
  * <span data-ttu-id="47184-115">Włączono moduł sprzedaży</span><span class="sxs-lookup"><span data-stu-id="47184-115">Sales module enabled</span></span>
  * <span data-ttu-id="47184-116">Konto z dostępem administratorów do tej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="47184-116">Account with administrator access to this subscription</span></span>

## <a name="flow-overview"></a><span data-ttu-id="47184-117">Omówienie przepływu</span><span class="sxs-lookup"><span data-stu-id="47184-117">Flow overview</span></span>

<span data-ttu-id="47184-118">Odwołania są importowane do programu CRM przy użyciu następującego przepływu:</span><span class="sxs-lookup"><span data-stu-id="47184-118">Referrals are imported into the CRM using the following flow:</span></span>

1. <span data-ttu-id="47184-119">Partner konfiguruje element webhook w celu otrzymywania powiadomień o odwołaniach.</span><span class="sxs-lookup"><span data-stu-id="47184-119">Partner sets up a webhook to receive referral notifications.</span></span>
2. <span data-ttu-id="47184-120">Partner rejestruje element webhook w centrum partnerskim.</span><span class="sxs-lookup"><span data-stu-id="47184-120">Partner registers the webhook with Partner Center.</span></span> <span data-ttu-id="47184-121">Partner również subskrybuje zdarzenia elementu webhook w przypadku tworzenia lub aktualizowania odwołań.</span><span class="sxs-lookup"><span data-stu-id="47184-121">The partner also subscribes to webhook events for when referrals are created or updated.</span></span>
3. <span data-ttu-id="47184-122">Klient referencyjny tworzy lub aktualizuje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="47184-122">Referral client creates or updates a referral.</span></span>
4. <span data-ttu-id="47184-123">System webhook Centrum partnerskiego sprawdza rejestrację partnera i wysyła powiadomienie do elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="47184-123">Partner Center webhook system checks for the partner's registration and sends a notification to the webhook.</span></span>
5. <span data-ttu-id="47184-124">Element webhook odbiera powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="47184-124">Webhook receives the notification.</span></span>
6. <span data-ttu-id="47184-125">Dokument przepływu w usłudze Microsoft Flow używa tokenu do wywołania interfejsu API referencyjnego Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="47184-125">Flow document in Microsoft flow uses a token to make a call to the Partner Center referral API.</span></span>
7. <span data-ttu-id="47184-126">Punkt końcowy przepływu pobiera odwołanie.</span><span class="sxs-lookup"><span data-stu-id="47184-126">Flow endpoint gets the referral.</span></span>
8. <span data-ttu-id="47184-127">Punkt końcowy przepływu tworzy lidera CRM.</span><span class="sxs-lookup"><span data-stu-id="47184-127">Flow endpoint creates the CRM lead.</span></span>

![Wykres przepływu przedstawiający kroki opisane w tej sekcji w celu zaimportowania odwołań partnerów do programu CRM.](../images/referralwebhook.png)

## <a name="flow-document-process"></a><span data-ttu-id="47184-129">Proces dokumentu przepływu</span><span class="sxs-lookup"><span data-stu-id="47184-129">Flow document process</span></span>

<span data-ttu-id="47184-130">Dokument przepływu dla łącznika odwołań synchronizuje odwołanie partnera z liderem programu CRM z usługi Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="47184-130">The flow document for a referral connector synchronizes a partner referral with a CRM lead from Dynamics 365.</span></span>

1. <span data-ttu-id="47184-131">Łącznik pobiera token, z którym ma zostać nawiązane połączenie `https://api.partner.microsoft.com/v1.0/engagements/referrals` .</span><span class="sxs-lookup"><span data-stu-id="47184-131">Connector gets a token to connect to `https://api.partner.microsoft.com/v1.0/engagements/referrals`.</span></span>
2. <span data-ttu-id="47184-132">Łącznik uzyskuje odwołanie, które wyzwoliło łącznik przy użyciu `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .</span><span class="sxs-lookup"><span data-stu-id="47184-132">Connector obtains referral that triggered the connector using `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}`.</span></span>
3. <span data-ttu-id="47184-133">Łącznik nawiązuje połączenie z usługą Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="47184-133">Connector connects to Dynamics 365.</span></span>
4. <span data-ttu-id="47184-134">Łącznik tworzy nowego potencjalnego klienta lub aktualizuje istniejącego potencjalnego klienta z najnowszymi informacjami na temat odwołania.</span><span class="sxs-lookup"><span data-stu-id="47184-134">Connector creates a new lead or updates an existing lead with the latest information on the referral.</span></span>
5. <span data-ttu-id="47184-135">Łącznik aktualizuje odwołania z najnowszymi aktualizacjami z poziomu lidera programu CRM.</span><span class="sxs-lookup"><span data-stu-id="47184-135">Connector updates referral with the latest updates from the CRM lead.</span></span>

![Wykres przepływu przedstawiający kroki opisane w tej sekcji dla procesu dokumentu przepływu.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a><span data-ttu-id="47184-137">Przykładowy łącznik odwołań</span><span class="sxs-lookup"><span data-stu-id="47184-137">Sample referral connector</span></span>

<span data-ttu-id="47184-138">Poniższy *przykładowy łącznik odwołań* pokazuje, jak synchronizować odwołania Centrum partnerskiego z potencjalnymi klientami programu CRM w usłudze Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="47184-138">The following *sample referral connector* shows how to synchronize Partner Center referrals to CRM leads in Dynamics 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47184-139">Możesz pisać do różnych CRMs, zastępując [Łączniki Flow](https://flow.microsoft.com/en-us/connectors/) w przykładowym kodzie.</span><span class="sxs-lookup"><span data-stu-id="47184-139">You can write to different CRMs by replacing the [flow connectors](https://flow.microsoft.com/en-us/connectors/) in the sample code.</span></span>

### <a name="import-flow-synchronization-package"></a><span data-ttu-id="47184-140">Importuj pakiet synchronizacji przepływu</span><span class="sxs-lookup"><span data-stu-id="47184-140">Import flow synchronization package</span></span>

<span data-ttu-id="47184-141">Pobierz i zaimportuj *przykładowy pakiet kodu* do Microsoft Flow i Połącz się z usługą Dynamics 365:</span><span class="sxs-lookup"><span data-stu-id="47184-141">Download and import the *sample code package* into Microsoft Flow and connect to Dynamics 365:</span></span>

1. <span data-ttu-id="47184-142">Pobierz [pakiet synchronizacji przepływu](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) z [repozytorium GitHub](https://github.com/microsoft/Partner-Center-Referrals).</span><span class="sxs-lookup"><span data-stu-id="47184-142">Download the [flow synchronization package](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) from the [GitHub repo](https://github.com/microsoft/Partner-Center-Referrals).</span></span>
2. <span data-ttu-id="47184-143">Zaloguj się do [Microsoft Flow](https://flow.microsoft.com) przy użyciu odpowiednich poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="47184-143">Sign in to [Microsoft Flow](https://flow.microsoft.com) using the appropriate credentials.</span></span>
3. <span data-ttu-id="47184-144">Wybierz pozycję **Moje przepływy** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="47184-144">Choose **My Flows** in the navigation menu.</span></span> <span data-ttu-id="47184-145">Następnie wybierz pozycję **Importuj**.</span><span class="sxs-lookup"><span data-stu-id="47184-145">Then choose **Import**.</span></span>
4. <span data-ttu-id="47184-146">Na stronie **Importuj pakiet** wybierz pobrany pakiet synchronizacji przepływu.</span><span class="sxs-lookup"><span data-stu-id="47184-146">On the **Import package** page, select the flow synchronization package that you downloaded.</span></span> <span data-ttu-id="47184-147">Następnie wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="47184-147">Then choose **Upload**.</span></span>

    ![Ekran importowania pakietu dla plików pakietu](../images/importPackage.png)

5. <span data-ttu-id="47184-149">Po zakończeniu przekazywania pakietu Znajdź pakiet, który został przekazany w **zawartości recenzowania** pakietu.</span><span class="sxs-lookup"><span data-stu-id="47184-149">After the package upload is complete, find the package you uploaded in the **Review Package Content** .</span></span>

    ![Szczegóły ekranu importowania pakietu](../images/importPackageDetails.png)

6. <span data-ttu-id="47184-151">Wybierz przycisk **akcji** (ikona ołówka) dla przekazanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="47184-151">Choose the **Action** button (pencil icon) for your uploaded package.</span></span> <span data-ttu-id="47184-152">Spowoduje to otwarcie bloku **Importuj konfigurację** .</span><span class="sxs-lookup"><span data-stu-id="47184-152">This opens the **Import setup** blade.</span></span>
7. <span data-ttu-id="47184-153">Wybierz typ **instalacji** .</span><span class="sxs-lookup"><span data-stu-id="47184-153">Choose your **Setup** type.</span></span>

    * <span data-ttu-id="47184-154">Aby utworzyć nowy przepływ, wybierz pozycję **Utwórz jako nowy** i wprowadź nową **nazwę zasobu**.</span><span class="sxs-lookup"><span data-stu-id="47184-154">To create a new flow, select **Create as new**, and enter a new **Resource name**.</span></span>
    * <span data-ttu-id="47184-155">Aby zaktualizować istniejący przepływ o tej samej nazwie, wybierz pozycję **Aktualizuj**.</span><span class="sxs-lookup"><span data-stu-id="47184-155">To update an existing flow with the same name, select **Update**.</span></span>

    ![Utwórz lub zaktualizuj nowy ekran uaktualniający](../images/CreateNewConnection.png)

8. <span data-ttu-id="47184-157">Na stronie **Importuj pakiet** Znajdź połączenie Dynamics 365 w sekcji **Przejrzyj zawartość pakietu** w obszarze **powiązane zasoby**.</span><span class="sxs-lookup"><span data-stu-id="47184-157">On the **Import package** page, find your Dynamics 365 connection in the **Review Package Content** section under **Related Resources**.</span></span>
9. <span data-ttu-id="47184-158">Wybierz przycisk **akcji** (ikona ołówka) dla połączenia z usługą Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="47184-158">Choose the **Action** button (pencil icon) for your Dynamics 365 connection.</span></span> <span data-ttu-id="47184-159">Spowoduje to otwarcie bloku **Konfiguracja** dla tego powiązanego zasobu.</span><span class="sxs-lookup"><span data-stu-id="47184-159">This opens the **Import setup** blade for this related resource.</span></span>
10. <span data-ttu-id="47184-160">Wybierz pozycję **Utwórz nowy** , aby utworzyć nowe połączenie usługi Dynamics 365 lub Wybierz istniejące połączenie.</span><span class="sxs-lookup"><span data-stu-id="47184-160">Choose **Create new** to create a new Dynamics 365 connection, or select an existing connection.</span></span>
11. <span data-ttu-id="47184-161">Sprawdź, czy na stronie **Importowanie pakietu** jest teraz widoczny wybrany typ instalacji przepływu i połączenie z usługą Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="47184-161">Verify that the **Import package** page now shows your selected flow setup type and Dynamics 365 connection.</span></span> <span data-ttu-id="47184-162">Następnie wybierz pozycję **Importuj**.</span><span class="sxs-lookup"><span data-stu-id="47184-162">Then choose **Import**.</span></span>

    ![Ekran stanu pakietu importowania](../images/importStatus.png)

12. <span data-ttu-id="47184-164">Sprawdź, czy zasób przepływu został utworzony lub zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="47184-164">Verify that your flow resource is now created or updated.</span></span>

### <a name="configure-flow-parameters"></a><span data-ttu-id="47184-165">Konfigurowanie parametrów przepływu</span><span class="sxs-lookup"><span data-stu-id="47184-165">Configure flow parameters</span></span>

<span data-ttu-id="47184-166">Skonfiguruj parametry zasobu przepływu:</span><span class="sxs-lookup"><span data-stu-id="47184-166">Configure the parameters of your flow resource:</span></span>

1. <span data-ttu-id="47184-167">W [Microsoft Flow](https://flow.microsoft.com)wybierz pozycję **Moje przepływy** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="47184-167">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="47184-168">Wybierz utworzony lub zaktualizowany zasób przepływu w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="47184-168">Choose the flow resource you created or updated in the previous section.</span></span>
3. <span data-ttu-id="47184-169">Na stronie Flow (przepływ) wybierz pozycję **Edytuj przepływ**.</span><span class="sxs-lookup"><span data-stu-id="47184-169">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="47184-170">Wybierz zmienną **identyfikatora AAD-Application (Client)** i wprowadź identyfikator aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47184-170">Choose the **AAD-Application (client) ID** variable and enter the ID of your Azure AD application.</span></span>
5. <span data-ttu-id="47184-171">Wybierz zmienną **UserID** i wprowadź swój identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47184-171">Choose the **UserId** variable and enter your user ID.</span></span>
6. <span data-ttu-id="47184-172">Wybierz zmienną **userPassword** i wprowadź hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47184-172">Choose the **UserPassword** variable and enter your user password.</span></span>
7. <span data-ttu-id="47184-173">Wybierz zmienną **identyfikatora AAD-Directory (dzierżawa)** .</span><span class="sxs-lookup"><span data-stu-id="47184-173">Select the **AAD-Directory (tenant) ID** variable.</span></span> <span data-ttu-id="47184-174">Wprowadź identyfikator dzierżawy aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47184-174">Enter the tenant ID of your Azure AD application.</span></span>
8. <span data-ttu-id="47184-175">Wybierz pozycję **Zapisz** , aby zapisać przepływ.</span><span class="sxs-lookup"><span data-stu-id="47184-175">Choose **Save** to save your flow.</span></span>

    ![Ekran ustawień zmiennych przepływu](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a><span data-ttu-id="47184-177">Uwierzytelnianie wywołania zwrotnego</span><span class="sxs-lookup"><span data-stu-id="47184-177">Authenticate the callback</span></span>

<span data-ttu-id="47184-178">Uwierzytelnij zdarzenie wywołania zwrotnego z Centrum partnerskiego:</span><span class="sxs-lookup"><span data-stu-id="47184-178">Authenticate the callback event from the Partner Center:</span></span>

> [!TIP]
> <span data-ttu-id="47184-179">Aby zapoznać się z przykładem, zobacz [kod aplikacji funkcji przykładowej](#sample-function-app-code) w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="47184-179">For an example, see the [sample function app code](#sample-function-app-code) in the following section.</span></span>

1. <span data-ttu-id="47184-180">[Utwórz aplikację funkcji platformy Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) , która [uwierzytelnia zdarzenie wywołania zwrotnego z Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span><span class="sxs-lookup"><span data-stu-id="47184-180">[Create an Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) that [authenticates the callback event from the Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span></span>

    1. <span data-ttu-id="47184-181">Sprawdź, czy istnieją wymagane nagłówki (**Authorization**, **x-MS-Certificate-URL** i **x-MS-Signature-Algorithm**).</span><span class="sxs-lookup"><span data-stu-id="47184-181">Verify that the required headers are present (**Authorization**, **x-ms-certificate-url**, and **x-ms-signature-algorithm**).</span></span>
    2. <span data-ttu-id="47184-182">Pobierz certyfikat używany do podpisywania zawartości (**x-MS-Certificate-URL**).</span><span class="sxs-lookup"><span data-stu-id="47184-182">Download the certificate used to sign the content (**x-ms-certificate-url**).</span></span>
    3. <span data-ttu-id="47184-183">Sprawdź łańcuch certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="47184-183">Verify the certificate chain.</span></span>
    4. <span data-ttu-id="47184-184">Sprawdź **organizację** certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="47184-184">Verify the **Organization** of the certificate.</span></span>
    5. <span data-ttu-id="47184-185">Zapoznaj się z zawartością przy użyciu kodowania UTF-8 w buforze.</span><span class="sxs-lookup"><span data-stu-id="47184-185">Read the content with UTF-8 encoding into a buffer.</span></span>
    6. <span data-ttu-id="47184-186">Utwórz dostawcę usług kryptograficznych RSA.</span><span class="sxs-lookup"><span data-stu-id="47184-186">Create an RSA Crypto Provider.</span></span>
    7. <span data-ttu-id="47184-187">[Sprawdź, czy sygnatura pasuje](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) do tego, co było podpisane przy użyciu określonego algorytmu wyznaczania wartości skrótu (na przykład SHA256).</span><span class="sxs-lookup"><span data-stu-id="47184-187">[Verify that the signature matches](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) what was signed with the specified hash algorithm (for example, SHA256).</span></span>
    8. <span data-ttu-id="47184-188">Jeśli weryfikacja zakończy się pomyślnie, zostanie zwrócony komunikat **OK** .</span><span class="sxs-lookup"><span data-stu-id="47184-188">If the verification succeeds, an **OK** message is returned.</span></span>

2. <span data-ttu-id="47184-189">Zanotuj wygenerowany identyfikator URI wywołania zwrotnego dla punktu końcowego HTTP aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="47184-189">Note the generated callback URI for your function app's HTTP endpoint.</span></span> <span data-ttu-id="47184-190">Ten identyfikator URI jest wyświetlany podczas tworzenia aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="47184-190">This URI is displayed when you create your function app.</span></span> <span data-ttu-id="47184-191">Możesz również znaleźć ten identyfikator URI na stronie zasobów platformy Azure w aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="47184-191">You can also find this URI on your function app's Azure resource page.</span></span>
3. <span data-ttu-id="47184-192">W [Microsoft Flow](https://flow.microsoft.com)Edytuj przepływ "odwolanie partnera do programu Microsoft Dynamics CRM ołów" zaimportowany w sekcji *[Importuj pakiet synchronizacji przepływu](#import-flow-synchronization-package)*.</span><span class="sxs-lookup"><span data-stu-id="47184-192">In [Microsoft Flow](https://flow.microsoft.com), edit the flow "Partner Referral to Microsoft Dynamics CRM Lead" that you imported in the section *[Import flow synchronization package](#import-flow-synchronization-package)*.</span></span>

    1. <span data-ttu-id="47184-193">Dodaj wartość identyfikatora URI aplikacji funkcji do kroku "Walidacja certyfikatu elementu webhook".</span><span class="sxs-lookup"><span data-stu-id="47184-193">Add the value of the function app's URI to the "web hook certificate validation" step.</span></span>
    2. <span data-ttu-id="47184-194">Skopiuj i wklej identyfikator URI wywołania zwrotnego aplikacji funkcji do dokumentu przepływu.</span><span class="sxs-lookup"><span data-stu-id="47184-194">Copy and paste your function app's callback URI into the flow document.</span></span>
    3. <span data-ttu-id="47184-195">Zapisz dokument przepływu.</span><span class="sxs-lookup"><span data-stu-id="47184-195">Save your flow document.</span></span>

#### <a name="sample-function-app-code"></a><span data-ttu-id="47184-196">Przykładowy kod aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="47184-196">Sample function app code</span></span>

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### <a name="register-flow-with-partner-center"></a><span data-ttu-id="47184-197">Rejestrowanie przepływu w centrum partnerskim</span><span class="sxs-lookup"><span data-stu-id="47184-197">Register flow with Partner Center</span></span>

<span data-ttu-id="47184-198">Zarejestruj zasób przepływu w centrum partnerskim, aby wyzwolić przepływ i odbierać zdarzenia elementu webhook:</span><span class="sxs-lookup"><span data-stu-id="47184-198">Register your flow resource with the Partner Center to trigger the flow and receive webhook events:</span></span>

1. <span data-ttu-id="47184-199">W [Microsoft Flow](https://flow.microsoft.com)wybierz pozycję **Moje przepływy** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="47184-199">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="47184-200">Wybierz utworzony lub zaktualizowany przepływ.</span><span class="sxs-lookup"><span data-stu-id="47184-200">Choose the flow you created or updated.</span></span>
3. <span data-ttu-id="47184-201">Na stronie Flow (przepływ) wybierz pozycję **Edytuj przepływ**.</span><span class="sxs-lookup"><span data-stu-id="47184-201">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="47184-202">Skopiuj i Zapisz **adres URL post protokołu HTTP** dla przepływu.</span><span class="sxs-lookup"><span data-stu-id="47184-202">Copy and save the flow's **HTTP POST URL**.</span></span> <span data-ttu-id="47184-203">Musisz użyć tego adresu URL, aby wyzwolić przepływ.</span><span class="sxs-lookup"><span data-stu-id="47184-203">You will need to use this URL to trigger the flow.</span></span>
5. <span data-ttu-id="47184-204">[Zarejestruj się, aby otrzymywać zdarzenia elementu webhook](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) podczas tworzenia lub aktualizowania odwołań.</span><span class="sxs-lookup"><span data-stu-id="47184-204">[Register to receive webhook events](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) when referrals are created or updated.</span></span> <span data-ttu-id="47184-205">Użyj następującego formatu treści:</span><span class="sxs-lookup"><span data-stu-id="47184-205">Use the following body format:</span></span>

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```
