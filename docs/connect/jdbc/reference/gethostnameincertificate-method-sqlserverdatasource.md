---
description: Méthode getHostNameInCertificate (SQLServerDataSource)
title: Méthode getHostNameInCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26e931b104c1eba44a09e1b43b51e00d2beaad70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435871"
---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>Méthode getHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retourne le nom d’hôte utilisé dans la validation du certificat TLS (Transport Layer Security), anciennement SSL (Secure Sockets Layer), SQL Server.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>Valeur de retour  
 **Chaîne** contenant le nom d’hôte ou Null si aucune valeur n’est définie.  
  
## <a name="remarks"></a>Notes  
 Le nom d’hôte sert à valider la valeur du certificat TLS/SSL SQL Server quand la couche de communication est chiffrée à l’aide du protocole TLS/SSL.  
  
 Si le nom d’hôte n’est pas défini, la méthode [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) retourne la valeur Null.  
  
## <a name="see-also"></a>Voir aussi  
 [SQLServerDataSource, membres](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource, classe](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
