---
description: '&#x40;&#x40;CURSOR_ROWS (Transact-SQL)'
title: '@@CURSOR_ROWS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@CURSOR_ROWS'
- '@@CURSOR_ROWS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CURSOR_ROWS function'
- cursors [SQL Server], last-opened
- last-opened cursor
- asynchronous cursors [SQL Server]
ms.assetid: 31bd7a97-7f28-42a8-ba24-24d16d22973d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: afc9e800545ffdc3002c0bfbddbb572432b10589
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91114859"
---
# <a name="x40x40cursor_rows-transact-sql"></a>&#x40;&#x40;CURSOR_ROWS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Cette fonction retourne le nombre de lignes éligibles se trouvant actuellement dans le dernier curseur ouvert sur la connexion. Afin d'améliorer les performances, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] peut charger de grands curseurs pilotés par jeux de clés et curseurs statiques de manière asynchrone. `@@CURSOR_ROWS` peut être appelée pour déterminer que le nombre de lignes éligibles pour un curseur sont extraites au moment de l’appel de @@CURSOR_ROWS.
  
![Icône Lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône du lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntaxe  
  
```syntaxsql
@@CURSOR_ROWS  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Types de retour
**integer**
  
## <a name="return-value"></a>Valeur de retour  
  
|Valeur retournée|Description|  
|---|---|
|-*m*|Le curseur se remplit de façon asynchrone. La valeur retournée (-*m*) correspond au nombre de lignes figurant actuellement dans le jeu de clés.|  
|-1|Le curseur est dynamique. Sachant que les curseurs dynamiques reflètent toutes les modifications, le nombre de lignes éligibles pour le curseur varie constamment. Le curseur ne récupère pas nécessairement toutes les lignes éligibles.|  
|0|Aucun curseur n'a été ouvert, aucune ligne n'a été qualifiée pour le dernier curseur ouvert ou le dernier curseur ouvert est fermé ou désalloué.|  
|*n*|Le curseur est totalement rempli. La valeur retournée (*n*) correspond au nombre total de lignes du curseur.|  
  
## <a name="remarks"></a>Notes  
`@@CURSOR_ROWS` retourne un nombre négatif si le dernier curseur s’est ouvert de façon asynchrone. Les curseurs de jeu de clés ou les curseurs statiques s’ouvrent de façon asynchrone si la valeur du seuil de curseur sp_configure est supérieure à 0 et si le nombre de lignes contenues dans le jeu de résultats du curseur est supérieur au seuil du curseur.
  
## <a name="examples"></a>Exemples  
Cet exemple déclare d’abord un curseur et utilise ensuite `SELECT` pour afficher la valeur de `@@CURSOR_ROWS`. Le paramètre a pour valeur `0` avant l’ouverture du curseur et prend ensuite la valeur `-1` pour indiquer que le jeu de clés du curseur est rempli de façon asynchrone.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@CURSOR_ROWS;  
DECLARE Name_Cursor CURSOR FOR  
SELECT LastName ,@@CURSOR_ROWS FROM Person.Person;  
OPEN Name_Cursor;  
FETCH NEXT FROM Name_Cursor;  
SELECT @@CURSOR_ROWS;  
CLOSE Name_Cursor;  
DEALLOCATE Name_Cursor;  
GO             
```  
  
Voici les jeux de résultats obtenus.
  
```
-----------
0  
```

```
LastName
---------------
Sanchez
```

```
-----------
-1
```  
  
## <a name="see-also"></a>Voir aussi
[Fonctions de curseur &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  
