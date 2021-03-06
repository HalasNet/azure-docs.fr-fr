---
title: Conflit de port lors du démarrage des services dans Azure HDInsight
description: Étapes de dépannage et résolutions possibles pour les problèmes de conflit de port rencontrés lors d’interactions avec des clusters Azure HDInsight.
ms.service: hdinsight
ms.topic: troubleshooting
ms.date: 01/23/2020
ms.openlocfilehash: f42e84d5d9c1dd49d9bf5604fe2f967eae0b6276
ms.sourcegitcommit: 2f9f306fa5224595fa5f8ec6af498a0df4de08a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "98943100"
---
# <a name="scenario-port-conflict-when-starting-services-in-azure-hdinsight"></a>Scénario : Conflit de port lors du démarrage des services dans Azure HDInsight

Cet article décrit les éventuelles solutions à appliquer pour résoudre les problèmes rencontrés lors d’interactions avec des clusters Azure HDInsight.

## <a name="issue"></a>Problème

Échec du démarrage d’un service.

## <a name="cause"></a>Cause

Il existe un conflit de port.

## <a name="resolution"></a>Résolution

### <a name="method-1"></a>Méthode 1

Utilisez les commandes ci-dessous pour obtenir ou tuer tous les processus en cours d’exécution, lesquels sont perturbés par le problème de port.

```bash
netstat -lntp | grep <port>
ps -ef | grep <service>
kill -9 <service>
```

Démarrez ensuite le service.

### <a name="method-2"></a>Méthode 2

Redémarrez le nœud.

## <a name="next-steps"></a>Étapes suivantes

Si votre problème ne figure pas dans cet article ou si vous ne parvenez pas à le résoudre, utilisez un des canaux suivants pour obtenir de l’aide :

* Obtenez des réponses de la part d’experts Azure en faisant appel au [Support de la communauté Azure](https://azure.microsoft.com/support/community/).

* Connectez-vous à [@AzureSupport](https://twitter.com/azuresupport), le compte Microsoft Azure officiel pour améliorer l’expérience client. Connexion de la communauté Azure aux ressources appropriées : réponses, support technique et experts.

* Si vous avez besoin d’une aide supplémentaire, vous pouvez envoyer une requête de support à partir du [Portail Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/). Sélectionnez **Support** dans la barre de menus, ou ouvrez le hub **Aide + Support**. Pour plus d’informations, consultez [Création d’une demande de support Azure](../../azure-portal/supportability/how-to-create-azure-support-request.md). L’accès au support relatif à la gestion et à la facturation des abonnements est inclus avec votre abonnement Microsoft Azure. En outre, le support technique est fourni avec l’un des [plans de support Azure](https://azure.microsoft.com/support/plans/).