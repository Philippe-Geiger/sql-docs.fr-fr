---
description: CursorLocationEnum
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: rothja
ms.author: jroth
ms.openlocfilehash: 206d9da9130c0dce78e0f8748bf3ace8634dab44
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974420"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Spécifie l’emplacement du service de curseur.  
  
|Constante|Valeur|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Utilise des curseurs côté client fournis par une bibliothèque de curseurs locale. Les services de curseur locaux autorisent souvent de nombreuses fonctionnalités que les curseurs fournis par le pilote peuvent ne pas. l’utilisation de ce paramètre peut donc offrir un avantage en ce qui concerne les fonctionnalités qui seront activées. Pour la compatibilité descendante, le synonyme **adUseClientBatch** est également pris en charge.|  
|**adUseNone**|1|N’utilise pas les services de curseur. (Cette constante est obsolète et s’affiche uniquement pour des raisons de compatibilité descendante.)|  
|**adUseServer**|2|Par défaut. Utilise des curseurs fournis par le fournisseur de données ou le pilote. Ces curseurs sont parfois très flexibles et permettent de renforcer la sensibilité aux modifications apportées par d’autres personnes à la source de données. Toutefois, certaines fonctionnalités du [service de curseur Microsoft pour OLE DB](../../guide/data/the-microsoft-cursor-service-for-ole-db.md), telles que dissociées<br /><br /> Les objets [Recordset](./recordset-object-ado.md) ne peuvent pas être simulés avec des curseurs côté serveur et ces fonctionnalités ne seront pas disponibles avec ce paramètre.|  
  
## <a name="adowfc-equivalent"></a>Équivalent ADO/WFC  
 Package : **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. CursorLocation. CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>S'applique à  
 [CursorLocation, propriété (ADO)](./cursorlocation-property-ado.md)