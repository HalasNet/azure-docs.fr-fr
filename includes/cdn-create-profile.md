---
title: Fichier include
description: Fichier include
services: cdn
author: SyntaxC4
ms.service: azure-cdn
ms.topic: include
ms.date: 04/30/2020
ms.author: cfowler
ms.custom: include file
ms.openlocfilehash: 9a003b5c42a6ef4c699a3768d15ae08f86d56e52
ms.sourcegitcommit: d4734bc680ea221ea80fdea67859d6d32241aefc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100367286"
---
## <a name="create-a-new-cdn-profile"></a>Créer un profil CDN

Un profil CDN est un conteneur pour les points de terminaison CDN, qui spécifie un niveau tarifaire.

1. Dans le portail Azure (en haut à gauche), sélectionnez **Créer une ressource**. Le volet **Nouveau** s’affiche.
   
1. Recherchez et sélectionnez **CDN**, puis **Créer** :
   
    ![Sélectionnez une ressource CDN](./media/cdn-create-profile/cdn-new-resource.png)

    Le volet du **profil CDN** s’affiche.

1. Saisissez les valeurs suivantes :
   
    | Paramètre  | Valeur |
    | -------- | ----- |
    | **Nom** | Entrez *cdn-profile-123* comme nom de profil. |
    | **Abonnement** | Sélectionnez un abonnement Azure dans la liste déroulante. |
    | **Groupe de ressources** | Sélectionnez **Créer nouveau** et entrez *CDNQuickstart-rg* pour le nom de votre groupe de ressources, ou sélectionnez **Utiliser existant** et choisissez *CDNQuickstart-rg* si vous disposez déjà du groupe. | 
    | **Emplacement du groupe de ressources** | Sélectionnez un emplacement près de vous dans la liste déroulante. |
    | **Niveau tarifaire** | Sélectionnez une option **Akamai standard** dans la liste déroulante. (Le temps de déploiement du niveau Akamai est d’environ une minute. Le niveau Microsoft prend environ 10 minutes et les niveaux Verizon environ 30 minutes.) |
    | **Créer un point de terminaison CDN maintenant** | Laissez non sélectionné. |  
   
    ![Nouveau profil CDN](./media/cdn-create-profile/cdn-new-profile.png)

1. Cliquez sur **Créer** pour créer le profil.

