---
title: 'Accéder aux données externes : Oracle - PolyBase'
description: Cet article montre comment utiliser PolyBase pour créer une source de données externes afin d’accéder aux données Oracle.
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 322c858a9b20548662136e395c0db1c76171f5fd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85740957"
---
# <a name="configure-polybase-to-access-external-data-in-oracled"></a>Configurer PolyBase pour accéder à des données externes dans Oracle

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

L’article explique comment utiliser PolyBase sur une instance SQL Server pour interroger des données externes dans Oracle.

## <a name="prerequisites"></a>Prérequis

Si vous n’avez pas installé PolyBase, consultez [Installation de PolyBase](polybase-installation.md).

  La [clé principale](../../t-sql/statements/create-master-key-transact-sql.md) doit être créée avant les informations d’identification incluses dans l’étendue de la base de données. 

## <a name="configure-an-oracle-external-data-source"></a>Configurer une source de données externes Oracle

Pour interroger les données d’une source de données Oracle, vous devez créer des tables externes pour référencer les données externes. Cette section fournit un exemple de code pour créer ces tables externes.

Les commandes Transact-SQL suivantes sont utilisées dans cette section :

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)


1. Créez des informations d’identification incluses dans l’étendue de la base de données pour accéder à la source Oracle.

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```

1. Créez une source de données externe avec [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    /* 
    * LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    * PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    * CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = 'oracle://<server address>[:<port>]',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_name)
    ```

1. **Facultatif :** Créez des statistiques sur une table externe.

    Pour des performances de requêtes optimales, nous vous recommandons de créer des statistiques sur les colonnes de table externe, en particulier celles utilisées pour les jointures, les filtres et les agrégats.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>Une fois que vous avez créé une source de données externes, vous pouvez utiliser la commande [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) afin de créer une table requêtable sur cette source. 

Pour plus d’informations et pour obtenir des exemples, consultez les articles suivants :

- [CRÉER UNE TABLE EXTERNE](../../t-sql/statements/create-external-table-transact-sql.md).
- [Vue d’ensemble de Polybase SQL Server](polybase-guide.md).
