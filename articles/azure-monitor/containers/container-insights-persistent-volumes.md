---
title: Configurer la supervision de volumes persistants avec Azure Monitor pour conteneurs | Microsoft Docs
description: Cet article explique comment configurer la supervision de clusters Kubernetes constitués de volumes persistants à l’aide d’Azure Monitor pour conteneurs.
ms.topic: conceptual
ms.date: 10/20/2020
ms.openlocfilehash: d7da6bc88e7c8526e3940714502d3c92d2f37dd8
ms.sourcegitcommit: e559daa1f7115d703bfa1b87da1cf267bf6ae9e8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "100600393"
---
# <a name="configure-pv-monitoring-with-azure-monitor-for-containers"></a>Configurer la supervision de volumes persistants avec Azure Monitor pour conteneurs

À partir de la version de l’agent *ciprod10052020*, l’agent intégré Azure Monitor pour conteneurs prend désormais en charge l’analyse des volumes persistants.

## <a name="pv-metrics"></a>Métriques de volume persistant

Azure Monitor pour conteneurs lance automatiquement la supervision des volumes persistants en collectant les métriques suivantes toutes les 60 secondes et en les stockant dans la table **InsightMetrics**.

|Nom de métrique |Dimension de la métrique (balises) |Description |
|------------|------------------------|------------|
| `pvUsedBytes`|`container.azm.ms/pv`|Espace utilisé en octets pour un volume persistant spécifique avec une revendication utilisée par un pod spécifique. `pvCapacityBytes` est plié en tant que dimension dans le champ Balises pour réduire le coût d’ingestion des données et simplifier les requêtes.|

## <a name="monitor-persistent-volumes"></a>Superviser les volumes persistants

Azure Monitor pour conteneurs inclut des graphiques préconfigurés pour cette métrique sous la forme d’un classeur pour chaque cluster. Vous pouvez trouver les graphiques dans l’onglet Volume persistant du classeur **Détails de la charge de travail** directement à partir d’un cluster AKS en sélectionnant Classeurs dans le volet gauche, puis dans la liste déroulante **Voir les classeurs** dans Insight. Vous pouvez également activer une alerte recommandée pour l’utilisation de volumes persistants, ainsi que pour interroger ces métriques dans Log Analytics.  

![Exemple de classeur pour les charges de travail de volume persistant Azure Monitor](./media/container-insights-persistent-volumes/pv-workload-example.PNG)

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur les métriques de volume persistant collectées [ici](./container-insights-agent-config.md).
