---
title: namespace-URI-from-QName (XQuery) | Microsoft Docs
description: Découvrez comment utiliser la fonction namespace-URI-from-QName pour récupérer l’URI d’espace de noms d’un QName.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 91174fa3ef113a7944ef02bb62e7088acd344f3e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720031"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Fonctions relatives aux QName : namespace-uri-from-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retourne une chaîne représentant l’URI d’espace de noms du QName spécifié par *$arg*. Le résultat est la séquence vide si *$arg* est la séquence vide.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>Arguments  
 *$arg*  
 est le QName d'où est renvoyé l'URI d'espace de noms.  
  
## <a name="examples"></a>Exemples  
 Cette rubrique fournit des exemples de XQuery relatifs à des instances XML stockées dans différentes colonnes de type **XML** dans la base de données AdventureWorks.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. Récupération d'un URI d'espace de noms à partir d'un QName  
 Pour obtenir un exemple fonctionnel, consultez [local-name-from-QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>Limites de mise en œuvre  
 Les limitations suivantes s'appliquent :  
  
-   La fonction **namespace-URI-from-QName ()** retourne des instances de XS : String au lieu de XS : anyURI.  
  
## <a name="see-also"></a>Voir aussi  
 [Fonctions liées à QNames &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
