---
title: IServerVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: Cet article fournit des informations de référence sur la commande IServerVirtualDeviceSet2::OpenDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b43f2adedde0c317f24ee811c4ac1b2a69057de2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898922"
---
# <a name="iservervirtualdeviceset2opendevice-vdi"></a>IServerVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La fonction **OpenDevice** obtient les interfaces des appareils virtuels auprès de l’ensemble d’appareils virtuels.

## <a name="syntax"></a>Syntaxe

```c
HRESULT IServerVirtualDeviceSet2::OpenDevice (
   LPCWSTR                     lpName,
   IServerVirtualDevice**      ppVirtualDevice
);
```

## <a name="parameters"></a>Paramètres

*lpName* : fourni à partir de la première clause VIRTUAL_DEVICE = de la commande BACKUP ou RESTORE. Ce nom est utilisé comme clé pour obtenir l’accès à l’ensemble d’appareils virtuels créé par le client.

*ppVirtualDevice* : utilisé pour retourner une interface d’appareil virtuel.

## <a name="return-value"></a>Valeur de retour

|Valeur de retour | Explication |
|---|---|
| NOERROR | La fonction a réussi. |
| VD_E_OPEN |Tous les appareils ont été ouverts. |

## <a name="remarks"></a>Notes

Chaque appel retourne l’appareil non ouvert suivant. La fonction ne peut être appelée qu’un nombre de fois égal au nombre d’appareils spécifié dans la configuration de l’ensemble d’appareils virtuels.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez [Vue d’ensemble des informations de référence sur l’interface des appareils virtuels SQL Server](reference-virtual-device-interface.md).