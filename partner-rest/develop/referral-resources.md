---
title: Zasoby dotyczące poleceń
description: Zasoby referencyjne reprezentują lidera sprzedaży od klienta, firmy Microsoft lub innego partnera.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 08438d208da57a4df40aeb609b14b6b6a6128d45
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770477"
---
# <a name="referral-resources"></a>Zasoby dotyczące poleceń

Dotyczy:

- Centrum partnerskie

Te zasoby reprezentują lidera sprzedaży od klienta, firmy Microsoft lub innego partnera.

## <a name="referral"></a>Zgłoszenia

Reprezentuje odwołanie.

| Właściwość              | Typ                                              | Opis                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | ciąg                                            | Identyfikator dla tego odwołania.                                                                                         |
| EngagementId          | ciąg                                            | EngagementID dla tego odwołania. Wiele odwołań może być skojarzonych z pojedynczym EngagementID                 |
| Nazwa                  | ciąg                                            | Nazwa odwołania.                 |
| ExternalReferenceId   | ciąg                                            | Zewnętrzny identyfikator odwołania. Przykład: Zachowaj własny identyfikator systemu Dynamics 365 potencjalnego klienta/szansy sprzedaży                    |
| CreatedDateTime       | ciąg w formacie daty i godziny czasu UTC                    | Data utworzenia odwołania.                                                                                |
| UpdatedDateTime       | ciąg w formacie daty i godziny czasu UTC                    | Data ostatniej aktualizacji odwołania.                                                                           |
| ExpirationDateTime    | ciąg w formacie daty i godziny czasu UTC                    | Data wygaśnięcia odwołania.                                                                                |
| Stan                | [ReferralStatus](referral-resources.md#referralstatus)      | [Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan odwołania. |
| Substatus          | [ReferralSubstatus](referral-resources.md#referralsubstatus)      | [Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan podrzędny odwołania. |
| StatusReason          | ciąg                                            | Opisowy komunikat o stanie. Przykład: Dlaczego odwołanie zostało utracone? |
| — Odwołanie          | [— Odwołanie](referral-resources.md#referraltype)          | Reprezentuje typ odwołania.                                                                                     |
| Kwalifikacja         | [ReferralQualification](referral-resources.md#referralqualification)| Reprezentuje jakość odwołania.                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#customerprofile)    | Informacje o kliencie.                                                                                     |
| Wyrażanie zgody               | [Wyrażanie zgody](referral-resources.md#consent)                    | Flagi zgody na udostępnianie informacji innym organizacjom i Zezwalanie na kontakt z użytkownikami.         |
| Szczegóły               | [ReferralDetails](referral-resources.md#referraldetails)    | Szczegóły klienta, notatki, wartość transakcji, Data zamknięcia waluty.                                                                |
| Zespół                  | [Członek](referral-resources.md#member)                      | Reprezentuje użytkowników należących do organizacji.                                |
| InviteContext         | [InviteContext](referral-resources.md#invitecontext)        | Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera.  |
| Element ETag                  | ciąg                                            | Elementy ETag są używane i wymagane do sprawdzania współbieżności podczas aktualizowania zasobów. |
| Cel         | [ReferralTarget](referral-resources.md#target)        | Reprezentuje dodatkowe informacje, które użytkownik może podać podczas zapraszania innej organizacji do zaangażowania partnera.  |

## <a name="referralstatus"></a>ReferralStatus

[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan odwołania.

| Wartość           | Opis                                                                                |
|-----------------|---------------------------------------------------------------------------------------------|
| Brak            |                                                                                             |
| Nowy             | Reprezentuje nowe odwołanie.                                                                 |
| Aktywna          | Reprezentuje aktywne odwołanie.                                                             |
| Zamknięty          | Reprezentuje zamknięte odwołanie.                                                              |

## <a name="referralsubstatus"></a>ReferralSubstatus

[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan odwołania.

| Wartość           | Opis                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| Brak            |                                                                                            |
| Oczekiwanie         | Reprezentuje nowe odwołanie, które jest w stanie oczekiwania.                                                 |
| Odebrano        | Reprezentuje nowe odwołanie, które zostało odebrane.                   |
| Zaakceptowano        | Reprezentuje aktywne odwołanie, które zostało zaakceptowane.                                                    |
| Uzyskany             | Reprezentuje zamknięte odwołanie, które zostało wygrane.                                            |
| Następuje            | Reprezentuje zamknięte odwołanie, które zostało utracone.                                           |
| Odrzucone        | Reprezentuje zamknięte odwołanie, które zostało odrzucone.                                       |
| Wygasłe         | Reprezentuje zamknięte odwołanie, które wygasło.                                             |

### <a name="status--substatus-transition-states"></a>Stan przejścia & stanu Substatus

| Stan                | Dozwolone przejście stanu     | Dozwolony stan Substatus                |
|-----------------------|-------------------------------|---------------------------------------|
| Nowy                   | Nowy, aktywny, zamknięty           | Oczekiwanie, odebrano                     |
| Aktywna                | Aktywne, zamknięte                | Zaakceptowano                              |
| Zamknięty                | Zamknięty                        | Wygrane, utracone, odrzucone, wygasłe          |

## <a name="referraltype"></a>— Odwołanie

[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami, które wskazują typ referencyjny.

| Właściwość              | Opis                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| Udostępniona                | Reprezentuje odwołanie, w którym wszystkie zainteresowane strony będą współpracować w celu zamknięcia.  |
| Ocen           | Reprezentuje odwołanie, w którym dwie strony będą współpracować ze sobą w celu zamknięcia.           |

## <a name="referralqualification"></a>ReferralQualification

[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi stan odwołania.

| Wartość                | Opis                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| Brak                 | Reprezentuje odwołanie, które nie ma skojarzonej miary jakości.                               |
| Direct               | Reprezentuje odwołanie, które zostało utworzone bezpośrednio przez klienta.                         |
| MarketingQualified   | Reprezentuje odwołanie, które zostało wygenerowane za pośrednictwem systemów automatyzacji marketingu firmy Microsoft.   |
| SalesQualified       | Reprezentuje odwołanie od agenta sprzedaży firmy Microsoft.                                         |

## <a name="customerprofile"></a>CustomerProfile

Zawiera informacje kontaktowe klienta.

| Właściwość | Typ                                                   | Opis                                            |
|----------|--------------------------------------------------------|--------------------------------------------------------|
| Nazwa     | ciąg                                                 | Nazwa organizacji klienta.                        |
| Adres  | [Adres](referral-resources.md#address)                         | Adres klienta.                           |
| Rozmiar     | ciąg                                                 | Liczba pracowników w organizacji klientów. |
| Zespół     | [Członek](referral-resources.md#member)                           | Kontakty dla organizacji klienta.            |
| Identyfikatory      | [CustomerProfileType](referral-resources.md#customerprofiletype) | [Tablica](https://docs.microsoft.com/dotnet/api/system.array) wartości wskazujących zewnętrzne identyfikatory dla klienta.                        |

## <a name="customerprofiletype"></a>CustomerProfileType

Zawiera identyfikatory zewnętrzne dla klienta.

| Właściwość | Typ   | Opis                                                                           |
|----------|--------|---------------------------------------------------------------------------------------|
| Duns     | ciąg | [Numer Bradstreety programu Dun &](https://www.dnb.com/duns-number.html) dla klienta. |
| Zewnętrzna | ciąg | Identyfikator klienta unikatowy dla Twojej organizacji.                                            |

## <a name="address"></a>Adres

Adres do użycia dla klienta.

| Właściwość     | Typ   | Opis                                                |
|--------------|--------|------------------------------------------------------------|
| AddressLine1 | ciąg | Pierwszy wiersz adresu.                             |
| AddressLine2 | ciąg | Drugi wiersz adresu. Ta właściwość jest opcjonalna. |
| City (Miasto)         | ciąg | Miasto.                                                  |
| Stan        | ciąg | Stan.                                                 |
| PostalCode   | ciąg | Kod pocztowy                                |
| Kraj      | ciąg | Kraj/region w [formacie kodu kraju ISO](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.threeletterisoregionname?view=netframework-4.7.2).             |
| Region (Region)       | ciąg | Region.                                                |

## <a name="member"></a>Członek

Opisuje informacje kontaktowe dla konkretnej osoby.

| Właściwość    | Typ   | Opis                  |
|-------------|--------|------------------------------|
| FirstName (Imię)   | ciąg | Imię kontaktu.    |
| LastName (Nazwisko)    | ciąg | Nazwisko osoby kontaktowej.     |
| PhoneNumber | ciąg | Numer telefonu kontaktu.  |
| E-mail       | ciąg | Adres e-mail osoby kontaktowej. |
| ContactPreference       | [ContactPreference](referral-resources.md#contactpreference) | Preferencja kontaktu na potrzeby otrzymywania powiadomień e-mail. |

## <a name="contactpreference"></a>ContactPreference

Opisuje preferencje osoby kontaktowej dotyczące otrzymywania powiadomień e-mail.

| Właściwość    | Typ   | Opis                  |
|-------------|--------|------------------------------|
| Regionalne   | ciąg | Ustawienia regionalne powiadomienia e-mail. Obsługiwane są [AllCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_AllCultures), [NeutralCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_NeutralCultures)i [SpecificCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_SpecificCultures)  |
| DisableNotifications    | bool | Spowoduje wyłączenie powiadomień e-mail dla użytkownika.     |

## <a name="consent"></a>Wyrażanie zgody

Flagi zgody na udostępnianie informacji innym organizacjom i Zezwalanie na kontakt z użytkownikami.

| Właściwość                                         | Typ      | Opis                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToToShareInfoWithOthers                   | boolean   | Wskazuje zgodę na udostępnianie danych osobowych innym osobom.             |
| ConsentToContact                                 | boolean   | Oznacza zgodę na kontakt z użytkownikami.  |

## <a name="invitecontext"></a>InviteContext

Dodatkowe informacje, które mogą być udostępniane w przypadku zapraszania do innej organizacji.

| Właściwość              | Typ                                                       | Opis                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Uwagi                 | ciąg                                                     | Dodatkowe uwagi dotyczące organizacji przejmującej.                |
| InvitedBy | [InvitedBy](referral-resources.md#invitedby)                                     | Identyfikator organizacji, który wysłał odwołanie.                                   |

## <a name="invitedby"></a>InvitedBy

Dodatkowe informacje, które mogą być udostępniane w przypadku zapraszania do innej organizacji.

| Właściwość              | Typ                                                       | Opis                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| OrganizationId        | ciąg                                                     | Identyfikator organizacji, który wysłał odwołanie.                |
| OrganizationName      | ciąg                                                     | Nazwa organizacji, która wysłała odwołanie.                                   |

## <a name="referraldetails"></a>ReferralDetails

Reprezentuje szczegóły odwołania.

| Właściwość              | Typ                                                       | Opis                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Uwagi                 | ciąg                                                     | Dodatkowe uwagi dotyczące organizacji przejmującej.                |
| DealValue             | decimal                                                    | Wartość odwołania.                                    |
| Waluta              | ciąg                                                    | [Symbol ISO 4217 waluty](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.isocurrencysymbol?view=netframework-4.7.2)                                   |
| ClosingDateTime       | ciąg w formacie daty i godziny czasu UTC                         | Data, przez którą klient ma zostać zamknięty.                           |
| Wymagania          | [ReferralRequirements](referral-resources.md#referralrequirements)   | Branża, produkty, typ usługi i rozwiązania, których dotyczy klient.|

## <a name="referralrequirements"></a>ReferralRequirements

Zawiera wymagania klienta.

| Właściwość        | Typ                                                         | Opis                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Branże      | [Tag](referral-resources.md#tag)                                       | Branża, do której interesuje Cię klient.        |
| Produkty        | [Tag](referral-resources.md#tag)                                       | Produkty, których dotyczy klient.          |
| Usługi        | [Tag](referral-resources.md#tag)                                       | Usługi, których dotyczy klient.          |
| Rozwiązania       | [SolutionTag](referral-resources.md#solutiontag)                       | Rozwiązania, których dotyczy klient.                             |

## <a name="solutiontag"></a>SolutionTag

Zawiera szczegółowe informacje o rozwiązaniu.

| Właściwość        | Typ                                         | Opis                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| Id              | ciąg                                       | Identyfikator rozwiązania.        |
| Nazwa            | ciąg                                       | Nazwa rozwiązania.          |
| Typrozwiązania    | [Typrozwiązania](referral-resources.md#solutiontype)     | Typ rozwiązania.          |

## <a name="solutiontype"></a>Typrozwiązania

[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi typ rozwiązania.

| Właściwość        | Opis                                                     |
|-----------------|-----------------------------------------------------------------|
| Brak            |                                                                  |
| Kategoria        |  Wykorzystuje wstępnie zdefiniowane nazwy rozwiązań.                            |
| Nazwa            |  Możliwość odwoływania się do rozwiązań z wykazu Microsoft. |

## <a name="target"></a>Cel

Opisuje cel referencyjny.

| Właściwość                  | Typ                                                  | Opis                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | ciąg                                                | Identyfikator celu odwołania. |
| Typ                      | [ReferralTargetType](referral-resources.md#targettype) | Typ docelowy odwołania |

## <a name="targettype"></a>Typ

[Wyliczenie](https://docs.microsoft.com/dotnet/api/system.enum) z wartościami wskazującymi typ rozwiązania.

| Właściwość        | Opis                                                     |
|-----------------|-----------------------------------------------------------------|
| Brak            |                                                                  |
| BusinessProfileLocation         |  Lokalizacja profilu w profilu biznesowym partnera.                            |
| SolutionProfile            |  Profil rozwiązania partnera. |

## <a name="tag"></a>Tag

Opisuje tag.

| Właściwość                  | Typ                                                  | Opis                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | ciąg                                                | Identyfikator dla tego tagu.                                          |

### <a name="products"></a>Produkty

| Wartość        |
|-----------------|
|Azure|
|EnterpriseMobilityAndSecurity|
|Exchange|
|DeveloperTools|
|Dynamics365Business|
|Dynamics365Enterprise|
|DynamicsAX, GP, nawigacja, SL|
|Microsoft365|
|Office|
|PowerBI|
|Project|
|SharePoint|
|SkypeForBusiness|
|Surface|
|SurfaceHub|
|SQL|
|Teams|
|Visio|
|Windows|
|Yammer|

### <a name="services"></a>Usługi

| Wartość        |
|-----------------|
|ConsultingAndProfessional|
|CustomSolution (ISV)|
|DeploymentOrMigration|
|Sprzęt|
|Integracja|
|IPServices (ISV)|
|LearningAndCertification|
|Licencjonowanie|
|ManagedServices|
|ProjectServices|

### <a name="industries"></a>Branże

| Wartość        |
|-----------------|
|Rolnictwo, leśnictwo, & rybołówstwo|
|Komunikacja & Media|
|Education|
|Usługi finansowe|
|Instytucje rządowe|
|Opieka zdrowotna|
|Hotelarstwo|
|Produkcja|
|Narzędzia & pakietu|
|Bezpieczeństwo publiczne i bezpieczeństwo narodowe|
|Towary konsumenckie detaliczne &|
|Usługi|
|Transport & podróże|
|Dystrybucja & hurtowych|

### <a name="solutions"></a>Rozwiązania

| Wartość        |
|-----------------|
|AdvancedAnalytics|
|ApplicationIntegration|
|ArtificialIntelligence|
|AzureSecurityOperationManagement|
    |AzureStack|
    |BackupDisasterRecovery|
    |BigData|
    |Łańcuch bloków|
    |Chatbot|
    |CloudDatabaseMigration|
    |CloudMigration|
    |CloudVoice|
    |CognitiveServices|
    |CompetitiveDatabaseMigration|
    |Kontenery|
    |DataWarehouse|
    |DatabaseonLinux|
    |DevelopmentandTest|
    |DevOps|
    |DigitalMedia|
    |Dynamics365forCustomerService|
    |Dynamics365forFieldService|
    |Dynamics365forFinanceOperations|
    |Dynamics365forRetail|
    |Dynamics365forSales|
    |Dynamics365forTalent|
    |DynamicsonAzure|
    |EnterpriseBusinessIntelligence|
    |Gry|
    |HighPerformanceComputing|
    |HybridStorage|
    |IdentityandAccessManagement|
    |InformationManagement|
    |InternetofThings|
    |MachineLearning|
    |Microserviceapplications|
    |MobileApplications|
    |MySQLPostgresMigrationtoAzure|
    |Sieć|
    |NoSQLMigration|
    |RedhatonAzure|
    |RegulatoryComplianceGDPR|
    |SAPonAzure|
    |ServerlessComputing|
    |SharepointonAzure|
    |SQLServerUpgrade|
    |ThreatProtection|
    |Tworzenie aplikacji dla deweloperów|

### <a name="customer-size"></a>Rozmiar klienta

| Wartość        |
|-----------------|
|    1to50employees|
|    51to500employees|
|    Morethan500employees|
|    1to9employees|
|    10to50employees|
|    51to250employees|
|    251to1000employees|
|    1001to5000employees|
|    5001to10000employees|
|    10001to20000employees|
|    Morethan20000employees|
