---
title: Types de numéros de téléphone dans Azure Communication Services
titleSuffix: An Azure Communication Services concept document
description: Découvrez comment utiliser efficacement les différents types de numéros de téléphone pour les SMS et la téléphonie.
author: prakulka
manager: nmurav
services: azure-communication-services
ms.author: prakulka
ms.date: 10/05/2020
ms.topic: overview
ms.custom: references_regions
ms.service: azure-communication-services
ms.openlocfilehash: b7d780ce6362e34c801b4da25332bff90f0b7515
ms.sourcegitcommit: b4647f06c0953435af3cb24baaf6d15a5a761a9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2021
ms.locfileid: "101659271"
---
# <a name="phone-number-types-in-azure-communication-services"></a>Types de numéros de téléphone dans Azure Communication Services

[!INCLUDE [Regional Availability Notice](../../includes/regional-availability-include.md)]

Azure Communication Services vous permet d’utiliser des numéros de téléphone pour effectuer des appels vocaux et envoyer des SMS avec le réseau téléphonique commuté public (RTPC). Dans ce document, nous allons examiner les types de numéro de téléphone, les options de configuration et la disponibilité dans les régions pour la planification de votre solution de téléphonie et de SMS à l’aide de Communication Services.

## <a name="number-types-and-features"></a>Types et caractéristiques des numéros
Communication Services propose deux types de numéros de téléphone : **local** et **gratuit**.

### <a name="local-numbers"></a>Numéros locaux
Les numéros locaux (géographiques) sont des numéros de téléphone à 10 chiffres comportant un indicatif régional aux États-Unis. Par exemple, `+1 (206) XXX-XXXX` est un numéro local dont l’indicatif régional est `206`. Cet indicatif régional est attribué à la ville de Seattle. Ces numéros de téléphone sont généralement utilisés par les particuliers et les entreprises locales. Azure Communication Services propose des numéros locaux aux États-Unis. Ces numéros peuvent être utilisés pour passer des appels téléphoniques, mais pas pour envoyer des SMS.

### <a name="toll-free-numbers"></a>Numéros gratuits
Les numéros gratuits sont des numéros de téléphone à 10 chiffres comportant un indicatif régional spécifique qui peuvent être composés gratuitement à partir de n’importe quel numéro de téléphone. Par exemple, `+1 (800) XXX-XXXX` est un numéro gratuit dans la région Amérique du Nord. Ces numéros de téléphone sont généralement utilisés pour contacter un service client. Azure Communication Services propose des numéros gratuits aux États-Unis. Ces numéros peuvent être utilisés pour passer des appels téléphoniques et envoyer des SMS. Les numéros gratuits ne peuvent pas être utilisés par des personnes et ne peuvent être attribués qu’à des applications.

#### <a name="choosing-a-phone-number-type"></a>Choix d’un type de numéro de téléphone

Si le numéro de téléphone est destiné à être utilisé par une application (par exemple, pour effectuer des appels ou envoyer des messages pour le compte de votre service), vous pouvez sélectionner un numéro gratuit ou local (géographique). Vous pouvez sélectionner un numéro gratuit si votre application envoie des SMS et/ou effectue des appels.

Dans le cas d’une utilisation par une personne (par exemple, un utilisateur de votre application appelante), c’est le numéro de téléphone local (géographique) qui doit être utilisé.

Le tableau ci-dessous résume ces types de numéros de téléphone :

| Type de numéro de téléphone | Exemple                              | Disponibilité dans le pays    | Fonctionnalités du numéro de téléphone |Cas d’utilisation courant                                                                                                     |
| ----------------- | ------------------------------------ | ----------------------- | ------------------------|------------------------------------------------------------------------------------------------------------------- |
| Local (géographique)        | +1 (indicatif régional) XXX XX XX XX  | US                      | Appel (sortant) | Attribution des numéros de téléphone aux utilisateurs de vos applications  |
| Gratuit         | \+ 1 (*indicatif* de zone d’appel gratuit) XXX XX XX | US                      | Appel (sortant), SMS (entrant/sortant)| Attribution des numéros de téléphone à des systèmes/bots de réponse vocale interactive (IVR), applications SMS                                        |


