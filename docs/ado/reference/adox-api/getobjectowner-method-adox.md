---
description: GetObjectOwner, méthode (ADOX)
title: GetObjectOwner, méthode (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f065e2625afa088489f08ade9f4ef00c5eb7d4d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984540"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner, méthode (ADOX)
Retourne le propriétaire d’un objet dans un [catalogue](./catalog-object-adox.md).  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valeur de retour  
 Retourne une valeur de **chaîne** qui spécifie le [nom](./name-property-adox.md) de l' [utilisateur](./user-object-adox.md) ou du [groupe](./group-object-adox.md) propriétaire de l’objet.  
  
#### <a name="parameters"></a>Paramètres  
 *ObjectName*  
 Valeur de **chaîne** qui spécifie le nom de l’objet pour lequel le propriétaire doit être retourné.  
  
 *ObjectType*  
 Valeur de type **long** qui peut être l’une des constantes [ObjectTypeEnum](./objecttypeenum.md) , qui spécifie le type de l’objet pour lequel obtenir le propriétaire.  
  
 *ObjectTypeId*  
 facultatif. Valeur de **type Variant** qui spécifie le GUID pour un type d’objet fournisseur non défini par la spécification OLE DB. Ce paramètre est obligatoire si *ObjectType* a la valeur **adPermObjProviderSpecific**; dans le cas contraire, il n’est pas utilisé.  
  
## <a name="remarks"></a>Notes  
 Une erreur se produit si le fournisseur ne prend pas en charge le retour de propriétaires d’objets.  
  
## <a name="applies-to"></a>S'applique à  
 [Catalog, objet (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>Voir aussi  
 [GetObjectOwner et SetObjectOwner, exemple de méthodes (VB)](./getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner, méthode](./setobjectowner-method.md)