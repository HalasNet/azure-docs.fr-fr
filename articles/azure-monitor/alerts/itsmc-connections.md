---
title: Connecteur de gestion des services informatiques dans Azure Monitor
description: Cet article fournit des informations vous indiquant comment connecter vos produits/services ITSM à IT Service Management Connector (ITSMC) dans Azure Monitor pour surveiller et gérer les éléments de travail ITSM de manière centralisée.
ms.subservice: logs
ms.topic: conceptual
author: nolavime
ms.author: v-jysur
ms.date: 05/12/2020
ms.openlocfilehash: a372cdcd05267f3bdb093f676948a79c473ad955
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101734772"
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector"></a>Connecter des produits/services ITSM à IT Service Management Connector
Cet article fournit des informations vous indiquant comment configurer la connexion entre votre produit/service ITSM au connecteur de gestion des services informatiques (ITSMC) dans Log Analytics pour gérer de manière centralisée vos éléments de travail. Pour plus d’informations sur le connecteur ITSM, consultez [Présentation](./itsmc-overview.md).

Les produits/services ITSM suivants sont pris en charge. Sélectionnez le produit pour afficher des informations détaillées sur la connexion du produit à ITSMC.

- [ServiceNow](./itsmc-connections-servicenow.md)
- [System Center Service Manager](./itsmc-connections-scsm.md)
- [Cherwell](./itsmc-connections-cherwell.md)
- [Provance](./itsmc-connections-provance.md)

> [!NOTE]
> Nous proposons à nos clients Cherwell et Provance d’utiliser une [action webhook](./action-groups.md#webhook) pour point de terminaison Cherwell et Provance en guise d’autre solution pour l’intégration.

## <a name="next-steps"></a>Étapes suivantes

* [Résolution des problèmes dans le connecteur ITSM](./itsmc-resync-servicenow.md)