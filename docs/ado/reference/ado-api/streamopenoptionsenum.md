---
description: StreamOpenOptionsEnum
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f3865a3b0e550e7e3fe4887fb948bca72eadf1b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988500"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Spécifie les options d’ouverture d’un objet de [flux](./stream-object-ado.md) . Les valeurs peuvent être combinées avec une opération OR.  
  
|Constante|Valeur|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Ouvre l’objet de **flux** en mode asynchrone.|  
|**adOpenStreamFromRecord**|4|Identifie le contenu du paramètre *source* comme étant un objet [enregistrement](./record-object-ado.md) déjà ouvert. Le comportement par défaut consiste à traiter la *source* comme une URL qui pointe directement vers un nœud dans une arborescence. Le flux par défaut associé à ce nœud est ouvert.|  
|**adOpenStreamUnspecified**|-1|Par défaut. Spécifie l’ouverture de l’objet de **flux** avec les options par défaut.|  
  
## <a name="adowfc-equivalent"></a>Équivalent ADO/WFC  
 Ces constantes n’ont pas d’équivalents ADO/WFC.  
  
## <a name="applies-to"></a>S'applique à  
 [Open, méthode (Stream ADO)](./open-method-ado-stream.md)