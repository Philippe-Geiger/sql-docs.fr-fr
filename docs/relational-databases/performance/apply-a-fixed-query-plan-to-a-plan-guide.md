---
title: Appliquer un plan de requête fixe à un repère de plan | Microsoft Docs
description: Découvrez comment appliquer un plan de requête fixe à un repère de plan de type OBJET ou SQL dans SQL Server. Cet exemple crée un repère de plan pour une instruction SQL ad hoc simple.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: bbf401f9-af7c-48e7-8a43-bf25e8af2fd7
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b39441ba86d8337fd4a59d9ffbc1f27a68c569ca
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458611"
---
# <a name="apply-a-fixed-query-plan-to-a-plan-guide"></a>Appliquer un plan de requête fixe à un repère de plan
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Vous pouvez appliquer un plan de requête fixe à un repère de plan de type OBJET ou SQL. Les repères de plan qui appliquent un plan de requête fixe sont utiles lorsque vous avez connaissance d'un plan d'exécution existant plus performant que celui sélectionné par l'optimiseur pour une requête particulière.  
  
 L'exemple suivant crée un repère de plan pour une instruction SQL ad hoc simple. Le plan de requête souhaité pour cette instruction est fourni dans le repère de plan en spécifiant directement le plan d'exécution XML pour la requête dans le paramètre `@hints` . L'exemple exécute en premier l'instruction SQL pour générer un plan dans le cache du plan. Pour les besoins de cet exemple, il est supposé que le plan généré est le plan souhaité et qu'aucune analyse de requête supplémentaire n'est requise. Le plan d'exécution de requêtes XML pour la requête est obtenu en interrogeant les vues de gestion dynamique `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`et `sys.dm_exec_text_query_plan` , et est assigné à la variable `@xml_showplan` . La variable `@xml_showplan` est ensuite transmise à l'instruction `sp_create_plan_guide` dans le paramètre `@hints` . Vous pouvez aussi créer un repère de plan à partir d’un plan de requête dans le cache des plans à l’aide de la procédure stockée [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = @xml_showplan;  
GO  
```  
  
  
