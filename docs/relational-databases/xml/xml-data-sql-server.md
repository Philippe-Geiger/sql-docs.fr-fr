---
title: Données XML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML [SQL Server]
- XML [SQL Server], about XML
ms.assetid: 6a1793c9-9856-485c-aac5-88fda62f61a8
author: RothJa
ms.author: jroth
ms.openlocfilehash: 8fed086b5553e8c8f4368f7ef671c074fe342362
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729814"
---
# <a name="xml-data-sql-server"></a>Données XML (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] constitue une puissante plateforme de développement d’applications d’une grande richesse pour la gestion des données semi-structurées. La prise en charge de XML est intégrée à tous les composants de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] et sous-entend :  
  
-   Le type de données **xml** . Les valeurs XML peuvent être stockées de façon native dans une colonne de type de données **xml** qui peut être typée en fonction d’une collection de schémas XML ou rester non typée. Vous pouvez indexer la colonne XML.  
  
-   La possibilité de spécifier une requête XQuery sur des données XML stockées dans des colonnes et des variables de type **xml** .  
  
-   Optimisation de OPENROWSET pour permettre le chargement en masse de données XML  
  
-   La clause FOR XML, pour extraire les données relationnelles au format XML.  
  
-   La fonction OPENXML, pour extraire les données XML au format relationnel.  
  
## <a name="in-this-section"></a>Dans cette section  
 [Type et colonnes de données XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md)  
 [Index XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
 [Collections de schémas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)  
  
## <a name="related-content"></a>Contenu associé  
 [Exemples d’importation et d’exportation en bloc de documents XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
 [Références relatives au langage Xquery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
 [xml (Transact-SQL)](../../t-sql/xml/xml-transact-sql.md)
  
