---
title: référence d’API du pilote SQLSRV
description: Les informations de référence sur l’API pour le pilote SQLSRV pour PHP décrivent les fonctions disponibles, leurs paramètres et les valeurs de retour.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0b55da26-ddeb-4e89-872a-91e0aba57103
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01dfb59cd433a545efbe7376fd369c897ee4f693
ms.sourcegitcommit: b2ab989264dd9d23c184f43fff2ec8966793a727
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381073"
---
# <a name="sqlsrv-driver-api-reference"></a>référence d’API du pilote SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Le nom de l’API pour le pilote SQLSRV dans [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] est **sqlsrv**. Tous les fonctions **sqlsrv** commencent par **sqlsrv_** et sont suivies d’un verbe ou d’un nom. Celles qui sont suivies d’un verbe effectuent une action tandis que celles qui sont suivies d’un substantif retournent des métadonnées.  
  
## <a name="in-this-section"></a>Dans cette section  
Le pilote SQLSRV contient les fonctions suivantes :  
  
|Fonction|Description|  
|------------|---------------|  
|[sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)|Commence une transaction.|  
|[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)|Annule une instruction ; ignore les résultats en attente de l’instruction.|  
|[sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)|Fournit des informations sur le client.|  
|[sqlsrv_close](../../connect/php/sqlsrv-close.md)|Ferme une connexion. Libère toutes les ressources associées à la connexion.|  
|[sqlsrv_commit](../../connect/php/sqlsrv-commit.md)|Valide une transaction.|  
|[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)|Modifie la gestion des erreurs et les configurations de journalisation.|  
|[sqlsrv_connect](../../connect/php/sqlsrv-connect.md)|Crée et ouvre une connexion.|  
|[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)|Retourne des informations d’erreur et/ou d’avertissement sur la dernière opération.|  
|[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)|Exécute une instruction préparée.|  
|[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)|Rend la ligne suivante de données disponible pour la lecture.|  
|[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)|Récupère la ligne suivante de données sous la forme d’un tableau indexé numériquement, de tableau associatif ou les deux.|  
|[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)|Récupère la ligne suivante de données sous la forme d’un objet.|  
|[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)|Retourne les métadonnées de champ.|  
|[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)|Ferme une instruction. Libère toutes les ressources associées à l’instruction.|  
|[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)|Retourne la valeur du paramètre de configuration spécifié.|  
|[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)|Récupère un champ dans la ligne actuelle par index. Le type de retour PHP peut être spécifié.|  
|[sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md)|Détecte si un jeu de résultats comporte une ou plusieurs lignes.|  
|[sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)|Rend le résultat suivant disponible pour le traitement.|  
|[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)|Indique le nombre de lignes dans un jeu de résultats.|  
|[sqlsrv_num_fields](../../connect/php/sqlsrv-num-fields.md)|Récupère le nombre de champs dans un jeu de résultats actif.|  
|[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)|Prépare une requête Transact-SQL sans l’exécuter. Lie implicitement des paramètres.|  
|[sqlsrv_query](../../connect/php/sqlsrv-query.md)|Prépare et exécute une requête Transact-SQL.|  
|[sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)|Restaure une transaction.|  
|[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)|Retourne le nombre de lignes modifiées.|  
|[sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)|Envoie jusqu’à huit kilo-octets (8 Ko) de données au serveur à chaque appel à la fonction.|  
|[sqlsrv_server_info](../../connect/php/sqlsrv-server-info.md)|Fournit des informations sur le serveur.|  
  
## <a name="reference"></a>Informations de référence  
[Manuel PHP](https://php.net/manual)  
  
## <a name="see-also"></a>Voir aussi  
[Vue d’ensemble de Microsoft Drivers for PHP for SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)

[Constantes &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Guide de programmation pour les pilotes Microsoft pour PHP pour SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Bien démarrer avec les pilotes Microsoft pour PHP pour SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)
  
