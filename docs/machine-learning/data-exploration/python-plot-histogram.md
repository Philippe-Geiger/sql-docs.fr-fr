---
title: Création d’un histogramme pour l’exploration de données avec Python
titleSuffix: SQL machine learning
description: Découvrez comment créer un histogramme pour visualiser les données avec Python.
author: cawrites
ms.author: chadam
ms.date: 07/14/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: 1a946efdd8da5a64d2475164a1b8057c7b41554f
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91226831"
---
# <a name="plot-histograms-in-python"></a>Création d’histogrammes en Python 
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Cet article explique comment représenter des données sous forme graphique à l’aide du package Python [Pandas hist()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.hist.html). Une base de données SQL est la source utilisée pour visualiser les intervalles de données d’histogramme dont les valeurs sont consécutives et ne se chevauchent pas.

## <a name="prerequisites"></a>Configuration requise :

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* Serveur SQL Server. Pour savoir comment l’installer, consultez [SQL Server pour Windows](../../database-engine/install-windows/install-sql-server.md) ou [pour Linux](../../linux/sql-server-linux-overview.md).
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
* Azure SQL Database. Pour savoir comment s’inscrire, consultez [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Azure SQL Managed Instance. Pour savoir comment s’inscrire, consultez [Azure SQL Managed Instance](https://docs.microsoft.com/azure/azure-sql/managed-instance/instance-create-quickstart).

* [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) pour restaurer l’exemple de base de données sur Azure SQL Managed Instance.
::: moniker-end

* Azure Data Studio. Pour savoir comment l’installer, consultez [Azure Data Studio](../../azure-data-studio/what-is.md).

* [Exemple de restauration de base de données DW](../../samples/adventureworks-install-configure.md) pour obtenir les exemples de données utilisés dans cet article.

## <a name="verify-restored-database"></a>Vérification de la base de données restaurée

Vous pouvez vérifier que la base de données restaurée existe en interrogeant la table **Person.CountryRegion** :
```sql
USE AdventureWorksDW;
SELECT * FROM Person.CountryRegion;
```
  
## <a name="install-python-packages"></a>Installer des packages Python

[Téléchargez et installez Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md).

Installez les packages Python suivants :
  * pyodbc
  * pandas

  Pour installer ces packages :

  1. Dans votre notebook Azure Data Studio, sélectionnez **Gérer les packages**.
  2. Dans le volet **Gérer les packages**, sélectionnez l’onglet **Ajouter nouveau**.
  3. Pour chacun des packages suivants, entrez le nom du package, cliquez sur **Rechercher**, puis cliquez sur **Installer**.

## <a name="plot-histogram"></a>Création de l’histogramme

Les données distribuées affichées dans l’histogramme s’appuient sur une requête SQL d’AdventureWorksDW. L’histogramme permet de visualiser les données et la fréquence des valeurs de données. Modifiez les variables de chaîne de connexion « server », « database », « username » et « password » pour la connexion à la base de données SQL.

Pour créer un bloc-notes :

1. Dans Azure Data Studio, sélectionnez **Fichier**, puis **Nouveau notebook**.
2. Dans le notebook, sélectionnez le noyau **Python3**, puis **+code**.
3. Collez le code dans le notebook, puis sélectionnez **Tout exécuter**.

```python
import pyodbc 
import pandas as plt
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'servername' 
database = 'AdventureWorksDW' 
username = 'yourusername' 
password = 'databasename'  
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
sql = "SELECT DATEDIFF(year, c.BirthDate, GETDATE()) AS Age FROM [dbo].[FactInternetSales] s INNER JOIN dbo.DimCustomer c ON s.CustomerKey = c.CustomerKey"
df = pd.read_sql(sql, cnxn)
df.hist(bins=10)
```

L’affichage présente la distribution de l’âge des clients dans la table FactInternetSales.

![Histogramme Pandas](./media/python-histogram.png)


