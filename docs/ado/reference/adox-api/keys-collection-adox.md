---
description: Keys, collection (ADOX)
title: Keys, collection (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: rothja
ms.author: jroth
ms.openlocfilehash: 675584dd52cd1a403b9d9d44351b86e88caba382
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983980"
---
# <a name="keys-collection-adox"></a>Keys, collection (ADOX)
Contient tous les objets [clés](./key-object-adox.md) d’une [table](./table-object-adox.md).  
  
## <a name="remarks"></a>Notes  
 La méthode [Append](./append-method-adox-keys.md) d’une [collection Keys]() est unique pour ADOX. Vous pouvez :  
  
-   Ajoutez une nouvelle clé à la collection à l’aide de la méthode [Append](./append-method-adox-keys.md) .  
  
 Les propriétés et les méthodes restantes sont standard pour les collections ADO. Vous pouvez :  
  
-   Accédez à une clé de la collection avec la propriété [Item](../ado-api/item-property-ado.md) .  
  
-   Retourne le nombre de clés contenues dans la collection avec la propriété [Count](../ado-api/count-property-ado.md) .  
  
-   Supprime une clé de la collection à l’aide de la méthode [Delete](./delete-method-adox-collections.md) .  
  
-   Mettez à jour les objets de la collection pour refléter le schéma de la base de données actuelle avec la méthode [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Cette section contient la rubrique suivante.  
  
-   [Propriétés, méthodes et événements de la collection Indexes](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Méthodes Append des clés, type de clé, RelatedColumn, RelatedTable et UpdateRule, exemple de propriétés (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Propriétés, méthodes et événements de la collection Keys](./keys-collection-properties-methods-and-events.md)   
 [Key, objet (ADOX)](./key-object-adox.md)