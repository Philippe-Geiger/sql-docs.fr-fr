---
description: SQLProcedures
title: SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 801f814433feddf26a7f8438bd543ce0d3c85e8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423971"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Toutes les procédures stockées [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retournent une valeur. Les rapports **SQLProcedures** SQL_PT_FUNCTION pour la colonne de l’ensemble de résultats PROCEDURE_TYPE.  
  
 **SQLProcedures** retourne SQL_SUCCESS si des valeurs existent pour les paramètres *nomcatalogue, SchemaName* ou *procname* . **SQLFetch** retourne SQL_NO_DATA lorsque des valeurs non valides sont utilisées dans ces paramètres.  
  
 Les **SQLProcedures** peuvent être exécutés sur un curseur côté serveur statique. Une tentative d’exécution de **SQLProcedures** sur un curseur pouvant être mis à jour (dynamique ou de jeu de clés) retourne SQL_SUCCESS_WITH_INFO, ce qui indique que le type de curseur a été modifié.  
  
 **SQLProcedures** retourne des informations sur les procédures dont les noms correspondent à *procname* et peuvent être exécutés par l’utilisateur actuel, ou pour lesquels l’utilisateur actuel a reçu l’autorisation View definition.  
  
## <a name="see-also"></a>Voir aussi  
 [SQLProcedures (fonction)](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [Détails de l’implémentation d’API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
