---
title: Présentation des pools de données
titleSuffix: SQL Server big data clusters
description: Découvrez le rôle des pools de données SQL Server dans un cluster Big Data SQL Server, ainsi que l’architecture et les fonctionnalités d’un pool de données SQL.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4d9eaba636c2567d60dfc62ce37080717e9c32e9
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680566"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>Présentation des pools de données dans un cluster Big Data SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Cet article décrit le rôle des *pools de données SQL Server* dans un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Les sections suivantes décrivent l’architecture et les fonctionnalités d’un pool de données SQL.

Cette vidéo de 5 minutes présente des pools de données et vous montre comment interroger des données à partir de pools de données :

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Querying-Data-from-Big-Data-Cluster-Data-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="data-pool-architecture"></a>Architecture du pool de données

Un pool de données se compose d’une ou plusieurs instances de pool de données SQL Server. Les instances de pool de données SQL assurent un stockage SQL Server persistant pour le cluster. Un pool de données est utilisé pour l’ingestion des données à partir de requêtes SQL ou de travaux Spark. Pour améliorer les performances dans des jeux de données volumineux, les données d’un pool de données sont réparties en partitions sur les instances de pools de données SQL membres.

## <a name="scale-out-data-marts"></a>DataMart avec scale-out

Les pools de données permettent de créer des DataMarts avec scale-out où les données externes de plusieurs sources sont ingérées dans le pool de données. Les données étant réparties entre plusieurs instances du pool de données, les requêtes parallèles sur les données organisées sont plus efficaces.

![DataMart avec scale-out](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur les [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], consultez les ressources suivantes :

- [Que sont les [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ?](big-data-cluster-overview.md)
- [Atelier : Architecture des [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
