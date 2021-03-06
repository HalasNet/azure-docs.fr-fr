---
title: Résoudre les erreurs courantes liées à l’intégration d’Azure Automanage
description: Erreurs courantes d’intégration à Automanage et résolution
author: asinn826
ms.service: virtual-machines
ms.subservice: automanage
ms.workload: infrastructure
ms.topic: conceptual
ms.date: 01/14/2021
ms.author: alsin
ms.openlocfilehash: df5133ad4bb3155afdc9d43e595591d9cfda4ea0
ms.sourcegitcommit: b4647f06c0953435af3cb24baaf6d15a5a761a9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2021
ms.locfileid: "101644440"
---
# <a name="troubleshoot-common-automanage-onboarding-errors"></a>Résoudre les erreurs courantes liées à l’intégration d’Automanage
Automanage peut échouer à intégrer un ordinateur sur le service. Ce document explique comment résoudre les échecs de déploiement, partage quelques raisons courantes pour lesquelles les déploiements peuvent échouer et décrit les étapes suivantes possibles d’atténuation.

## <a name="troubleshooting-deployment-failures"></a>Résoudre les problèmes de déploiement
L’intégration d’une machine à Automanage entraînera la création d’un déploiement d’Azure Resource Manager. En cas d’échec de l’intégration, il peut être utile d’examiner le déploiement pour plus d’informations sur la raison de l’échec. Vous trouverez des liens vers les déploiements dans le menu volant détaillant les échecs, illustré ci-dessous.

:::image type="content" source="media\automanage-common-errors\failure-flyout.png" alt-text="Menu volant détaillant les échecs d’Automanage.":::

### <a name="check-the-deployments-for-the-resource-group-containing-the-failed-vm"></a>Vérifier les déploiements pour le groupe de ressources contenant la machine virtuelle ayant échoué
Le menu volant des échecs contient un lien vers les déploiements au sein du groupe de ressources qui contient la machine dont l’intégration a échoué et un nom de préfixe que vous pouvez utiliser pour filtrer les déploiements. Cliquez sur le lien pour accéder au panneau des déploiements, où vous pouvez ensuite filtrer les déploiements pour voir les déploiements Automanage sur votre ordinateur. Si vous effectuez un déploiement dans plusieurs régions, veillez à cliquer sur le déploiement dans la bonne région.

### <a name="check-the-deployments-for-the-subscription-containing-the-failed-vm"></a>Vérifier les déploiements pour l’abonnement contenant la machine virtuelle ayant échoué
Si vous ne constatez aucun échec dans le déploiement du groupe de ressources, l’étape suivante consiste à examiner les déploiements de votre abonnement contenant la machine virtuelle dont l’intégration a échoué. Cliquez sur le lien **Déploiements pour l’abonnement** dans le menu volant des échecs et filtrez les déploiements à l’aide du filtre **Automanage-DefaultResourceGroup**. Utilisez le nom du groupe de ressources du panneau des échecs pour filtrer les déploiements. Le nom du déploiement sera suivi d’un nom de région. Si vous effectuez un déploiement dans plusieurs régions, veillez à cliquer sur le déploiement dans la bonne région.

### <a name="check-deployments-in-a-subscription-linked-to-a-log-analytics-workspace"></a>Vérifier les déploiements dans un abonnement lié à un espace de travail Log Analytics
Si vous ne voyez aucun échec de déploiement dans le groupe de ressources ou l’abonnement contenant votre machine virtuelle ayant échoué, et si votre machine virtuelle ayant échoué est connectée à un espace de travail Log Analytics dans un autre abonnement, accédez à l’abonnement lié à votre espace de travail Log Analytics et vérifiez les échecs de déploiement.

## <a name="common-deployment-errors"></a>Erreurs de déploiement courantes

Error |  Limitation des risques
:-----|:-------------|
Erreur d’autorisations insuffisantes pour le compte Automanage | Cela peut se produire si vous avez récemment déplacé un abonnement contenant un nouveau compte Automanage dans un nouveau locataire. Les étapes de résolution sont accessibles [ici](./repair-automanage-account.md).
La région de l’espace de travail ne correspond pas aux spécifications du mappage des régions | Automanage n’a pas pu intégrer votre machine, mais l’espace de travail Log Analytics auquel la machine est actuellement liée n’est pas mappé à une région Automation prise en charge. Assurez-vous que votre compte Automation et votre espace de travail Log Analytics existants se trouvent dans un [mappage de régions pris en charge](../automation/how-to/region-mappings.md).
« L’attribution a échoué ; aucune information supplémentaire n’est disponible. » | Ouvrez un cas auprès du support Microsoft Azure.

## <a name="next-steps"></a>Étapes suivantes

* [En savoir plus sur Azure Automanage](./automanage-virtual-machines.md)

> [!div class="nextstepaction"]
> [Activer le service Automanage pour machines virtuelles dans le portail Azure](quick-create-virtual-machines-portal.md)