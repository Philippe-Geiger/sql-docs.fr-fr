---
description: Curseurs (SQL Server)
title: Curseurs (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- results [SQL Server], cursors
- Transact-SQL cursors, about cursors
- cursors [SQL Server]
- data access [SQL Server], cursors
- result sets [SQL Server], cursors
- requesting cursors
- cursors [SQL Server], about cursors
ms.assetid: e668b40c-bd4d-4415-850d-20fc4872ee72
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a26ba9a6d321de5b13277e52829286a4f3cfe13d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465493"
---
# <a name="sql-server-cursors"></a>Curseurs SQL Server
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
  Les opérations réalisées dans une base de données relationnelle s'exécutent sur un ensemble complet de lignes. Par exemple, l’ensemble de lignes retourné par une instruction `SELECT` contient toutes les lignes satisfaisant aux conditions de la clause `WHERE` de l’instruction. Cet ensemble complet de lignes retournées par l'instruction est appelé ensemble de résultats. Les applications, en particulier les applications interactives en ligne, peuvent ne pas toujours fonctionner efficacement si l'ensemble de résultats est traité comme une unité. Ces applications ont besoin d'un mécanisme leur permettant de travailler avec une seule ligne ou avec un petit bloc de lignes à la fois. Les curseurs sont une extension des ensembles de résultats et fournissent ce mécanisme.  
  
 Les curseurs permettent l'extension du traitement des résultats en procédant aux opérations suivantes :  
  
-   Ils permettent de vous positionner sur des lignes spécifiques de l'ensemble de résultats.  
  
-   Ils extraient une ligne ou un bloc de lignes à partir de la position actuelle dans l'ensemble de résultats.  
  
-   Ils prennent en charge les modifications de données apportées aux lignes à la position actuelle dans l'ensemble de résultats.  
  
-   Ils prennent en charge différents niveaux de visibilité des modifications apportées par d'autres utilisateurs aux données de la base de données qui figurent dans l'ensemble de résultats.  
  
-   Ils permettent aux instructions [!INCLUDE[tsql](../includes/tsql-md.md)] figurant dans les scripts, les procédures stockées et les déclencheurs d'accéder aux données d'un ensemble de résultats.  
  
> [!TIP]
> Dans certains scénarios, s’il existe une clé primaire sur une table, il est possible d’utiliser une boucle `WHILE` à la place d’un curseur, sans supporter la charge d’un curseur.
> Cependant, dans certains scénarios, les curseurs ne sont pas seulement inévitables, ils sont bel et bien obligatoires. Dans ce cas, s’il n’y aucune nécessité de mettre à jour les tables basées sur le curseur, utilisez des curseurs *firehose*, c’est-à-dire des curseurs [avant uniquement et en lecture seule](#forward-only).
  
## <a name="cursor-implementations"></a>Implémentations des curseurs  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] prend en charge trois implémentations de curseurs.  
  
### <a name="transact-sql-cursors"></a>curseurs Transact-SQL  
Les curseurs [!INCLUDE[tsql](../includes/tsql-md.md)] sont basés sur la syntaxe `DECLARE CURSOR` et sont utilisés principalement dans les déclencheurs, les procédures stockées et les scripts [!INCLUDE[tsql](../includes/tsql-md.md)]. [!INCLUDE[tsql](../includes/tsql-md.md)] Les curseurs sont implémentés sur le serveur et sont gérés par des instructions [!INCLUDE[tsql](../includes/tsql-md.md)] envoyées du client au serveur. Ils peuvent également être contenus dans des traitements, des procédures stockées ou des déclencheurs.  
  
### <a name="application-programming-interface-api-server-cursors"></a>Curseurs de serveur d'API (Application Programming Interface)  
Les curseurs d’API prennent en charge les fonctions de curseur d’API comme OLE DB et ODBC. Les curseurs de serveur d'API sont implémentés sur le serveur. Chaque fois qu’une application cliente appelle une fonction de curseur d’API, le fournisseur OLE DB de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ou le pilote ODBC transmet la demande au serveur afin d’appliquer une action au curseur côté serveur d’API.  
  
### <a name="client-cursors"></a>Curseurs clients  
Les curseurs clients sont implémentés en interne par le pilote ODBC [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client et par la DLL qui implémente l’API ADO. Les curseurs clients sont implémentés par la mise en mémoire cache sur le client de toutes les lignes de l'ensemble de résultats. Chaque fois qu’une application cliente appelle une fonction de curseur d’API, le pilote ODBC de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ou la DLL ADO exécute l’opération de curseur sur les lignes du jeu de résultats mises en cache sur le client.  
  
## <a name="type-of-cursors"></a>Type de curseur  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] prend en charge quatre types de curseur. 

> [!NOTE]
> Les curseurs peuvent tirer parti des tables de travail tempdb. Tout comme les opérations d’agrégation ou de tri en dépassement, ils engendrent des E/S et peuvent constituer un goulot d’étranglement qui nuisent aux performances. Les curseurs `STATIC` utilisent des tables de travail dès leur création. Pour plus d’informations, consultez [Tables de travail dans le Guide d’architecture de traitement des requêtes](../relational-databases/query-processing-architecture-guide.md#worktables).

### <a name="forward-only"></a>Curseur avant uniquement  
Un curseur avant uniquement est spécifié avec `FORWARD_ONLY` et `READ_ONLY` et ne prend pas en charge le défilement. Ces curseurs sont aussi appelés *firehose* et prennent en charge uniquement l’extraction des lignes en série du début jusqu’à la fin du curseur. Les lignes ne sont pas sorties de la base de données tant qu'elles n'ont pas été extraites. Les effets de toutes les instructions `INSERT`, `UPDATE` et `DELETE` émises par l’utilisateur actif ou validées par d’autres utilisateurs et ayant une incidence sur les lignes du jeu de résultats sont visibles à mesure que les lignes sont extraites à partir du curseur.  
  
 Étant donné que le curseur ne permet pas le défilement arrière, la plupart des modifications apportées aux lignes de la base de données après l'extraction d'une ligne ne sont pas visibles par le biais du curseur. En revanche, si une valeur utilisée pour déterminer l'emplacement de la ligne dans le jeu de résultats est modifiée, par exemple dans le cas de la mise à jour d'une colonne couverte par un index cluster, la valeur modifiée est visible à l'aide du curseur.  
  
 Les modèles de curseur d'API de base de données considèrent un curseur avant uniquement comme un type distinct de curseur, contrairement à [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] prend en compte les curseurs avant uniquement et de défilement en tant qu’options pouvant être appliquées aux curseurs statiques, de jeu de clés et dynamiques. [!INCLUDE[tsql](../includes/tsql-md.md)] Les curseurs prennent en charge les curseurs avant uniquement, statiques, de jeu de clés et dynamiques. Les modèles de curseurs d'API de bases de données supposent que les curseurs statiques, de jeux de clés et dynamiques permettent toujours le défilement. Lorsqu'un attribut ou une propriété de curseur d'API de bases de données est défini comme étant de type avant uniquement, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implémente ce curseur en tant que curseur dynamique avant uniquement.  
  
### <a name="static"></a>statique  
 Le jeu de résultats complet d’un curseur statique est créé dans **tempdb** à l’ouverture du curseur. Un curseur statique affiche toujours l'ensemble de résultats tel qu'il était au moment où le curseur a été ouvert. Les curseurs statiques détectent peu ou pas de modifications, mais consomment relativement peu de ressources pendant le défilement.  
  
Le curseur ne reflète pas les modifications de la base de données qui concernent soit l'appartenance de l'ensemble de résultats, soit les modifications apportées aux valeurs des colonnes des lignes constituant l'ensemble de résultats. Après son ouverture, un curseur statique n’affiche pas les nouvelles lignes insérées dans la base de données, même si celles-ci correspondent aux conditions de recherche de l'instruction `SELECT` du curseur. Si certaines lignes constituant l'ensemble de résultats sont mises à jour par d'autres utilisateurs, les nouvelles valeurs des données ne sont pas affichées dans le curseur statique. Le curseur statique affiche les lignes supprimées de la base de données après l'ouverture du curseur. Aucune opération `UPDATE`, `INSERT` ou `DELETE` n’apparaît dans un curseur statique (à moins qu’il soit fermé et rouvert), ni même les modifications effectuée en utilisant la même connexion que celle qui a ouvert le curseur.  
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Les curseurs statiques sont toujours en lecture seule.  
  
> [!NOTE]
> Étant donné que l’ensemble de résultats d’un curseur statique est stocké dans une table de travail de la base de données **tempdb**, la taille des lignes de l’ensemble de résultats ne peut pas dépasser la taille maximale des lignes d’une table [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> Pour plus d’informations, consultez [Tables de travail dans le Guide d’architecture de traitement des requêtes](../relational-databases/query-processing-architecture-guide.md#worktables). Pour plus d’informations sur la taille maximale des lignes, consultez [Spécifications des capacités maximales pour SQL Server](../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] utilise le terme INSENSITIVE pour désigner les curseurs statiques. Certaines API de bases de données les appellent curseurs d'instantané.  
  
### <a name="keyset"></a>Keyset  
L'appartenance et l'ordre des lignes d'un curseur de jeu de clés sont fixés au moment de l'ouverture du curseur. Les curseurs de jeux de clés sont gérés par un ensemble d'identificateurs uniques (clés) appelé jeu de clés. Les clés sont créées à partir d'un ensemble de colonnes qui identifient uniquement les lignes de l'ensemble de résultats. Le jeu de clés est l’ensemble des valeurs de clés de toutes les lignes remplissant les conditions requises par l’instruction `SELECT` au moment où le curseur a été ouvert. Le jeu de clés d’un curseur de jeux de clés est créé dans **tempdb** au moment de l’ouverture du curseur.  
  
### <a name="dynamic"></a>Dynamique  
Les curseurs dynamiques sont le contraire des curseurs statiques. Les curseurs dynamiques reflètent toutes les modifications apportées aux lignes de leur jeu de résultats lorsque vous les parcourez. Les valeurs des données, l'ordre et l'appartenance des lignes du jeu de résultats peuvent changer à chaque extraction. Toutes les instructions `UPDATE`, `INSERT` et `DELETE` émises par l’ensemble des utilisateurs sont visibles à l’aide du curseur. Les mises à jour sont visibles immédiatement si elles ont été effectuées à l’aide du curseur, soit au moyen d’une fonction API comme **SQLSetPos**, soit au moyen de la clause [!INCLUDE[tsql](../includes/tsql-md.md)] `WHERE CURRENT OF`. Les mises à jour effectuées en dehors du curseur ne sont pas visibles tant qu'elles n'ont pas été validées, à moins que le niveau d'isolement d'une transaction de curseur soit paramétré pour permettre la lecture des données non validées. Pour plus d’informations sur les niveaux d’isolement, consultez [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md). 
 
> [!NOTE]
> Les plans de curseur dynamique n'utilisent jamais d'index spatiaux.  
  
## <a name="requesting-a-cursor"></a>Demande de curseur  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] prend en charge deux méthodes de demande de curseur :  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]  
  
     Le langage [!INCLUDE[tsql](../includes/tsql-md.md)] prend en charge une syntaxe permettant l'utilisation de curseurs modélisés d'après la syntaxe de curseur ISO.  
  
-   Fonctions de curseur de l'interface de programmation d'application (API) de bases de données  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] prend en charge la fonctionnalité de curseur des API des bases de données suivantes :  
  
    -   ADO ([!INCLUDE[msCoName](../includes/msconame-md.md)] ActiveX Data Object)  
  
    -   OLE DB  
  
    -   ODBC (Open Database Connectivity)  
  
Une application ne doit jamais combiner ces deux méthodes de demande de curseur. Une application ayant utilisé l'API pour spécifier des comportements de curseur ne doit pas ensuite exécuter une instruction [!INCLUDE[tsql](../includes/tsql-md.md)] DECLARE CURSOR pour demander aussi un curseur [!INCLUDE[tsql](../includes/tsql-md.md)] . Une application ne doit exécuter une instruction DECLARE CURSOR que si elle a ramené tous les attributs de curseur de l'API à leurs valeurs par défaut.  
  
Dans le cas où ni un curseur [!INCLUDE[tsql](../includes/tsql-md.md)] , ni un curseur d'API n'a été demandé, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] retourne par défaut à l'application un ensemble de résultats complet, appelé ensemble de résultats par défaut.  
  
## <a name="cursor-process"></a>Processus des curseurs  
 [!INCLUDE[tsql](../includes/tsql-md.md)] Les curseurs et les curseurs d’API ont une syntaxe différente, mais le processus général suivant est utilisé avec tous les curseurs [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
1.  Associez un curseur à l'ensemble de résultats d'une instruction [!INCLUDE[tsql](../includes/tsql-md.md)] et définissez les caractéristiques du curseur, en indiquant par exemple si les lignes contenues dans le curseur peuvent être mises à jour.  
  
2.  Exécutez l'instruction [!INCLUDE[tsql](../includes/tsql-md.md)] pour remplir le curseur.  
  
3.  Dans le curseur que vous voulez afficher, extrayez les lignes. L'opération consistant à récupérer une ligne ou un bloc de lignes à partir d'un curseur est appelée une extraction. Le défilement est l'opération consistant à effectuer une série d'extractions afin d'extraire des lignes vers l'avant ou vers l'arrière.  
  
4.  Vous pouvez, si vous le souhaitez, effectuer des opérations de modification (mise à jour ou suppression) sur la ligne à la position actuelle du curseur.  
  
5.  Fermez le curseur.  
  
## <a name="related-content"></a>Contenu associé  
[Comportements des curseurs](../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)    
[Comment les curseurs sont implémentés](../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
## <a name="see-also"></a>Voir aussi  
[DECLARE CURSOR &#40;Transact-SQL&#41;](../t-sql/language-elements/declare-cursor-transact-sql.md)   
[Curseurs &#40;Transact-SQL&#41;](../t-sql/language-elements/cursors-transact-sql.md)   
[Fonctions de curseur &#40;Transact-SQL&#41;](../t-sql/functions/cursor-functions-transact-sql.md)   
[Procédures stockées de curseur &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)    

  
