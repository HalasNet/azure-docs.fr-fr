---
title: Utilisation de l’éditeur Azure Cloud Shell | Microsoft Docs
description: Vue d’ensemble de l’utilisation de l’éditeur Azure Cloud Shell.
services: azure
documentationcenter: ''
author: maertendMSFT
manager: timlt
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/24/2018
ms.author: damaerte
ms.openlocfilehash: 1e3ea9222b0f231250bde43fb86c07847ca4835e
ms.sourcegitcommit: d1b0cf715a34dd9d89d3b72bb71815d5202d5b3a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99832333"
---
# <a name="using-the-azure-cloud-shell-editor"></a>Utilisation de l’éditeur Azure Cloud Shell

Azure Cloud Shell inclut un éditeur de fichier intégré, créé à partir de l’[éditeur Monaco](https://github.com/Microsoft/monaco-editor) open source. L’éditeur Cloud Shell prend en charge des fonctionnalités telles que la mise en surbrillance du langage, la palette de commandes et un explorateur de fichiers.

![Éditeur Cloud Shell](media/using-cloud-shell-editor/open-editor.png)

## <a name="opening-the-editor"></a>Ouverture de l’éditeur

Pour la simple création et modification de fichiers, lancez l’éditeur en exécutant `code .` dans le terminal Cloud Shell. Cette action ouvre l’éditeur avec votre répertoire de travail actif, défini dans le terminal.

Pour ouvrir directement un fichier et le modifier rapidement, exécutez `code <filename>` qui ouvre l’éditeur sans l’explorateur de fichiers.

Pour ouvrir l’éditeur via le bouton de l’interface utilisateur, cliquez sur l’icône de l’éditeur `{}` dans la barre d’outils. L’éditeur et l’explorateur de fichiers par défaut s’ouvrent alors dans le répertoire `/home/<user>`.

## <a name="closing-the-editor"></a>Fermeture de l’éditeur

Pour fermer l’éditeur, ouvrez le panneau d’actions `...` en haut à droite de l’éditeur et sélectionnez `Close editor`.

![Fermer l’éditeur](media/using-cloud-shell-editor/close-editor.png)

## <a name="command-palette"></a>Palette de commandes

Pour lancer la palette de commandes, utilisez la touche `F1` lorsque le focus est défini sur l’éditeur. L’ouverture de la palette de commandes peut également être effectuée par le biais du panneau d’actions.

![Palette cmd](media/using-cloud-shell-editor/cmd-palette.png)

## <a name="contributing-to-the-monaco-editor"></a>Contribution à l’éditeur Monaco

La prise en charge de la surbrillance du langage dans l’éditeur Cloud Shell est assurée par le biais de fonctionnalités en amont, dans l’utilisation des définitions de syntaxe Monarch par l’[Éditeur Monaco](https://github.com/Microsoft/monaco-editor). Pour savoir comment apporter des contributions, lisez le [guide du contributeur Monaco](https://github.com/Microsoft/monaco-editor/blob/master/CONTRIBUTING.md).

## <a name="next-steps"></a>Étapes suivantes

- [Essayer le démarrage rapide de Bash dans Cloud Shell](quickstart.md)
- [Afficher la liste complète des outils Cloud Shell intégrés](features.md)
