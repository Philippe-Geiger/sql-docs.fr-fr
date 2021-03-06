---
description: DrilldownMemberBottom (MDX)
title: DrilldownMemberBottom (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b55b71a77a8513619edfde723da0e9d761af3d19
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483982"
---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)


  Extrait vers le bas les membres dans un jeu spécifié qui sont présents dans un second jeu spécifié, ce qui limite l'ensemble de résultats à un nombre spécifique de membres. Cette fonction extrait également vers le bas un jeu de tuples à l'aide de la première hiérarchie de tuple ou de la hiérarchie éventuellement spécifiée.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
DrillDownMemberBottom(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expresion>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Arguments  
 *Set_Expression1*  
 Expression MDX (Multidimensional Expressions) valide qui retourne un jeu.  
  
 *Set_Expression2*  
 Expression MDX (Multidimensional Expressions) valide qui retourne un jeu.  
  
 *Count*  
 Expression numérique valide qui précise le nombre de tuples à retourner.  
  
 *Numeric_Expression*  
 Expression numérique valide qui correspond généralement à une expression MDX (Multidimensional Expressions) des coordonnées des cellules qui retournent un nombre.  
  
 *Hierarchy*  
 Expression MDX (Multidimensional Expressions) valide qui retourne une hiérarchie.  
  
 *Récursive*  
 Mot clé qui indique une comparaison récursive de jeux.  
  
 *Include_Calc_Members*  
 Mot clé permettant d'activer les membres calculés à inclure dans les résultats de l'extraction vers le bas.  
  
## <a name="remarks"></a>Notes  
 Si une expression numérique est spécifiée, la fonction **DrilldownMemberBottom** trie, par ordre croissant, les enfants de chaque membre du premier jeu, en fonction de la valeur de l’expression numérique, telle qu’évaluée sur le jeu de membres enfants. Si aucune expression numérique n'est spécifiée, cette fonction trie, par ordre croissant, les enfants de chaque membre dans le premier jeu selon les valeurs des cellules représentées par le jeu des membres enfants, comme le détermine le contexte de la requête. Ce comportement est semblable aux fonctions BottomCount et Tail (MDX) qui retournent un jeu de membres dans l'ordre naturel, sans tri.  
  
 Après le tri, la fonction **DrilldownMemberBottom** retourne un jeu qui contient les membres parents et le nombre de membres enfants, spécifiés dans *Count,* avec la valeur la plus faible et qui sont contenus par les deux ensembles.  
  
 Si la fonction **récursive** est spécifiée, la fonction trie le premier jeu comme décrit précédemment, puis compare de manière récursive les membres du premier jeu, tels qu’ils sont organisés dans une hiérarchie, par rapport au deuxième jeu. La fonction extrait le nombre le plus faible d'enfants pour chaque membre du premier jeu également présent dans le deuxième jeu.  
  
 Le premier jeu peut contenir des tuples au lieu de membres. L’exploration des tuples est une extension de OLE DB et retourne un jeu de tuples au lieu de membres.  
  
 La fonction **DrilldownMemberBottom** est similaire à la fonction [DrilldownMember](../mdx/drilldownmember-mdx.md) , mais au lieu d’inclure tous les enfants de chaque membre du premier jeu qui est également présent dans le deuxième jeu, la fonction **DrilldownMemberBottom** retourne le nombre le plus bas de membres enfants pour chaque membre.  
  
 L’interrogation de la propriété XMLA MdpropMdxDrillFunctions vous permet de vérifier le niveau de prise en charge fourni par le serveur pour les fonctions de perçage. Pour plus d’informations, consultez [Propriétés XMLA prises en charge &#40;&#41;XMLA ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
## <a name="see-also"></a>Voir aussi  
 [Guide de référence des fonctions MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
