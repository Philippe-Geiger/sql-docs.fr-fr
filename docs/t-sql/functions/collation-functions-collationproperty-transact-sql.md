---
description: Fonctions de classement - COLLATIONPROPERTY (Transact-SQL)
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLLATIONPROPERTY_TSQL
- COLLATIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], properties
- COLLATIONPROPERTY function
ms.assetid: f5029e74-a1db-4f69-b0f5-5ee920c3311d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67977deba00a1df52a9264256b83f6e57bc49ed5
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116129"
---
# <a name="collation-functions---collationproperty-transact-sql"></a>Fonctions de classement - COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Cette fonction retourne la propriété demandée d’un classement spécifié.
  
![Icône Lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône du lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntaxe  
  
```syntaxsql
COLLATIONPROPERTY( collation_name , property )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Arguments
*collation_name*  
Nom du classement. L’argument *collation_name* a un type de données **nvarchar(128)**, sans valeur par défaut.
  
*property*  
Propriété du classement. L’argument *property* a un type de données **varchar(128)** et peut avoir une des valeurs suivantes :
  
|Nom de la propriété|Description|  
|---|---|
|**CodePage**|Page de codes non-Unicode du classement. Il s’agit du jeu de caractères utilisé pour les données **varchar**. Consultez [Annexe G – Tables de mappage DBCS/Unicode](https://msdn.microsoft.com/library/cc194886.aspx) et [Annexe H – Pages de code](https://msdn.microsoft.com/library/cc195051.aspx) pour convertir ces valeurs et voir leurs mappages de caractères.<br /><br />Type de données de base : **int**|  
|**LCID**|ID des paramètres régionaux Windows. Il s’agit de la culture utilisée pour les règles de tri et de comparaison. Consultez [Structure LCID](https://msdn.microsoft.com/library/cc233968.aspx) pour convertir ces valeurs (vous devrez commencer par les convertir en **varbinary**).<br /><br />Type de données de base : **int**|  
|**ComparisonStyle**|Style de comparaison Windows du classement. Retourne 0 pour les classements binaires - à la fois (\_BIN) et (\_BIN2) - ainsi que quand toutes les propriétés respectent les caractères (\_CS\_AS\_KS\_WS) et (\_CS\_AS\_KS\_WS\_SC) et (\_CS\_AS\_KS\_WS\_VSS). Valeurs de masque de bits :<br /><br /> Ignorer la casse : 1<br /><br /> Ignorer les accents : 2<br /><br /> Ignorer le type de caractères Kana : 65536<br /><br /> Ignorer la largeur : 131 072<br /><br /> Remarque : L’option de sélecteur de variante (\_VSS) n’est pas représentée dans cette valeur, même si elle affecte le comportement de la comparaison.<br /><br />Type de données de base : **int**|  
|**Version**|Version du classement. Retourne une valeur comprise entre 0 et 3.<br /><br /> Les classements dont le nom contient « 140 » retournent 3.<br /><br /> Les classements dont le nom contient « 100 » retournent 2.<br /><br /> Les classements dont le nom contient « 90 » retournent 1.<br /><br /> Tous les autres classements retournent 0.<br /><br />Type de données de base : **tinyint**|  
  
## <a name="return-types"></a>Types de retour
**sql_variant**
  
## <a name="examples"></a>Exemples  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] et [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
1252   
```  
  
## <a name="see-also"></a>Voir aussi
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  

