---
title: Connecteur de gestion des services informatiques – Exportation sécurisée dans Azure Monitor – Configuration à l’aide de ServiceNow
description: Cet article vous montre comment connecter vos produits/services ITSM à l’aide de ServiceNow sur Exportation sécurisée dans Azure Monitor.
ms.subservice: logs
ms.topic: conceptual
author: nolavime
ms.author: v-jysur
ms.date: 12/31/2020
ms.openlocfilehash: 02b167219a4f1604d340d72f9dc47e67919c2542
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101714134"
---
# <a name="connect-servicenow-to-azure-monitor"></a>Connecter ServiceNow à Azure Monitor

Les sections suivantes fournissent des détails sur la connexion de votre produit ServiceNow et l’exportation sécurisée dans Azure.

## <a name="prerequisites"></a>Prérequis

Assurez-vous d’avoir respecté les prérequis suivants :

* Azure AD est inscrit.
* Vous avez la version prise en charge de la Gestion des événements ServiceNow – ITOM (version New York ou ultérieure).
* L’[application](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ac4c9c57dbb1d090561b186c1396191a/1.3.1?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%26q%3DEvent%2520Management%2520Connectors&sl=sh) est installée sur l’instance ServiceNow.

## <a name="configure-the-servicenow-connection"></a>Configurer la connexion ServiceNow

1. Utilisez le lien https://(nom de l’instance).service-now.com/api/sn_em_connector/em/inbound_event?source=azuremonitor afin d’obtenir l’URI pour la définition d’exportation sécurisée.

2. Suivez les instructions correspondant à la version :
   * [Paris](https://docs.servicenow.com/bundle/paris-it-operations-management/page/product/event-management/task/azure-events-authentication.html)
   * [Orlando](https://docs.servicenow.com/bundle/orlando-it-operations-management/page/product/event-management/task/azure-events-authentication.html)
   * [New York](https://docs.servicenow.com/bundle/newyork-it-operations-management/page/product/event-management/task/azure-events-authentication.html)
