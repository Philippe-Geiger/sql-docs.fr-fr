---
description: LEFT (expression SSIS)
title: LEFT (expression SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 619fea9cdf5f9445d9da3146f98453e0d5d60550
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425461"
---
# <a name="left-ssis-expression"></a>LEFT (expression SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Renvoie le nombre de caractères spécifié en commençant par la partie la plus à gauche d'une expression de caractères donnée.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
LEFT(character_expression,number)  
```  
  
## <a name="arguments"></a>Arguments  
 *expression_caractère*  
 Expression de caractères à partir de laquelle doivent être extraits les caractères.  
  
 *number*  
 Expression entière indiquant le nombre de caractères à renvoyer.  
  
## <a name="result-types"></a>Types des résultats  
 DT_WSTR  
  
## <a name="remarks"></a>Notes  
 Si *number* est supérieur à la longueur de *character_expression*, la fonction retourne *character_expression*.  
  
 Si l'argument *number* a pour valeur zéro, la fonction renvoie une chaîne de longueur nulle.  
  
 Si l'argument *number* est un nombre négatif, la fonction renvoie une erreur.  
  
 L'argument *number* peut accepter des variables et des colonnes.  
  
 La fonction LEFT fonctionne seulement avec le type de données DT_WSTR. Un argument *character_expression* qui est un littéral de chaîne ou une colonne de données avec le type de données DT_STR est implicitement converti dans le type de données DT_WSTR avant que LEFT effectue son opération. Les autres types de données doivent être explicitement convertis vers le type de données DT_WSTR. Pour plus d’informations, consultez [Types de données d’Integration Services](../../integration-services/data-flow/integration-services-data-types.md) et [Cast &#40;expression SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 La fonction LEFT renvoie un résultat NULL si l'un des arguments est NULL.  
  
## <a name="expression-examples"></a>Exemples d'expressions  
 L'exemple suivant utilise un littéral de chaîne. Le résultat obtenu est `"Mountain"`.  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>Voir aussi  
 [RIGHT &#40;expression SSIS&#41;](../../integration-services/expressions/right-ssis-expression.md)   
 [Fonctions &#40;expression SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
