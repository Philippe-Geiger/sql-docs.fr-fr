---
description: cdc.captured_columns (Transact-SQL)
title: CDC. captured_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.captured_columns
- cdc.captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.captured_columns
ms.assetid: 7bb4d408-d764-4ef6-802c-f271c8d39c2a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 675d6934c468b4f2a4574b82e79c203ab4796c9a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538353"
---
# <a name="cdccaptured_columns-transact-sql"></a>cdc.captured_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retourne une ligne pour chaque colonne suivie dans une instance de capture. Par défaut, toutes les colonnes de la table source sont capturées. Toutefois, les colonnes peuvent être incluses ou exclues lorsque la table source est activée pour la capture des données modifiées en spécifiant une liste de colonnes. Pour plus d’informations, consultez [sys. sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 Nous vous recommandons de ne **pas interroger directement les tables système**. Au lieu de cela, exécutez la procédure stockée [sys. sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md) .  
   
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificateur de la table source à laquelle appartient la colonne capturée.|  
|**column_name**|**sysname**|Nom de la colonne capturée.|  
|**column_id**|**int**|ID de la colonne capturée dans la table source.|  
|**column_type**|**sysname**|Type de la colonne capturée.|  
|**column_ordinal**|**int**|Ordinal de colonne (de base 1) dans la table de modifications. Les colonnes de métadonnées dans la table de modifications sont exclues. L'ordinal 1 est assigné à la première colonne capturée.|  
|**is_computed**|**bit**|Indique que la colonne capturée est une colonne calculée dans la table source.|  
  
## <a name="see-also"></a>Voir aussi  
 [CDC. change_tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
