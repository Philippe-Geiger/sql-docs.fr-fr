---
description: sys.dm_tran_top_version_generators (Transact-SQL)
title: sys. dm_tran_top_version_generators (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_top_version_generators
- sys.dm_tran_top_version_generators
- dm_tran_top_version_generators_TSQL
- sys.dm_tran_top_version_generators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_top_version_generators dynamic management view
ms.assetid: cec7809b-ba8a-4df9-b5bb-d4f651ff1a86
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 54e3caeb50a0c6fd9f3a6b1523675eb482005384
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546478"
---
# <a name="sysdm_tran_top_version_generators-transact-sql"></a>sys.dm_tran_top_version_generators (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Renvoie une table virtuelle pour les objets qui génèrent la majorité des versions d'un magasin de versions. **sys. dm_tran_top_version_generators** retourne les 256 premières longueurs d’enregistrements agrégés regroupées par le **database_id** et **rowset_id**. **sys. dm_tran_top_version_generators** récupère les données en interrogeant la table virtuelle **dm_tran_version_store** . **sys. dm_tran_top_version_generators** est une vue inefficace à exécuter, car cette vue interroge la Banque des versions et la Banque des versions peut être très volumineuse. Nous vous recommandons d'utiliser cette fonction pour rechercher les clients les plus volumineux de la banque des versions.  
  
> [!NOTE]  
>  Pour appeler cette valeur à partir de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , utilisez le nom **sys. dm_pdw_nodes_tran_top_version_generators**.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
sys.dm_tran_top_version_generators  
```  
  
## <a name="table-returned"></a>Table retournée  
  
|Nom de la colonne|Type de données|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID de la base de données.|  
|**rowset_id**|**bigint**|ID de l'ensemble de lignes.|  
|**aggregated_record_length_in_bytes**|**int**|Somme des longueurs d’enregistrements pour chaque paire **database_id** et **rowset_id** dans la Banque des versions.|  
|**pdw_node_id**|**int**|**S’applique à**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificateur du nœud sur lequel cette distribution se trouve.|  
  
## <a name="permissions"></a>Autorisations

Sur [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiert l' `VIEW SERVER STATE` autorisation.   
Sur [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] les niveaux Premium, requiert l' `VIEW DATABASE STATE` autorisation dans la base de données. Sur [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] les niveaux standard et de base, nécessite l'  **administrateur du serveur** ou un compte d' **administrateur Azure Active Directory** .   

## <a name="remarks"></a>Notes  
 Étant donné que **sys. dm_tran_top_version_generators** peut avoir besoin de lire de nombreuses pages au cours de l’analyse de l’intégralité de la Banque des versions, l’exécution de **sys. dm_tran_top_version_generators** peut interférer avec les performances du système.  
  
## <a name="examples"></a>Exemples  
 L'exemple suivant illustre un scénario de test dans lequel quatre transactions simultanées, chacune étant identifiée par un numéro de séquence de transaction, sont exécutées dans une base de données où les options ALLOW_SNAPSHOT_ISOLATION et READ_COMMITTED_SNAPSHOT sont définies à ON. Les transactions suivantes sont exécutées :  
  
-   XSN-57 est une opération Update exécutée avec le niveau d'isolement sérialisable.  
  
-   XSN-58 est identique à XSN-57.  
  
-   XSN-59 est une opération Select exécutée avec le niveau d'isolement d'instantané.  
  
-   XSN-60 est identique à XSN-59.  
  
 La requête suivante est exécutée :  
  
```  
SELECT  
    database_id,  
    rowset_id,  
    aggregated_record_length_in_bytes  
  FROM sys.dm_tran_top_version_generators;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
database_id rowset_id            aggregated_record_length_in_bytes  
----------- -------------------- ---------------------------------  
9           72057594038321152    87  
9           72057594038386688    33  
```  
  
 La sortie indique que toutes les versions sont créées par `database_id``9` et que les versions sont générées à partir de deux tables.  
  
## <a name="see-also"></a>Voir aussi  
 [Fonctions et vues de gestion dynamique &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Fonctions et vues de gestion dynamique relatives aux transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


