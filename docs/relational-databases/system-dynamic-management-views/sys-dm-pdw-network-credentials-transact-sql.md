---
description: sys. dm_pdw_network_credentials (Transact-SQL)
title: sys. dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b66dc3fcdbb358e1177b3db3fd62cc1b8aa80259
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89530931"
---
# <a name="sysdm_pdw_network_credentials-transact-sql"></a>sys. dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Retourne la liste de toutes les informations d’identification réseau stockées dans l' [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance pour tous les serveurs cibles. Les résultats sont répertoriés pour le nœud de contrôle et tous les nœuds de calcul.  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|ID numérique unique associé au nœud.|  
|target_server_name|**nvarchar(32)**|Adresse IP du serveur cible qui [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] accédera à l’aide des informations d’identification du nom d’utilisateur et du mot de passe.|  
|username|**nvarchar(32)**|Nom d’utilisateur pour lequel le mot de passe est stocké.|  
|last_modified|**datetime**|Date et heure de la dernière opération ayant modifié les informations d’identification.|  
  
## <a name="permissions"></a>Autorisations  
 Requiert l’état du serveur d’affichage.  
  
## <a name="general-remarks"></a>Remarques d'ordre général  
 La clé de cette vue de gestion dynamique est *pdw_node_id* plus *target_server_name*.  
  
## <a name="see-also"></a>Voir aussi  
 [SQL Data Warehouse et les vues de gestion dynamique Data Warehouse parallèles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
