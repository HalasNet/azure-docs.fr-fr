---
title: Erreur de refus d’autorisation avec une table Apache Hive dans Azure HDInsight
description: Erreur de refus d’autorisation lors de la tentative de création d’une table Apache Hive dans Azure HDInsight
ms.service: hdinsight
ms.topic: troubleshooting
ms.date: 08/09/2019
ms.openlocfilehash: 6d91ca747bb264b4c7262eec2bb0745b8a40b7a0
ms.sourcegitcommit: 2f9f306fa5224595fa5f8ec6af498a0df4de08a8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "98930913"
---
# <a name="scenario-permission-denied-error-when-trying-to-create-an-apache-hive-table-in-azure-hdinsight"></a>Scénario : Erreur de refus d’autorisation lors de la tentative de création d’une table Apache Hive dans Azure HDInsight

Cet article décrit la procédure à suivre pour résoudre les problèmes rencontrés lors de l’utilisation de composants Interactive Query dans des clusters Azure HDInsight.

## <a name="issue"></a>Problème

L’erreur suivante s’affiche lors de la tentative de création d’une table :

```
java.sql.SQLException: Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hdiuser] does not have [ALL] privilege on [wasbs://data@xxxxx.blob.core.windows.net/path/table]
```

Vous verrez un message d’erreur similaire si vous exécutez la commande de stockage HDFS suivante :

```
hdfs dfs -mkdir wasbs://data@xxxxx.blob.core.windows.net/path/table
```

## <a name="cause"></a>Cause

La possibilité de créer une table dans Apache Hive est déterminée par les autorisations appliquées au compte de stockage du cluster. Si les autorisations du compte de stockage de cluster sont incorrectes, vous ne pourrez pas créer de tables. Cela signifie que vous pouvez avoir les stratégies Ranger appropriées pour la création de table et voir néanmoins des erreurs « Autorisation refusée ».

## <a name="resolution"></a>Résolution

Cela est dû à un manque d’autorisations suffisantes sur le conteneur de stockage utilisé. L’utilisateur qui crée la table Hive a besoin d’autorisations de lecture, d’écriture et d’exécution sur le conteneur. Pour plus d’informations, consultez [Best Practices for Hive Authorization Using Apache Ranger in HDP 2.2](https://hortonworks.com/blog/best-practices-for-hive-authorization-using-apache-ranger-in-hdp-2-2/).

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [troubleshooting next steps](../../../includes/hdinsight-troubleshooting-next-steps.md)]