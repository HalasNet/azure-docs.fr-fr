---
title: Le REST Apache HBase ne répond pas aux requêtes dans Azure HDInsight
description: Résoudre le problème où l’API REST Apache HBase ne répond pas aux requêtes dans Azure HDInsight
ms.service: hdinsight
ms.topic: troubleshooting
ms.date: 08/01/2019
ms.openlocfilehash: b42a37d752f245eb66f3952b56ee4e36ae954874
ms.sourcegitcommit: 2f9f306fa5224595fa5f8ec6af498a0df4de08a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "98936957"
---
# <a name="scenario-apache-hbase-rest-not-responding-to-requests-in-azure-hdinsight"></a>Scénario : Le REST Apache HBase ne répond pas aux requêtes dans Azure HDInsight

Cet article décrit les éventuelles solutions à appliquer pour résoudre les problèmes rencontrés lors d’interactions avec des clusters Azure HDInsight.

## <a name="issue"></a>Problème

Le service REST Apache HBase ne répond pas aux requêtes dans Azure HDInsight.

## <a name="cause"></a>Cause

La cause possible ici peut être que le service REST Apache HBase présente des fuites de sockets, ce qui est particulièrement courant lorsque le service s’exécute depuis longtemps (par exemple, des mois). À partir du kit de développement logiciel (SDK) client, un message d’erreur semblable à celui-ci peut s’afficher :

```
System.Net.WebException : Unable to connect to the remote server --->
System.Net.Sockets.SocketException : A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond 10.0.0.19:8090
```

## <a name="resolution"></a>Résolution

Redémarrez le REST HBase à l’aide de la commande ci-dessous après par SSH sur l’hôte. Vous pouvez également utiliser des actions de script pour redémarrer ce service sur tous les nœuds Worker :

```bash
sudo service hdinsight-hbrest restart
```

Cette commande arrête HBase Region Server sur le même hôte. Vous pouvez soit démarrer manuellement HBase Region Server via Ambari, soit laisser la fonctionnalité de redémarrage automatique d’Ambari récupérer HBase Region Server automatiquement.

Si le problème persiste, vous pouvez installer le script d’atténuation suivant sous la forme d’une tâche CRON qui s’exécute toutes les 5 minutes sur chaque nœud Worker. Ce script d’atténuation effectue un test ping sur le service REST et le redémarre en cas de non-réponse du service REST.

```bash
#!/bin/bash
nc localhost 8090 < /dev/null
if [ $? -ne 0 ]
    then
    echo "RESTServer is not responding. Restarting"
    sudo /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh restart rest
fi
```

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [troubleshooting next steps](../../../includes/hdinsight-troubleshooting-next-steps.md)]