---
description: Propriétés du compte de proxy - Nouveau compte de proxy (page Général)
title: Propriétés du compte de proxy - Nouveau compte de proxy (page Général)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5e466d75990589513ce09e071dd17d55d2fd512c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468575"
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>Propriétés du compte de proxy - Nouveau compte de proxy (page Général)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Dans [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la plupart, mais pas toutes les fonctionnalités SQL Server Agent sont actuellement prises en charge. Pour plus d’informations, consultez [Différences T-SQL entre Azure SQL Managed Instance et SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Utilisez cette page pour afficher et changer les propriétés d’un compte proxy [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Options  
**Nom du proxy**  
Tapez le nom du proxy.  
  
**Nom des informations d’identification**  
Tapez le nom des informations d'identification du proxy.  
  
> [!NOTE]  
> Le nom des informations d'identification spécifié doit correspondre à des informations d'identification existantes. Pour obtenir des informations sur la création d’informations d’identification, consultez [Procédure : Créer un proxy](https://msdn.microsoft.com/c1e77e91-2a69-40d9-b8b3-97cffc710586)  
  
**...**  
Affiche la boîte de dialogue **Sélectionner les informations d'identification** .  
  
**Description**  
Tapez la description du proxy.  
  
**Actif pour les sous-systèmes suivants**  
Sélectionnez les sous-systèmes auxquels le compte de proxy a accès.  
  
**Réaffecter les étapes du travail à**  
Sélectionnez le proxy auquel réaffecter les étapes du travail. Cette liste est activée lorsque vous révoquez l'accès à un sous-système auquel le proxy avait accès auparavant.  
  
## <a name="see-also"></a>Voir aussi  
[Create a SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