### <a name="phone-number-features-in-azure-communication-services"></a>Fonctionnalités de numéros de téléphone dans Azure Communication Services

[!INCLUDE [Emergency Calling Notice](../../includes/emergency-calling-notice-include.md)]

Pour la plupart des numéros de téléphone, nous vous autorisons à configurer un ensemble de fonctionnalités « à la carte ». Ces fonctionnalités peuvent être sélectionnées quand vous louez vos numéros de téléphone dans Azure Communication Services.

Les fonctionnalités disponibles dépendent du pays dans lequel vous travaillez, de votre cas d’usage et du type de numéro de téléphone que vous avez sélectionné. Ces fonctionnalités varient selon le pays en raison des exigences réglementaires. Azure Communication Services offre les fonctionnalités de numéro de téléphone suivantes :

- **SMS sortants unidirectionnels** Cette option vous permet d’envoyer des SMS à vos utilisateurs. Elle peut être utile dans les scénarios de notification et d’authentification à 2 facteurs.
- **SMS entrants et sortants bidirectionnels** Cette option vous permet d’envoyer et de recevoir des messages de vos utilisateurs en utilisant les numéros de téléphone. Elle peut être utile dans les scénarios de service client.
- **Appels téléphoniques sortants unidirectionnels** Cette option vous permet d’effectuer des appels en direction de vos utilisateurs et de configurer l’ID de l’appelant pour les appels sortants passés par votre service. Elle peut être utile dans les scénarios de notifications vocales et de service client.

## <a name="countryregion-availability"></a>Disponibilité par pays/région

Le tableau suivant vous montre où vous pouvez acquérir les différents types de numéros de téléphone ainsi que les fonctionnalités d’appels entrants et sortants et de SMS correspondantes.

|Type de numéro| Zones d’acquisition des numéros | Zones destinatrices des appels                                        | Zones émettrices des appels                                    |Zones destinatrices des SMS       | Zones émettrices des SMS |
|-----------| ------------------ | ---------------------------------------------------  |-------------------------------------------------------|-----------------------|--------|
| Local (géographique)  | US                 | États-Unis, Canada, Royaume-Uni, Allemagne, France ainsi que d’autres*| États-Unis, Canada, Royaume-Uni, Allemagne, France ainsi que d’autres* |Non disponible| Non disponible |
| Gratuit | US                 | US                                                   | US                                                    |US                | US |

\* Pour plus d’informations sur les destinations des appels et les tarifs, reportez-vous à la [page des prix](../pricing.md).

## <a name="azure-subscriptions-eligibility"></a>Éligibilité des abonnements Azure

Pour obtenir un numéro de téléphone, vous devez détenir un abonnement Azure payant. Les numéros de téléphone ne peuvent pas être acquis sur des comptes d’essai ou avec des crédits gratuits Azure.

La disponibilité des numéros de téléphone est limitée aux abonnements Azure dont l’adresse de facturation se trouve aux États-Unis.

## <a name="next-steps"></a>Étapes suivantes

### <a name="quickstarts"></a>Démarrages rapides

- [Obtenir un numéro de téléphone](../../quickstarts/telephony-sms/get-phone-number.md)
- [Passer un appel](../../quickstarts/voice-video-calling/calling-client-samples.md)
- [Envoyer un SMS](../../quickstarts/telephony-sms/send.md)

### <a name="conceptual-documentation"></a>Documentation conceptuelle

- [Concepts vocaux et vidéo](../voice-video-calling/about-call-types.md)
- [Concepts de la téléphonie](./telephony-concept.md)
- [Flux d’appels](../call-flows.md)
- [Tarification](../pricing.md)
