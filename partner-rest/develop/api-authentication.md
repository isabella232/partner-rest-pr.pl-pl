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
# <a name="partner-api-authentication"></a>Uwierzytelnianie interfejsu API Partner

Dotyczy:

- Interfejs API partnera

Interfejs API partnera wykorzystuje Azure Active Directory (Azure AD) do uwierzytelniania. W przypadku korzystania z interfejsu API partnera należy prawidłowo skonfigurować aplikację usługi Azure AD i uzyskać token dostępu. Możesz uzyskać tokeny dostępu dla dostępu do [aplikacji i użytkowników](#application-and-user-access) lub [dostępu tylko do aplikacji](#application-only-access).

## <a name="application-and-user-access"></a>Dostęp do aplikacji i użytkowników

Ta metoda jest zalecana do konfigurowania **dostępu aplikacji i użytkowników** do interfejsu API.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).
2. Wybierz usługę **Azure Active Directory** .
3. Wybierz **rejestracje aplikacji**, a następnie wybierz pozycję **rejestracja nowej aplikacji**.
4. Utwórz nową aplikację. W obszarze **Typ aplikacji** wybierz opcję **natywny**. Podaj nazwę i adres URL, a następnie wybierz pozycję **Utwórz**.
5. Wybierz **uprawnienia interfejsu API** dla aplikacji. Na ekranie **Żądaj uprawnień interfejsu API** wybierz opcję **Dodaj uprawnienia**, a następnie wybierz **interfejsy API, których używa Moja organizacja**
6. Wyszukaj *partnera firmy Microsoft* (*Microsoft Dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).

    ![Zrzut ekranu przedstawiający ekran uprawnień interfejsu API żądania z wyszukiwaniem interfejsu API partnera firmy Microsoft](../images/SearchGatewayApi.png)

7. Ustaw **delegowane uprawnienia** do **Centrum partnerskiego**.

    ![Zrzut ekranu przedstawiający ekran konfiguracja uprawnień delegowanych dla interfejsu API partnera firmy Microsoft](../images/SelectUserPermission.png)
    
8. Wyszukaj *partnera firmy Microsoft* (*Microsoft Partner Center*) ( `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` ).

    ![Zrzut ekranu przedstawiający ekran uprawnień interfejsu API żądania z wyszukiwaniem interfejsu API Centrum partnerskiego firmy Microsoft](../images/SearchPCApi.png)
    
9. Wybierz pozycję **Microsoft Partner Center** i sprawdź **user_impersonation**.

10. Ustaw **delegowane uprawnienia** do **Centrum partnerskiego**.

    ![Zrzut ekranu przedstawiający ekran konfiguracja uprawnień delegowanych dla interfejsu API Centrum partnerskiego firmy Microsoft](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a>Dostęp tylko do aplikacji

Ta metoda jest zalecana w przypadku konfiguracji **dostępu tylko do aplikacji** do interfejsów API.

> [!IMPORTANT]
> Należy podać identyfikator aplikacji, klucz aplikacji i identyfikator katalogu w aplikacji usługi Azure AD.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).
2. Wybierz usługę **Azure Active Directory** .
3. Wybierz **rejestracje aplikacji**, a następnie wybierz pozycję **rejestracja nowej aplikacji**.
4. Utwórz nową aplikację. W obszarze **Typ aplikacji** wybierz pozycję **aplikacja sieci Web/interfejs API**. Wprowadź **nazwę** i **adres URL** aplikacji. Następnie wybierz pozycję **Utwórz**.
5. Wybierz **uprawnienia interfejsu API** dla aplikacji. Wybierz pozycję **Dodaj uprawnienie**, a następnie wybierz interfejsy API, które są **wykorzystywane przez moją organizację**
6. Wyszukaj *partnera firmy Microsoft* (*Microsoft Dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).

    ![Zrzut ekranu przedstawiający ekran uprawnień interfejsu API żądania z wyszukiwaniem interfejsu API partnera firmy Microsoft](../images/SearchGatewayApi.png)

7. Ustaw **delegowane uprawnienia** do **Centrum partnerskiego**.

    ![Zrzut ekranu przedstawiający ekran konfiguracja uprawnień delegowanych dla interfejsu API partnera firmy Microsoft](../images/SelectUserPermission.png)

8. W przypadku zarejestrowanej aplikacji wybierz pozycję **Właściwości** , a następnie wybierz pozycję **Kopiuj identyfikator aplikacji**.
9. Wybierz pozycję **Ustawienia**, a następnie wybierz pozycję **Certyfikaty & wpisy tajne**. Wybierz pozycję **nowy klucz tajny klienta** i ustaw wartość **wygaśnięcia**  na **nigdy nie wygasa**. Następnie wybierz pozycję **Zapisz**.
10. W menu **klucze** wybierz **Kopiuj wartość klucza**. Zapisz kopię tej wartości.

> [!WARNING]
> Pamiętaj, aby zapisać kopię wartości klucza dla utworzonego klucza. Ta wartość klucza będzie musiała zostać użyta później w celu uzyskania tokenu.

## <a name="partner-consent"></a>Zgoda partnera

W portalu zarządzania platformy Azure wybierz pozycję **aplikacje dla przedsiębiorstw**. Wyszukaj aplikację utworzoną w poprzedniej sekcji i wybierz tę aplikację. Wybierz pozycję **uprawnienia** , a następnie wybierz pozycję **Udziel zgody administratora na konto partnera**.
