---
description: sys.function_order_columns (Transact-SQL)
title: sys. function_order_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c7ac555630f4472e5cf58ad9017cdb03643ae2b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546791"
---
# <a name="sysfunction_order_columns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retourne une ligne par colonne qui fait partie d’une expression de **commande** d’une fonction table CLR (Common Language Runtime).  

  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID de l'objet (fonction table CLR) sur lequel l'ordre est défini.|  
|**order_column_id**|**int**|ID de la colonne d'ordre. **order_column_id** n’est unique que dans **object_id**.<br /><br /> **order_column_id** représente la position de cette colonne dans le classement.|  
|**column_id**|**int**|ID de la colonne dans **object_id**.<br /><br /> **column_id** n’est unique que dans **object_id**.|  
|**is_descending**|**bit**|1 = colonne d'ordre avec un ordre de tri descendant.<br /><br /> 0 = colonne d'ordre avec un ordre de tri ascendant.|  
  
## <a name="permissions"></a>Autorisations  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Pour plus d'informations, consultez [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Vues de catalogue d’objets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Affichages catalogue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
