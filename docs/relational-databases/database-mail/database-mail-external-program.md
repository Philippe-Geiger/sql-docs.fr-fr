---
description: Programme externe de la messagerie de base de données
title: Programme externe de la messagerie de base de données | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- external programs [Database Mail]
- DatabaseMail90.exe
- Database Mail [SQL Server], external programs
ms.assetid: bc124164-eb6e-4b7f-bf66-98a3113d02f7
author: stevestein
ms.author: sstein
ms.openlocfilehash: e8d609ec57f47cf3df061f286bd663c0a8431047
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465451"
---
# <a name="database-mail-external-program"></a>Programme externe de la messagerie de base de données
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   L’exécutable externe de la messagerie de base de données est **DatabaseMail.exe**, situé dans le **répertoire MSSQL\Binn** de l’installation [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La messagerie de base de données utilise l'activation Service Broker pour démarrer le programme externe lorsque des messages électroniques doivent être traités. La messagerie de base de données démarre une instance du programme externe. Le programme externe s'exécute dans le contexte de sécurité du compte de services pour [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Dans cette rubrique :**  
  
-   [Concepts du programme externe de la messagerie de base de données](#ComponentsAndConcepts)  
  
-   [Tâches liées à la configuration du programme externe de messagerie de base de données](#RelatedTasks)  
  
##  <a name="database-mail-external-program-concepts"></a><a name="ComponentsAndConcepts"></a> Concepts du programme externe de la messagerie de base de données  
 Lorsque le programme externe démarre, il se connecte à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à l'aide de l'authentification Windows et débute le traitement des messages électroniques. S'il n'y a eu aucun message à envoyer pendant le délai d'attente spécifié, le programme est fermé. Vous pouvez configurer la durée du délai d'attente du programme avant qu'il ne soit fermé en utilisant soit l'Assistant Configuration de la messagerie de base de données, soit les procédures stockées de la messagerie de base de données. Pour plus d’informations, consultez [sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md).  
  
 Le programme externe stocke les informations dans les tables système de la base de données **msdb** . Si le programme externe ne peut pas communiquer avec [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il consigne des erreurs dans le journal des événements des applications Microsoft Windows. Une journalisation supplémentaire des messages est assurée si vous définissez le niveau de journalisation à **Commentaires** dans la boîte de dialogue **Configurer les paramètres du système** de l' **Assistant Configuration de la messagerie de base de données**.  
  
 Notez que, pour des raisons d'efficacité, le programme externe met en cache les informations de compte et de profil. Les changements de configuration des comptes et profils peuvent donc ne pas être pris en compte dans le programme externe avant quelques minutes.  
  
##  <a name="tasks-related-to-configuring-database-mail-external-program"></a><a name="RelatedTasks"></a> Tâches liées à la configuration du programme externe de messagerie de base de données  
  
|Tâche de configuration|Lien de rubrique|  
|------------------------|----------------|  
|Spécifiez l'heure à laquelle le programme externe s'arrête.|[sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)|  
  
## <a name="see-also"></a>Voir aussi  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Journal et audits de la messagerie de base de données](../../relational-databases/database-mail/database-mail-log-and-audits.md)   
 [Messagerie de base de données](../../relational-databases/database-mail/database-mail.md)  
  
  
