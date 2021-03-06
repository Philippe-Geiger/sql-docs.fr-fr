---
title: SqlDataRecord, objet | Microsoft Docs
description: Dans SQL Server l’intégration du CLR, les procédures stockées peuvent utiliser la classe SqlDataRecord pour envoyer des jeux de résultats personnalisés au client.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlDataRecord object
- custom result sets [CLR integration]
ms.assetid: 2ed667fb-749c-4280-a8fb-650643683c8f
author: rothja
ms.author: jroth
ms.openlocfilehash: da1735c17a4d87e085fbe1e8b5f960d14a70b86c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765429"
---
# <a name="sqldatarecord-object"></a>Objet SqlDataRecord
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'objet **SqlDataRecord** représente une ligne unique de données avec ses métadonnées connexes.  
  
 Les procédures stockées managées peuvent envoyer au client des jeux de résultats clients qui ne proviennent pas d'un **SqlDataReader**. La classe **SqlDataRecord** , avec les méthodes **SendResultsStart**, **SendResultsRow**et **SendResultsEnd** de l'objet **SqlPipe** , permet aux procédures stockées d'envoyer des jeux de résultats personnalisés au client.  
  
 Pour plus d'informations, consultez la documentation de référence sur la classe **Microsoft.SqlServer.Server.SqlDataRecord** dans la documentation du Kit de développement logiciel (SDK) .NET Framework.  
  
## <a name="example"></a>Exemple  
 L'exemple suivant crée un nouvel enregistrement d'employé et le retourne à l'appelant.  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void CreateNewRecordProc()  
{  
    // Variables.         
    SqlDataRecord record;  
  
    // Create a new record with the column metadata.  The constructor   
    // is able to accept a variable number of parameters.  
    record = new SqlDataRecord(new SqlMetaData("EmployeeID", SqlDbType.Int),  
                               new SqlMetaData("Surname", SqlDbType.NVarChar, 20),  
                               new SqlMetaData("GivenName", SqlDbType.NVarChar, 20),  
                               new SqlMetaData("StartDate", SqlDbType.DateTime) );  
  
    // Set the record fields.  
    record.SetInt32(0, 0042);  
    record.SetString(1, "Funk");  
    record.SetString(2, "Don");  
    record.SetDateTime(3, new DateTime(2005, 7, 17));  
  
    // Send the record to the calling program.  
    SqlContext.Pipe.Send(record);  
  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  CreateNewRecordVBProc ()  
    ' Variables.  
    Dim record As SqlDataRecord  
  
    ' Create a new record with the column metadata. The constructor is   
    ' able to accept a variable number of parameters  
  
    record = New SqlDataRecord(New SqlMetaData("EmployeeID", SqlDbType.Int), _  
                           New SqlMetaData("Surname", SqlDbType.NVarChar, 20), _  
                           New SqlMetaData("GivenName", SqlDbType.NVarChar, 20), _  
                           New SqlMetaData("StartDate", SqlDbType.DateTime))  
  
    ' Set the record fields.  
    record.SetInt32(0, 42)  
    record.SetString(1, "Funk")  
    record.SetString(2, "Don")  
    record.SetDateTime(3, New DateTime(2005, 7, 17))  
  
    ' Send the record to the calling program.  
    SqlContext.Pipe.Send(record)  
  
End Sub  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Objet SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)  
  
  
