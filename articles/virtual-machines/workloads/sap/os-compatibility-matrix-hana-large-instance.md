---
title: Matrice de compatibilité du système d'exploitation pour SAP HANA (Grandes instances) | Microsoft Docs
description: La matrice de compatibilité présente la compatibilité des différentes versions du système d'exploitation avec différents types de matériel (Grandes instances)
services: virtual-machines-linux
documentationcenter: ''
author: sasarava
manager: hrushib
editor: ''
ms.service: virtual-machines-sap
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2020
ms.author: sasarava
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ccfdffc4e488de7f3cecb150305596743b3a9e44
ms.sourcegitcommit: b4647f06c0953435af3cb24baaf6d15a5a761a9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2021
ms.locfileid: "101675407"
---
# <a name="compatible-operating-systems-for-hana-large-instances"></a>Systèmes d'exploitation compatibles pour HANA - Grandes instances

## <a name="hana-large-instance-type-i"></a>HANA - Grandes instances Type I     
  | Système d’exploitation | Disponibilité        | Références (SKU)                                                          |
  |------------------|---------------------|---------------------------------------------------------------|
  | SLES 12 SP2      | Plus proposé | S72, S72m, S96, S144, S144m, S192, S192m, S192xm              |
  | SLES 12 SP3      | Disponible           | S72, S72m, S96, S144, S144m, S192, S192m, S192xm              |
  | SLES 12 SP4      | Disponible           | S72, S72m, S96, S144, S144m, S192, S192m, S192xm, S224, S224m |
  | SLES 12 SP5      | Disponible           | S72, S72m, S96, S144, S144m, S192, S192m, S192xm, S224, S224m |
  | SLES 15 SP1      | Disponible           | S72, S72m, S96, S144, S144m, S192, S192m, S192xm, S224, S224m |
  | RHEL 7.6         | Disponible           | S72, S72m, S96, S144, S144m, S192, S192m, S192xm, S224, S224m |

  
### <a name="persistent-memory-skus"></a>Références SKU de mémoire persistante
  | Système d’exploitation | Disponibilité | Références (SKU)                             |
  |------------------|--------------|----------------------------------|
  | SLES 12 SP4      | Disponible    | S224oo, S224om, S224ooo, S224oom |
  
## <a name="hana-large-instance-type-ii"></a>HANA - Grandes instances Type II     
  |  Système d’exploitation       | Disponibilité        | Références (SKU)                                                                     |
  |-------------------------|---------------------|--------------------------------------------------------------------------|
  | SLES 12 SP2             | Plus proposé | S384, S384m, S384xm, S384xxm, S576m, S576xm, S768m, S768xm, S960m        |
  | SLES 12 SP3             | Disponible           | S384, S384m, S384xm, S384xxm, S576m, S576xm, S768m, S768xm, S960m        |
  | SLES 12 SP4             | Disponible           | S384, S384m, S384xm, S384xxm, S576m, S576xm, S768m, S768xm, S960m        |
  | SLES 12 SP5             | Disponible           | S384, S384m, S384xm, S384xxm, S576m, S576xm, S768m, S768xm, S896m, S960m |
  | SLES 15 SP1             | Disponible           | S384, S384m, S384xm, S384xxm, S576m, S576xm, S768m, S768xm, S896m, S960m |
  | RHEL 7.6                | Disponible           | S384, S384m, S384xm, S384xxm, S576m, S576xm, S768m, S768xm, S896m, S960m |

## <a name="related-documents"></a>Documents associés

- Pour en savoir plus sur les [Références SKU disponibles](hana-available-skus.md)
- Pour savoir plus sur la [Mise à niveau du système d'exploitation](os-upgrade-hana-large-instance.md)
  

  
  
