---
title: 'Exemple : Construction de frères à l’aide du mode EXPLICIT | Microsoft Docs'
description: Visualisez un exemple d’une requête SQL qui utilise le mode EXPLICIT avec la clause FOR XML pour construire des frères XML.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- EXPLICIT FOR XML mode
ms.assetid: 8a57b765-a890-46a3-8b5f-5754e921ea6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e969fd0d003d44b3aaf97efad6e029d52e146dfa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633111"
---
# <a name="example-constructing-siblings-with-explicit-mode"></a>Exemple : Construction de frères à l’aide du mode EXPLICIT
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Supposons que vous souhaitiez construire un document XML qui fournit des informations sur les commandes. Les éléments <`SalesPerson`> et <`OrderDetail`> sont frères. Chaque commande possède un élément <`OrderHeader`>, un élément <`SalesPerson`> ainsi qu'un ou plusieurs éléments <`OrderDetail`>.  
  
```  
<OrderHeader SalesOrderID=... OrderDate=... CustomerID=... >  
  <SalesPerson SalesPersonID=... />  
  <OrderDetail SalesOrderID=... LineTotal=... ProductID=... OrderQty=... />  
  <OrderDetail SalesOrderID=... LineTotal=... ProductID=... OrderQty=.../>  
      ...  
</OrderHeader>  
<OrderHeader ...</OrderHeader>  
```  
  
 La requête en mode EXPLICIT suivante construit ce document XML. La requête spécifie les valeurs `Tag` 1 pour l'élément <`OrderHeader`>, 2 pour l'élément <`SalesPerson`> et 3 pour l'élément <`OrderDetail`>. Étant donné que <`SalesPerson`> et <`OrderDetail`> sont frères, la requête spécifie la même valeur de balise `Parent`, 1, pour identifier l'élément <`OrderHeader`>.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        SalesOrderID  as [OrderHeader!1!SalesOrderID],  
        OrderDate     as [OrderHeader!1!OrderDate],  
        CustomerID    as [OrderHeader!1!CustomerID],  
        NULL          as [SalesPerson!2!SalesPersonID],  
        NULL          as [OrderDetail!3!SalesOrderID],  
        NULL          as [OrderDetail!3!LineTotal],  
        NULL          as [OrderDetail!3!ProductID],  
        NULL          as [OrderDetail!3!OrderQty]  
FROM   Sales.SalesOrderHeader  
WHERE     SalesOrderID=43659 or SalesOrderID=43661  
UNION ALL   
SELECT 2 as Tag,  
       1 as Parent,  
        SalesOrderID,  
        NULL,  
        NULL,  
        SalesPersonID,    
        NULL,           
        NULL,           
        NULL,  
        NULL           
FROM   Sales.SalesOrderHeader  
WHERE     SalesOrderID=43659 or SalesOrderID=43661  
UNION ALL  
SELECT 3 as Tag,  
       1 as Parent,  
        SOD.SalesOrderID,  
        NULL,  
        NULL,  
        SalesPersonID,  
        SOH.SalesOrderID,  
        LineTotal,  
        ProductID,  
        OrderQty     
FROM    Sales.SalesOrderHeader SOH,Sales.SalesOrderDetail SOD  
WHERE   SOH.SalesOrderID = SOD.SalesOrderID  
AND     (SOH.SalesOrderID=43659 or SOH.SalesOrderID=43661)  
ORDER BY [OrderHeader!1!SalesOrderID], [SalesPerson!2!SalesPersonID],  
         [OrderDetail!3!SalesOrderID],[OrderDetail!3!LineTotal]  
FOR XML EXPLICIT;  
```  
  
 Voici le résultat partiel :  
  
```
<OrderHeader SalesOrderID="43659" OrderDate="2005-07-01T00:00:00" CustomerID="676">
  <SalesPerson SalesPersonID="279" />
  <OrderDetail SalesOrderID="43659" LineTotal="10.373000" ProductID="712" OrderQty="2" />
  <OrderDetail SalesOrderID="43659" LineTotal="28.840400" ProductID="716" OrderQty="1" />
  <OrderDetail SalesOrderID="43659" LineTotal="34.200000" ProductID="709" OrderQty="6" />
    ...
</OrderHeader>
<OrderHeader SalesOrderID="43661" OrderDate="2005-07-01T00:00:00" CustomerID="442">
  <SalesPerson SalesPersonID="282" />
  <OrderDetail SalesOrderID="43661" LineTotal="20.746000" ProductID="712" OrderQty="4" />
  <OrderDetail SalesOrderID="43661" LineTotal="40.373000" ProductID="711" OrderQty="2" />
  ...
</OrderHeader>
```
  
## <a name="see-also"></a>Voir aussi  
 [Utiliser le mode EXPLICIT avec FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
