---
description: Z (type de données geometry)
title: Z (type de données geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2e90df19c6d6946c17b554c9195c03bce3f55ca8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472370"
---
# <a name="z-geometry-data-type"></a>Z (type de données geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Valeur Z (élévation) de l'instance. La sémantique de la valeur d'élévation est définie par l'utilisateur.
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
.Z  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Types de retour
 Type [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **float**  
  
 Type CLR : **SqlDouble**  
  
## <a name="remarks"></a>Notes  
 La valeur de cette propriété est Null si l’instance geometry n’est pas un point, ainsi que pour toute instance **Point** pour laquelle elle n’est pas définie.  
  
 Cette propriété est en lecture seule.  
  
 Les coordonnées Z ne sont pas utilisées dans les calculs effectués par la bibliothèque et ne sont pas reportées dans les calculs de bibliothèque.  
  
## <a name="examples"></a>Exemples  
 L'exemple suivant crée une instance `Point` avec des valeurs Z (élévation) et M (mesure) et utilise `Z` pour extraire la valeur Z de l'instance.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>Voir aussi  
 [M &#40;type de données geometry&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM &#40;type de données geometry&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [Méthodes étendues sur les instances géométriques](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

