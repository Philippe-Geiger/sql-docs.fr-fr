---
description: Importer un fichier BACPAC pour créer une nouvelle base de données utilisateur
title: Importer un fichier BACPAC pour créer une base de données utilisateur
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb. importdac.results.f1
- sql13.swb.importdac.settings.f1
- sql13.swb.importdac.storagebrowser.f1
- sql13.swb.importdac.results.f1
- sql13.swb.importdac.progress.f1
- sql13.swb. importdac.summary.f1
- sql13.swb.importdac.summary.f1
- sql13.swb. importdac.progress.f1
- sql13.swb.importdac.welcome.f1
- sql13.swb. importdac.settings.f1
helpviewer_keywords:
- Data-tier application
- SQL Server DAC
- Migrate database
- DAC
ms.assetid: 736d8d9a-39f1-4bf8-b81f-2e56c134d12e
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5e02041dd6801f5ab0b819f4bffd91ca8ba38e8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412435"
---
# <a name="import-a-bacpac-file-to-create-a-new-user-database"></a>Importer un fichier BACPAC pour créer une nouvelle base de données utilisateur
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Importez un fichier d’application de couche Données (DAC), fichier portant l’extension .bacpac, pour créer une copie de la base de données d’origine, avec ses données, sur une nouvelle instance du [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou vers [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Les opérations d’exportation-importation peuvent être combinées pour migrer une DAC ou une base de données entre différentes instances, ou pour créer une sauvegarde logique, telles qu’une copie sur site d’une base de données déployée dans [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
## <a name="before-you-begin"></a>Avant de commencer  
 L'importation génère une nouvelle DAC en deux étapes.  
  
1.  L'importation crée la nouvelle DAC et la base de données associée à l'aide de la définition de la DAC stockée dans le fichier d'exportation de la même manière que le déploiement de la DAC crée la nouvelle DAC à partir de la définition dans un fichier de package DAC.  
  
2.  L'importation copie en bloc les données du fichier d'exportation.  

## <a name="sql-server-utility"></a>Utilitaire SQL Server  
 Si vous importez une DAC dans une instance du moteur de base de données, la DAC importée est incorporée dans l’Utilitaire SQL Server quand le jeu d’éléments de collecte de l’utilitaire est envoyé de l’instance au point de contrôle de l’utilitaire. La DAC est ensuite présente dans le nœud **Application de la couche Données déployée** au sein de l’**Explorateur d’utilitaire** [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] et est signalée dans la page de détails pour **Application de la couche Données déployée**.  
  
## <a name="database-options-and-settings"></a>Options et paramètres de bases de données  
 Par défaut, la base de données créée pendant l'importation aura tous les paramètres par défaut de l'instruction CREATE DATABASE, mais le classement de base de données et le niveau de compatibilité sont définis en fonction des valeurs définies dans le fichier d'exportation DAC. Un fichier d'exportation DAC utilise les valeurs de la base de données d'origine.  
  
 Certaines options de base de données, telles que TRUSTWORTHY, DB_CHAINING et HONOR_BROKER_PRIORITY, ne peuvent pas être ajustées dans le cadre du processus d'importation. Des propriétés physiques, telles que le nombre de groupes de fichiers ou le nombre et la taille des fichiers, ne peuvent pas être modifiées dans le cadre du processus d'importation. Une fois l'importation terminée, vous pouvez utiliser l'instruction ALTER DATABASE, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell pour personnaliser la base de données. Pour plus d'informations, consultez [Databases](../../relational-databases/databases/databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitations et restrictions  
 Une DAC peut être importée vers [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ou une instance du [!INCLUDE[ssDE](../../includes/ssde-md.md)] qui exécute [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) ou une version ultérieure. Si vous exportez une DAC d'une version ultérieure, elle peut contenir des objets non pris en charge par [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Vous ne pouvez pas déployer ces DAC vers les instances de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="prerequisites"></a>Conditions préalables  
 Nous vous recommandons de ne pas importer de fichier d'exportation DAC provenant de sources inconnues ou non approuvées. De tels fichiers peuvent contenir du code malveillant susceptible d'exécuter un code Transact-SQL indésirable ou de provoquer des erreurs en modifiant le schéma. Avant d'utiliser un fichier d'exportation provenant d'une source inconnue ou non approuvée, décompressez la DAC et vérifiez le code, par exemple les procédures stockées ou un autre code défini par l'utilisateur. Pour plus d'informations sur la façon de procéder à ces vérifications, consultez [Validate a DAC Package](validate-a-dac-package.md).  
  
## <a name="security"></a>Sécurité  
 Pour améliorer la sécurité, les connexions d'authentification SQL Server sont stockées dans un fichier d'exportation DAC sans mot de passe. Lorsque le fichier est importé, la connexion est créée en tant que connexion désactivée avec un mot de passe généré. Pour activer les connexions, connectez-vous à l’aide d’une connexion qui possède l’autorisation ALTER ANY LOGIN et utilisez ALTER LOGIN pour activer la connexion et affecter un nouveau mot de passe pouvant être communiqué à l’utilisateur. Cela n'est pas nécessaire pour les connexions d'authentification Windows car leurs mots de passe ne sont pas gérés par SQL Server.  
  
## <a name="permissions"></a>Autorisations  
 Une DAC ne peut être importée que par les membres des rôles serveur fixes **sysadmin** ou **serveradmin** , ou par les connexions figurant dans le rôle serveur fixe **dbcreator** et disposant d'autorisations ALTER ANY LOGIN. Le compte d’administrateur système [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intégré nommé **sa** peut également importer une DAC. L'importation d'une DAC avec des connexions à [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requiert l'appartenance aux rôles loginmanager ou serveradmin. L'importation d'une DAC sans connexions à [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requiert l'appartenance aux rôles dbmanager ou serveradmin.  
  
## <a name="using-the-import-data-tier-application-wizard"></a>Utilisation de l'Assistant Importation d'application de la couche Données  
 **Pour lancer l'Assistant, suivez les étapes suivantes :**  
  
1.  Connectez-vous à l’instance de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sur site ou dans [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
2.  Dans l’ **Explorateur d’objets**, cliquez avec le bouton droit sur **Bases de données**, puis sélectionnez l’option de menu **Importer une application de la couche Données** pour lancer l’Assistant.  
  
3.  Renseignez les boîtes de dialogue de l'Assistant :  
  
    -   [Page Introduction](#Introduction)  
  
    -   [Page Paramètres d'importation](#Import_settings)  
  
    -   [Page Paramètres de base de données](#Database_settings)  
  
    -   [Page Résumé](#Summary)  
  
    -   [Page Progression](#Progress)  
  
    -   [Page Résultats](#Results)  
  
###  <a name="introduction-page"></a><a name="Introduction"></a> Page Introduction  
 Cette page décrit les étapes de l'Assistant Importer l'application de la couche Données.  
  
 **Options**  
  
-   **Ne plus afficher cette page.** - Activez la case à cocher pour ne plus afficher la page Introduction à l'avenir.  
  
-   **Suivant** : passe à la page **Paramètres d’importation**.  
  
-   **Annuler** : annule l’opération et ferme l’Assistant.  
  
###  <a name="import-settings-page"></a><a name="Import_settings"></a> Page Paramètres d'importation  
 Utilisez cette page pour spécifier l'emplacement du fichier .bacpac à importer.  
  
-   **Importer à partir du disque local** : cliquez sur **Parcourir...** pour explorer l’ordinateur local, ou entrez le chemin d’accès dans la zone réservée à cet effet. Le chemin d'accès doit inclure un nom de fichier et l'extension .bacpac.  
  
-   **Importer à partir d’Azure** : importe un fichier BACPAC à partir d’un conteneur Microsoft Azure. Vous devez vous connecter à un conteneur Microsoft Azure afin de valider cette option. Notez que l’option Importer à partir d’Azure requiert également que vous spécifiiez un répertoire local pour le fichier temporaire. Le fichier temporaire est créé à l'emplacement spécifié et reste à cet endroit une fois l'opération terminée.  
  
     Lorsque vous parcourez Azure, vous pouvez basculer entre les conteneurs au sein d’un seul compte. Vous devez spécifier un seul fichier .bacpac pour continuer l'opération d'importation. Vous pouvez trier les colonnes par **Nom**, **Taille**ou **Date de modification**.  
  
     Pour continuer, spécifiez le fichier .bacpac à importer, puis cliquez sur **Ouvrir**.  
  
###  <a name="database-settings-page"></a><a name="Database_settings"></a> Page Paramètres de base de données  
 Utilisez cette page pour spécifier les détails de la base de données à créer.  
  
 **Pour une instance SQL Server locale :**  
  
-   **Nouveau nom de la base de données** : fournissez un nom pour la base de données importée.  
  
-   **Chemin d’accès du fichier de données** : fournissez un répertoire local pour les fichiers de données. Cliquez sur **Parcourir...** pour explorer l’ordinateur local, ou spécifiez le chemin d’accès dans l’espace fourni.  
  
-   **Chemin d’accès du fichier journal** : spécifiez un répertoire local pour les fichiers journaux. Cliquez sur **Parcourir...** pour explorer l’ordinateur local, ou spécifiez le chemin d’accès dans l’espace fourni.  
  
 Pour continuer, cliquez sur **Suivant**.  
  
 **Base de données SQL Azure :**  
  
 - **[Importer un fichier BACPAC pour créer une nouvelle base de données SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-import/)** fournit des instructions étape par étape relatives à l’utilisation du portail Azure, de PowerShell, de SSMS ou de SqlPackage.  
 - Consultez **[Options et performances de la base de données SQL : comprendre ce qui est disponible dans chaque niveau de service](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)** pour obtenir plus de détails sur les différents niveaux de service.  

### <a name="validation-page"></a>Page Validation  
 Utilisez cette page pour passer en revue tous les problèmes qui empêchent l'opération. Pour continuer, résolvez les problèmes bloquants, puis cliquez sur **Réexécuter la validation** pour vous assurer que la validation est réussie.  
  
 Pour continuer, cliquez sur **Suivant**.  
  
###  <a name="summary-page"></a><a name="Summary"></a> Page Résumé  
 Utilisez cette page pour passer en revue la source spécifiée et les paramètres cibles de l'opération. Pour terminer l'opération d'importation en utilisant les paramètres spécifiés, cliquez sur **Terminer**. Pour annuler l'opération d'importation et quitter l'Assistant, cliquez sur **Annuler**.  
  
###  <a name="progress-page"></a><a name="Progress"></a> Page Progression  
 Cette page affiche une barre de progression indiquant l'état de l'opération. Pour afficher l'état détaillé, cliquez sur l'option **Afficher les détails** .  
  
 Pour continuer, cliquez sur **Suivant**.  
  
###  <a name="results-page"></a><a name="Results"></a> Page Résultats  
 Cette page signale la réussite ou l'échec de l'importation et crée des opérations de base de données, affichant le succès ou l'échec de chacune. Toute action pour laquelle une erreur s'est produite aura un lien dans la colonne **Résultat** . Cliquez sur le lien pour consulter le rapport d'erreur de cette action.  
  
 Cliquez sur **Fermer** pour fermer l’assistant.  
  
## <a name="see-also"></a>Voir aussi  
[Importer un fichier BACPAC pour créer une nouvelle base de données Azure SQL](https://azure.microsoft.com/documentation/articles/sql-database-import/)  
 [Applications de la couche Données](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Exporter une application de la couche Données](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)  
  
  
