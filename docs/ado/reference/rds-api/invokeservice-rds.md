---
description: InvokeService (RDS)
title: InvokeService (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: rothja
ms.author: jroth
ms.openlocfilehash: acd5dc5f78319c8fc75891dbaad5a98fc4463196
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981970"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
Retourne un pointeur vers l’interface demandée sur une version plus puissante de l’objet.  
  
> [!IMPORTANT]
>  À compter de Windows 8 et de Windows Server 2012, les composants serveur RDS ne sont plus inclus dans le système d’exploitation Windows (pour plus d’informations, consultez le livre de recettes sur la compatibilité avec Windows 8 et [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) ). Les composants clients RDS seront supprimés dans une prochaine version de Windows. Évitez d'utiliser cette fonctionnalité dans de nouveaux travaux de développement, et prévoyez de modifier les applications qui utilisent actuellement cette fonctionnalité. Les applications qui utilisent RDS doivent migrer vers le  [service de données WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>Paramètres  
 *riid*  
  
 dans Identificateur de l’interface demandée.  
  
 *punkNotSoFunctionalInterface*  
  
 dans Objet source qui est le moins performant.  
  
 *ppunkMoreFunctionalInterface*  
  
 à Adresse de la variable pointeur qui reçoit le pointeur d’interface demandé dans *riid*. En cas de retour correct, le paramètre *ppunkMoreFunctionalInterface* contient le pointeur d’interface demandé à l’objet. Si l’objet ne prend pas en charge l’interface spécifiée dans *riid*, *ppunkMoreFunctionalInterface* a la valeur null.  
  
## <a name="return-value"></a>Valeur renvoyée  
 Valeur HRESULT qui indique si l’appel à la méthode **InvokeService** a réussi.  
  
## <a name="remarks"></a>Notes  
 L’implémentation du moteur de curseurs RDS de **InvokeService** prend l’ensemble de lignes d’entrée (ou plusieurs objets de résultats), remplit le moteur de curseur à partir de l’ensemble de lignes d’entrée, puis retourne un pointeur sur lui-même.  
  
## <a name="applies-to"></a>S'applique à  
 [IRDSService, interface (RDS)](./irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Méthodes RDS](./rds-methods.md)