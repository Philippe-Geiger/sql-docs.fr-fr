---
description: Objets ADOX
title: Objets ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [ADOX]
- ADOX, objects
ms.assetid: 3f5287e9-f62c-40c4-bb59-985102be956e
author: rothja
ms.author: jroth
ms.openlocfilehash: c38b184164109ee3e6fed18a439cd904119a3ec6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985660"
---
# <a name="adox-objects"></a>Objets ADOX
## <a name="adox-object-summary"></a>Résumé de l’objet ADOX  
  
|Object|Description|  
|------------|-----------------|  
|[Catalogue](./catalog-object-adox.md)|Contient des collections qui décrivent le catalogue de schémas d’une source de données.|  
|[Colonne](./column-object-adox.md)|Représente une colonne d’une table, d’un index ou d’une clé.|  
|[Groupe](./group-object-adox.md)|Représente un compte de groupe qui dispose d’autorisations d’accès au sein d’une base de données sécurisée.|  
|[Index](./index-object-adox.md)|Représente un index à partir d’une table de base de données.|  
|[Clé](./key-object-adox.md)|Représente un champ clé primaire, étrangère ou unique d’une table de base de données.|  
|[Procédure](./procedure-object-adox.md)|Représente une procédure stockée.|  
|[Table](./table-object-adox.md)|Représente une table de base de données, y compris des colonnes, des index et des clés.|  
|[Utilisateur](./user-object-adox.md)|Représente un compte d’utilisateur qui dispose d’autorisations d’accès au sein d’une base de données sécurisée.|  
|[Visualiser](./view-object-adox.md)|Représente un jeu d’enregistrements filtré ou une table virtuelle.|  
  
 Les relations entre ces objets sont illustrées dans le [modèle objet ADOX](./adox-object-model.md).  
  
 Chaque objet peut être contenu dans sa collection correspondante. Par exemple, un objet **table** peut être contenu dans une collection [tables](./tables-collection-adox.md) . Pour plus d’informations, consultez [regroupements ADOX](./adox-collections.md) ou une rubrique de regroupement spécifique.  
  
## <a name="see-also"></a>Voir aussi  
 [Informations de référence sur l’API ADOX](./adox-object-model.md?view=sql-server-ver15)   
 [Collections ADOX](./adox-collections.md)   
 [Modèle objet ADOX](./adox-object-model.md)   
 [Extensions ADO pour le langage de définition de données et la sécurité (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)