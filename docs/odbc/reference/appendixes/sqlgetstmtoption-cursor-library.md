---
description: SQLGetStmtOption (bibliothèque de curseurs)
title: SQLGetStmtOption (bibliothèque de curseurs) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Cursor Library
ms.assetid: 986170b3-fba8-4323-9224-60b381c7effb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 93a1e34648d1cef320ca7385eb24215701ed9dd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411105"
---
# <a name="sqlgetstmtoption-cursor-library"></a>SQLGetStmtOption (bibliothèque de curseurs)
> [!IMPORTANT]  
>  Cette fonctionnalité sera supprimée dans une future version de Windows. Évitez d’utiliser cette fonctionnalité dans de nouveaux travaux de développement et prévoyez de modifier les applications qui utilisent actuellement cette fonctionnalité. Microsoft recommande l’utilisation de la fonctionnalité de curseur du pilote.  
  
 Cette rubrique traite de l’utilisation de la fonction **SQLGetStmtOption** dans la bibliothèque de curseurs. Pour obtenir des informations générales sur **SQLGetStmtOption**, consultez [fonction SQLGetStmtOption](../../../odbc/reference/syntax/sqlgetstmtoption-function.md).  
  
 La bibliothèque de curseurs prend en charge les options d’instruction suivantes avec **SQLGetStmtOption**:  

:::row:::
    :::column:::
        SQL_BIND_TYPE  
        SQL_CONCURRENCY  
        SQL_CURSOR_TYPE  
        SQL_GET_BOOKMARK  
    :::column-end:::
    :::column:::
        SQL_ROW_NUMBER  
        SQL_ROWSET_SIZE  
        SQL_SIMULATE_CURSOR  
    :::column-end:::
:::row-end:::
