---
description: sys. pdw_loader_backup_run_details (Transact-SQL)
title: sys. pdw_loader_backup_run_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d42094beb9b29cc620007bb1d590a6fa8dc33987
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400525"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>sys. pdw_loader_backup_run_details (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contient des informations détaillées supplémentaires, au-delà des informations de [sys. pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), sur les opérations de sauvegarde et de restauration en cours et terminées dans [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] et sur les opérations de sauvegarde, de restauration et de chargement en cours et terminées dans [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] . Ces informations sont conservées après le redémarrage du système.  
  
|Nom de la colonne|Type de données|Description|Plage|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificateur unique pour une exécution de sauvegarde ou de restauration spécifique.<br /><br /> run_id et pdw_node_id forment la clé de cette vue.||  
|pdw_node_id|**int**|Identificateur unique d’un nœud d’appliance pour lequel cet enregistrement contient des détails.<br /><br /> run_id et pdw_node_id forment la clé de cette vue.|Consultez node_id dans [sys. dm_pdw_nodes &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar (16)**|État actuel de l’exécution.|« CANCELLED », « COMPLETED », « FAILED », « QUEUED », « RUNNING »|  
|start_time|**datetime**|Heure à laquelle l’opération a démarré sur ce nœud particulier.||  
|end_time|**datetime**|Heure à laquelle l’opération se termine sur ce nœud particulier, le cas échéant.||  
|total_elapsed_time|**int**|Durée totale d’exécution de l’opération sur ce nœud particulier.|Si total_elapsed_time dépasse la valeur maximale d’un entier (24,8 jours en millisecondes), cela entraînera un échec de matérialisation en raison d’un dépassement de capacité.<br /><br /> La valeur maximale en millisecondes est équivalente à 24,8 jours.|  
|progress|**int**|Progression de l’opération exprimée sous la forme d’un pourcentage.|0 à 100|  
  
## <a name="see-also"></a>Voir aussi  
 [Affichages catalogue SQL Data Warehouse et Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
