---
title: Uwierzytelnianie interfejsu API Partner
description: Skonfiguruj ustawienia uwierzytelniania, aby do uwierzytelniania używać interfejsu API partnera z usługą Azure AD.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c5810678dccc2be1c3c084c901299961d6ba7820
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770503"
---
# <a name="partner-api-authentication"></a><span data-ttu-id="4f89d-103">Uwierzytelnianie interfejsu API Partner</span><span class="sxs-lookup"><span data-stu-id="4f89d-103">Partner API authentication</span></span>

<span data-ttu-id="4f89d-104">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="4f89d-104">Applies to:</span></span>

- <span data-ttu-id="4f89d-105">Interfejs API partnera</span><span class="sxs-lookup"><span data-stu-id="4f89d-105">Partner API</span></span>

<span data-ttu-id="4f89d-106">Interfejs API partnera wykorzystuje Azure Active Directory (Azure AD) do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="4f89d-106">The Partner API utilizes Azure Active Directory (Azure AD) for authentication.</span></span> <span data-ttu-id="4f89d-107">W przypadku korzystania z interfejsu API partnera należy prawidłowo skonfigurować aplikację usługi Azure AD i uzyskać token dostępu.</span><span class="sxs-lookup"><span data-stu-id="4f89d-107">When you interact with the Partner API, you must correctly configure an Azure AD application and obtain an access token.</span></span> <span data-ttu-id="4f89d-108">Możesz uzyskać tokeny dostępu dla dostępu do [aplikacji i użytkowników](#application-and-user-access) lub [dostępu tylko do aplikacji](#application-only-access).</span><span class="sxs-lookup"><span data-stu-id="4f89d-108">You can obtain access tokens for [application and user access](#application-and-user-access) or [application-only access](#application-only-access).</span></span>

## <a name="application-and-user-access"></a><span data-ttu-id="4f89d-109">Dostęp do aplikacji i użytkowników</span><span class="sxs-lookup"><span data-stu-id="4f89d-109">Application and user access</span></span>

<span data-ttu-id="4f89d-110">Ta metoda jest zalecana do konfigurowania **dostępu aplikacji i użytkowników** do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4f89d-110">This method is recommended to set up **application and user access** to the API.</span></span>

1. <span data-ttu-id="4f89d-111">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f89d-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4f89d-112">Wybierz usługę **Azure Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="4f89d-112">Choose the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="4f89d-113">Wybierz **rejestracje aplikacji**, a następnie wybierz pozycję **rejestracja nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-113">Choose **App registrations**, then choose **New application registration**.</span></span>
4. <span data-ttu-id="4f89d-114">Utwórz nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="4f89d-114">Create your new application.</span></span> <span data-ttu-id="4f89d-115">W obszarze **Typ aplikacji** wybierz opcję **natywny**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-115">For **Application type**, select **Native**.</span></span> <span data-ttu-id="4f89d-116">Podaj nazwę i adres URL, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-116">Provide a name and URL, then select **Create**.</span></span>
5. <span data-ttu-id="4f89d-117">Wybierz **uprawnienia interfejsu API** dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4f89d-117">Choose **API permissions** for the application.</span></span> <span data-ttu-id="4f89d-118">Na ekranie **Żądaj uprawnień interfejsu API** wybierz opcję **Dodaj uprawnienia**, a następnie wybierz **interfejsy API, których używa Moja organizacja**</span><span class="sxs-lookup"><span data-stu-id="4f89d-118">On the **Request API permissions** screen, choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="4f89d-119">Wyszukaj *partnera firmy Microsoft* (*Microsoft Dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).</span><span class="sxs-lookup"><span data-stu-id="4f89d-119">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Zrzut ekranu przedstawiający ekran uprawnień interfejsu API żądania z wyszukiwaniem interfejsu API partnera firmy Microsoft](../images/SearchGatewayApi.png)

7. <span data-ttu-id="4f89d-121">Ustaw **delegowane uprawnienia** do **Centrum partnerskiego**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-121">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Zrzut ekranu przedstawiający ekran konfiguracja uprawnień delegowanych dla interfejsu API partnera firmy Microsoft](../images/SelectUserPermission.png)
    
8. <span data-ttu-id="4f89d-123">Wyszukaj *partnera firmy Microsoft* (*Microsoft Partner Center*) ( `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` ).</span><span class="sxs-lookup"><span data-stu-id="4f89d-123">Search for the *Microsoft Partner* (*Microsoft Partner Center*) API (`fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd`).</span></span>

    ![Zrzut ekranu przedstawiający ekran uprawnień interfejsu API żądania z wyszukiwaniem interfejsu API Centrum partnerskiego firmy Microsoft](../images/SearchPCApi.png)
    
9. <span data-ttu-id="4f89d-125">Wybierz pozycję **Microsoft Partner Center** i sprawdź **user_impersonation**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-125">Select **Microsoft Partner Center** and check **user_impersonation**.</span></span>

10. <span data-ttu-id="4f89d-126">Ustaw **delegowane uprawnienia** do **Centrum partnerskiego**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-126">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Zrzut ekranu przedstawiający ekran konfiguracja uprawnień delegowanych dla interfejsu API Centrum partnerskiego firmy Microsoft](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a><span data-ttu-id="4f89d-128">Dostęp tylko do aplikacji</span><span class="sxs-lookup"><span data-stu-id="4f89d-128">Application-only access</span></span>

<span data-ttu-id="4f89d-129">Ta metoda jest zalecana w przypadku konfiguracji **dostępu tylko do aplikacji** do interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="4f89d-129">This method is recommended for **application-only access** setup to the APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f89d-130">Należy podać identyfikator aplikacji, klucz aplikacji i identyfikator katalogu w aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f89d-130">You must provide the application ID, application key, and directory ID from your Azure AD application.</span></span>

1. <span data-ttu-id="4f89d-131">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f89d-131">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4f89d-132">Wybierz usługę **Azure Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="4f89d-132">Select the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="4f89d-133">Wybierz **rejestracje aplikacji**, a następnie wybierz pozycję **rejestracja nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-133">Choose **App registrations**, then select **New application registration**.</span></span>
4. <span data-ttu-id="4f89d-134">Utwórz nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="4f89d-134">Create your new application.</span></span> <span data-ttu-id="4f89d-135">W obszarze **Typ aplikacji** wybierz pozycję **aplikacja sieci Web/interfejs API**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-135">For **Application type**, choose **Web app/API**.</span></span> <span data-ttu-id="4f89d-136">Wprowadź **nazwę** i **adres URL** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4f89d-136">Enter a an application **name** and **URL**.</span></span> <span data-ttu-id="4f89d-137">Następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-137">Then choose **Create**.</span></span>
5. <span data-ttu-id="4f89d-138">Wybierz **uprawnienia interfejsu API** dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4f89d-138">Choose **API permissions** for the application.</span></span> <span data-ttu-id="4f89d-139">Wybierz pozycję **Dodaj uprawnienie**, a następnie wybierz interfejsy API, które są **wykorzystywane przez moją organizację**</span><span class="sxs-lookup"><span data-stu-id="4f89d-139">Choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="4f89d-140">Wyszukaj *partnera firmy Microsoft* (*Microsoft Dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).</span><span class="sxs-lookup"><span data-stu-id="4f89d-140">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Zrzut ekranu przedstawiający ekran uprawnień interfejsu API żądania z wyszukiwaniem interfejsu API partnera firmy Microsoft](../images/SearchGatewayApi.png)

7. <span data-ttu-id="4f89d-142">Ustaw **delegowane uprawnienia** do **Centrum partnerskiego**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-142">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Zrzut ekranu przedstawiający ekran konfiguracja uprawnień delegowanych dla interfejsu API partnera firmy Microsoft](../images/SelectUserPermission.png)

8. <span data-ttu-id="4f89d-144">W przypadku zarejestrowanej aplikacji wybierz pozycję **Właściwości** , a następnie wybierz pozycję **Kopiuj identyfikator aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-144">For the application you registered, choose **Properties** and then select **copy the Application ID**.</span></span>
9. <span data-ttu-id="4f89d-145">Wybierz pozycję **Ustawienia**, a następnie wybierz pozycję **Certyfikaty & wpisy tajne**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-145">Choose **Settings**, then choose **Certificates & Secrets**.</span></span> <span data-ttu-id="4f89d-146">Wybierz pozycję **nowy klucz tajny klienta** i ustaw wartość **wygaśnięcia**  na **nigdy nie wygasa**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-146">Choose **New Client Secret** and set the **Expiration**  to **Never expires**.</span></span> <span data-ttu-id="4f89d-147">Następnie wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-147">Then choose **Save**.</span></span>
10. <span data-ttu-id="4f89d-148">W menu **klucze** wybierz **Kopiuj wartość klucza**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-148">On the **Keys** menu, choose **Copy the key value**.</span></span> <span data-ttu-id="4f89d-149">Zapisz kopię tej wartości.</span><span class="sxs-lookup"><span data-stu-id="4f89d-149">Save a copy of this value.</span></span>

> [!WARNING]
> <span data-ttu-id="4f89d-150">Pamiętaj, aby zapisać kopię wartości klucza dla utworzonego klucza.</span><span class="sxs-lookup"><span data-stu-id="4f89d-150">Be sure to save a copy of the key value for the key you created.</span></span> <span data-ttu-id="4f89d-151">Ta wartość klucza będzie musiała zostać użyta później w celu uzyskania tokenu.</span><span class="sxs-lookup"><span data-stu-id="4f89d-151">You will need to use this key value later to obtain a token.</span></span>

## <a name="partner-consent"></a><span data-ttu-id="4f89d-152">Zgoda partnera</span><span class="sxs-lookup"><span data-stu-id="4f89d-152">Partner consent</span></span>

<span data-ttu-id="4f89d-153">W portalu zarządzania platformy Azure wybierz pozycję **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-153">In the Azure management portal, select **Enterprise applications**.</span></span> <span data-ttu-id="4f89d-154">Wyszukaj aplikację utworzoną w poprzedniej sekcji i wybierz tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="4f89d-154">Search for the application you created in the previous section, and select that application.</span></span> <span data-ttu-id="4f89d-155">Wybierz pozycję **uprawnienia** , a następnie wybierz pozycję **Udziel zgody administratora na konto partnera**.</span><span class="sxs-lookup"><span data-stu-id="4f89d-155">Select **Permissions** , then select **Grant Admin Consent for Partner Account**.</span></span>
