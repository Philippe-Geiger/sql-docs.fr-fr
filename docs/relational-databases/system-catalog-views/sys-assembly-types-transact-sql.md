---
description: sys.assembly_types (Transact-SQL)
title: sys. assembly_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 06eb2eb4fe6b0983b798ea38fa98057be73af77a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545069"
---
# <a name="sysassembly_types-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Contient une ligne pour chaque type défini par l'utilisateur et par un assembly CLR. La **sys. assembly_types** suivante s’affiche dans la liste des colonnes héritées (consultez [sys. types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) après **rule_object_id**.  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|ID de l'assembly à partir duquel ce type est créé.|  
|**assembly_class**|**sysname**|Nom de la classe dans l'assembly qui définit ce type.|  
|**is_binary_ordered**|**bit**|Trier les octets de ce type revient à trier les opérateurs de comparaison sur ce même type.|  
|**is_fixed_length**|**bit**|La longueur du type est toujours identique à max_length.|  
|**prog_id**|**nvarchar(40)**|ProgID du type exposé à COM.|  
|**assembly_qualified_name**|**nvarchar(4000)**|Nom du type qualifié de l'assembly. Le formatage du nom est tel qu'il peut être transmis à Type.GetType().|  
  
## <a name="permissions"></a>Autorisations  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Pour plus d'informations, consultez [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Affichages catalogue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Affichages catalogue types scalaires &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
