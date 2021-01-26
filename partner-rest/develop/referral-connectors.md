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
# <a name="referral-connectors"></a>Łączniki odwołań

Łączników odwołań można używać do synchronizowania odwołań partnerów z klientami zarządzania relacjami z klientami (CRM). Łącznik odwołań można utworzyć za pomocą [Microsoft Flow](https://flow.microsoft.com) jako punkt końcowy HTTPS do odbierania odwołań partnerów. Następnie można napisać odwołanie otrzymane przez przepływ do systemu CRM jako potencjalnego klienta.

## <a name="prerequisites"></a>Wymagania wstępne

* Subskrypcja Microsoft Flow
  * Konto z dostępem administratorów do tej subskrypcji
* Azure Active Directory (Azure AD) identyfikator aplikacji, identyfikator użytkownika, hasło i identyfikator dzierżawy (używane do uzyskiwania dostępu do interfejsu API partnera). Instrukcje dotyczące instalacji znajdują się w temacie [uwierzytelnianie partnera](api-authentication.md).
* Subskrypcja [aplikacji funkcji platformy Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) .
* Subskrypcja [zdarzeń elementu webhook Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) w celu [utworzenia odwołania](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) i [odwołania do zaktualizowanych](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) zdarzeń.
* Subskrypcja [systemu Microsoft Dynamics 365](https://dynamics.microsoft.com)
  * Włączono moduł sprzedaży
  * Konto z dostępem administratorów do tej subskrypcji

## <a name="flow-overview"></a>Omówienie przepływu

Odwołania są importowane do programu CRM przy użyciu następującego przepływu:

1. Partner konfiguruje element webhook w celu otrzymywania powiadomień o odwołaniach.
2. Partner rejestruje element webhook w centrum partnerskim. Partner również subskrybuje zdarzenia elementu webhook w przypadku tworzenia lub aktualizowania odwołań.
3. Klient referencyjny tworzy lub aktualizuje odwołanie.
4. System webhook Centrum partnerskiego sprawdza rejestrację partnera i wysyła powiadomienie do elementu webhook.
5. Element webhook odbiera powiadomienie.
6. Dokument przepływu w usłudze Microsoft Flow używa tokenu do wywołania interfejsu API referencyjnego Centrum partnerskiego.
7. Punkt końcowy przepływu pobiera odwołanie.
8. Punkt końcowy przepływu tworzy lidera CRM.

![Wykres przepływu przedstawiający kroki opisane w tej sekcji w celu zaimportowania odwołań partnerów do programu CRM.](../images/referralwebhook.png)

## <a name="flow-document-process"></a>Proces dokumentu przepływu

Dokument przepływu dla łącznika odwołań synchronizuje odwołanie partnera z liderem programu CRM z usługi Dynamics 365.

1. Łącznik pobiera token, z którym ma zostać nawiązane połączenie `https://api.partner.microsoft.com/v1.0/engagements/referrals` .
2. Łącznik uzyskuje odwołanie, które wyzwoliło łącznik przy użyciu `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .
3. Łącznik nawiązuje połączenie z usługą Dynamics 365.
4. Łącznik tworzy nowego potencjalnego klienta lub aktualizuje istniejącego potencjalnego klienta z najnowszymi informacjami na temat odwołania.
5. Łącznik aktualizuje odwołania z najnowszymi aktualizacjami z poziomu lidera programu CRM.

![Wykres przepływu przedstawiający kroki opisane w tej sekcji dla procesu dokumentu przepływu.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a>Przykładowy łącznik odwołań

Poniższy *przykładowy łącznik odwołań* pokazuje, jak synchronizować odwołania Centrum partnerskiego z potencjalnymi klientami programu CRM w usłudze Dynamics 365.

> [!IMPORTANT]
> Możesz pisać do różnych CRMs, zastępując [Łączniki Flow](https://flow.microsoft.com/en-us/connectors/) w przykładowym kodzie.

### <a name="import-flow-synchronization-package"></a>Importuj pakiet synchronizacji przepływu

Pobierz i zaimportuj *przykładowy pakiet kodu* do Microsoft Flow i Połącz się z usługą Dynamics 365:

1. Pobierz [pakiet synchronizacji przepływu](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) z [repozytorium GitHub](https://github.com/microsoft/Partner-Center-Referrals).
2. Zaloguj się do [Microsoft Flow](https://flow.microsoft.com) przy użyciu odpowiednich poświadczeń.
3. Wybierz pozycję **Moje przepływy** w menu nawigacji. Następnie wybierz pozycję **Importuj**.
4. Na stronie **Importuj pakiet** wybierz pobrany pakiet synchronizacji przepływu. Następnie wybierz pozycję **Przekaż**.

    ![Ekran importowania pakietu dla plików pakietu](../images/importPackage.png)

5. Po zakończeniu przekazywania pakietu Znajdź pakiet, który został przekazany w **zawartości recenzowania** pakietu.

    ![Szczegóły ekranu importowania pakietu](../images/importPackageDetails.png)

6. Wybierz przycisk **akcji** (ikona ołówka) dla przekazanego pakietu. Spowoduje to otwarcie bloku **Importuj konfigurację** .
7. Wybierz typ **instalacji** .

    * Aby utworzyć nowy przepływ, wybierz pozycję **Utwórz jako nowy** i wprowadź nową **nazwę zasobu**.
    * Aby zaktualizować istniejący przepływ o tej samej nazwie, wybierz pozycję **Aktualizuj**.

    ![Utwórz lub zaktualizuj nowy ekran uaktualniający](../images/CreateNewConnection.png)

8. Na stronie **Importuj pakiet** Znajdź połączenie Dynamics 365 w sekcji **Przejrzyj zawartość pakietu** w obszarze **powiązane zasoby**.
9. Wybierz przycisk **akcji** (ikona ołówka) dla połączenia z usługą Dynamics 365. Spowoduje to otwarcie bloku **Konfiguracja** dla tego powiązanego zasobu.
10. Wybierz pozycję **Utwórz nowy** , aby utworzyć nowe połączenie usługi Dynamics 365 lub Wybierz istniejące połączenie.
11. Sprawdź, czy na stronie **Importowanie pakietu** jest teraz widoczny wybrany typ instalacji przepływu i połączenie z usługą Dynamics 365. Następnie wybierz pozycję **Importuj**.

    ![Ekran stanu pakietu importowania](../images/importStatus.png)

12. Sprawdź, czy zasób przepływu został utworzony lub zaktualizowany.

### <a name="configure-flow-parameters"></a>Konfigurowanie parametrów przepływu

Skonfiguruj parametry zasobu przepływu:

1. W [Microsoft Flow](https://flow.microsoft.com)wybierz pozycję **Moje przepływy** w menu nawigacji.
2. Wybierz utworzony lub zaktualizowany zasób przepływu w poprzedniej sekcji.
3. Na stronie Flow (przepływ) wybierz pozycję **Edytuj przepływ**.
4. Wybierz zmienną **identyfikatora AAD-Application (Client)** i wprowadź identyfikator aplikacji usługi Azure AD.
5. Wybierz zmienną **UserID** i wprowadź swój identyfikator użytkownika.
6. Wybierz zmienną **userPassword** i wprowadź hasło użytkownika.
7. Wybierz zmienną **identyfikatora AAD-Directory (dzierżawa)** . Wprowadź identyfikator dzierżawy aplikacji usługi Azure AD.
8. Wybierz pozycję **Zapisz** , aby zapisać przepływ.

    ![Ekran ustawień zmiennych przepływu](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a>Uwierzytelnianie wywołania zwrotnego

Uwierzytelnij zdarzenie wywołania zwrotnego z Centrum partnerskiego:

> [!TIP]
> Aby zapoznać się z przykładem, zobacz [kod aplikacji funkcji przykładowej](#sample-function-app-code) w poniższej sekcji.

1. [Utwórz aplikację funkcji platformy Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) , która [uwierzytelnia zdarzenie wywołania zwrotnego z Centrum partnerskiego](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).

    1. Sprawdź, czy istnieją wymagane nagłówki (**Authorization**, **x-MS-Certificate-URL** i **x-MS-Signature-Algorithm**).
    2. Pobierz certyfikat używany do podpisywania zawartości (**x-MS-Certificate-URL**).
    3. Sprawdź łańcuch certyfikatów.
    4. Sprawdź **organizację** certyfikatu.
    5. Zapoznaj się z zawartością przy użyciu kodowania UTF-8 w buforze.
    6. Utwórz dostawcę usług kryptograficznych RSA.
    7. [Sprawdź, czy sygnatura pasuje](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) do tego, co było podpisane przy użyciu określonego algorytmu wyznaczania wartości skrótu (na przykład SHA256).
    8. Jeśli weryfikacja zakończy się pomyślnie, zostanie zwrócony komunikat **OK** .

2. Zanotuj wygenerowany identyfikator URI wywołania zwrotnego dla punktu końcowego HTTP aplikacji funkcji. Ten identyfikator URI jest wyświetlany podczas tworzenia aplikacji funkcji. Możesz również znaleźć ten identyfikator URI na stronie zasobów platformy Azure w aplikacji funkcji.
3. W [Microsoft Flow](https://flow.microsoft.com)Edytuj przepływ "odwolanie partnera do programu Microsoft Dynamics CRM ołów" zaimportowany w sekcji *[Importuj pakiet synchronizacji przepływu](#import-flow-synchronization-package)*.

    1. Dodaj wartość identyfikatora URI aplikacji funkcji do kroku "Walidacja certyfikatu elementu webhook".
    2. Skopiuj i wklej identyfikator URI wywołania zwrotnego aplikacji funkcji do dokumentu przepływu.
    3. Zapisz dokument przepływu.

#### <a name="sample-function-app-code"></a>Przykładowy kod aplikacji funkcji

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

### <a name="register-flow-with-partner-center"></a>Rejestrowanie przepływu w centrum partnerskim

Zarejestruj zasób przepływu w centrum partnerskim, aby wyzwolić przepływ i odbierać zdarzenia elementu webhook:

1. W [Microsoft Flow](https://flow.microsoft.com)wybierz pozycję **Moje przepływy** w menu nawigacji.
2. Wybierz utworzony lub zaktualizowany przepływ.
3. Na stronie Flow (przepływ) wybierz pozycję **Edytuj przepływ**.
4. Skopiuj i Zapisz **adres URL post protokołu HTTP** dla przepływu. Musisz użyć tego adresu URL, aby wyzwolić przepływ.
5. [Zarejestruj się, aby otrzymywać zdarzenia elementu webhook](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) podczas tworzenia lub aktualizowania odwołań. Użyj następującego formatu treści:

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
