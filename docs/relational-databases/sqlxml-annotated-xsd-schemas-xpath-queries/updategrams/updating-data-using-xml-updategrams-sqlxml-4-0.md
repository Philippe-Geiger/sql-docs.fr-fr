---
title: Mise à jour de données à l’aide de codes XML (SQLXML)
description: Découvrez comment mettre à jour des données existantes à l’aide d’un mise à jour XML dans SQLXML 4,0.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 01fd8e99d6eb770c2f5680ead1e2c4d9b9ec98b8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733656"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>Mise à jour de données à l'aide de codes de mise à jour (updategrams) XML (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Lorsque vous mettez à jour des données existantes, vous devez spécifier à la fois les **\<before>** **\<after>** blocs et. Les éléments spécifiés dans **\<before>** les **\<after>** blocs et décrivent la modification souhaitée. Le mise à jour utilise le ou les éléments spécifiés dans le **\<before>** bloc pour identifier les enregistrements existants dans la base de données. Le ou les éléments correspondants dans le **\<after>** bloc indiquent la manière dont les enregistrements doivent s’afficher après l’exécution de l’opération de mise à jour. À partir de ces informations, mise à jour crée une instruction SQL qui correspond au **\<after>** bloc. Le code de mise à jour (updategram) utilise ensuite cette instruction pour mettre à jour la base de données.  
  
 Voici le format du code de mise à jour (updategram) pour une opération de mise à jour :  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<updg:before>**  
 Les éléments du **\<before>** bloc identifient les enregistrements existants dans les tables de la base de données.  
  
 **\<updg:after>**  
 Les éléments du **\<after>** bloc décrivent comment les enregistrements spécifiés dans le **\<before>** bloc doivent apparaître après l’application des mises à jour.  
  
 L’attribut **mapping-schema** identifie le schéma de mappage qui doit être utilisé par le mise à jour. Si le mise à jour spécifie un schéma de mappage, les noms d’élément et d’attribut spécifiés dans les **\<before>** **\<after>** blocs et doivent correspondre aux noms du schéma. Le schéma de mappage mappe ces noms d'éléments ou d'attributs aux noms de tables et de colonnes de la base de données.  
  
 Si le code de mise à jour (updategram) ne spécifie pas de schéma, le mappage par défaut est utilisé. Dans le mappage par défaut, le **\<ElementName>** spécifié dans le mise à jour est mappé à la table de base de données et les éléments ou attributs enfants sont mappés aux colonnes de base de données.  
  
 Un élément du **\<before>** bloc doit correspondre à une seule ligne de table dans la base de données. Si l’élément correspond à plusieurs lignes de table ou ne correspond à aucune ligne de table, le mise à jour retourne une erreur et annule l’intégralité du **\<sync>** bloc.  
  
 Un mise à jour peut inclure plusieurs **\<sync>** blocs. Chaque **\<sync>** bloc est traité comme une transaction. Chaque **\<sync>** bloc peut avoir plusieurs **\<before>** **\<after>** blocs et. Par exemple, si vous mettez à jour deux des enregistrements existants, vous pouvez spécifier deux **\<before>** paires et **\<after>** , une pour chaque enregistrement en cours de mise à jour.  
  
## <a name="using-the-updgid-attribute"></a>Utilisation de l'attribut updg:id  
 Quand plusieurs éléments sont spécifiés dans **\<before>** les **\<after>** blocs et, utilisez l’attribut **attribut updg : ID** pour marquer les lignes dans les **\<before>** **\<after>** blocs et. La logique de traitement utilise ces informations pour déterminer quel enregistrement dans les **\<before>** paires de blocs avec quel enregistrement dans le **\<after>** bloc.  
  
 L’attribut **attribut updg : ID** n’est pas nécessaire (bien qu’il soit recommandé) s’il existe l’un des éléments suivants :  
  
-   L’attribut **SQL : key-fields** est défini pour les éléments du schéma de mappage spécifié.  
  
-   Il existe une ou plusieurs valeurs spécifiques fournies pour le ou les champs clés dans le code de mise à jour (updategram).  
  
 Si c’est le cas, le mise à jour utilise les colonnes clés spécifiées dans **SQL : key-fields** pour coupler les éléments dans les **\<before>** **\<after>** blocs et.  
  
 Si le schéma de mappage n’identifie pas les colonnes clés (à l’aide de **SQL : key-fields**) ou si mise à jour met à jour une valeur de colonne clé, vous devez spécifier **attribut updg : ID**.  
  
 Les enregistrements qui sont identifiés dans les **\<before>** **\<after>** blocs et n’ont pas besoin d’être dans le même ordre. L’attribut **attribut updg : ID** force l’association entre les éléments spécifiés dans les **\<before>** blocs et **\<after>** .  
  
 Si vous spécifiez un élément dans le **\<before>** bloc et un seul élément correspondant dans le **\<after>** bloc, l’utilisation de **attribut updg : ID** n’est pas nécessaire. Toutefois, il est recommandé de spécifier **attribut updg : ID** pour éviter toute ambiguïté.  
  
## <a name="examples"></a>Exemples  
 Avant d'utiliser les exemples de code de mise à jour (updategram), notez les points suivants :  
  
-   La plupart des exemples utilisent le mappage par défaut (en d'autres termes, aucun schéma de mappage n'est spécifié dans le code de mise à jour (updategram)). Pour obtenir plus d’exemples de codes qui utilisent des schémas de mappage, consultez [spécification d’un schéma de mappage annoté dans un mise à jour &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   La plupart des exemples sont basés sur l'exemple de base de données AdventureWorks. Toutes les mises à jour sont appliquées aux tables de cette base de données. Vous pouvez restaurer la base de données AdventureWorks.  
  
### <a name="a-updating-a-record"></a>A. Mise à jour d'un enregistrement  
 Le code de mise à jour (updategram) suivant met à jour le nom de famille d'un employé en le remplaçant par Fuller dans la table Person.Contact de la base de données AdventureWorks. Le code de mise à jour (updategram) ne spécifie pas de schéma de mappage ; par conséquent, le mappage par défaut est utilisé.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 L’enregistrement décrit dans le **\<before>** bloc représente l’enregistrement actif dans la base de données. Mise à jour utilise toutes les valeurs de colonne spécifiées dans le **\<before>** bloc pour Rechercher l’enregistrement. Dans ce mise à jour, le **\<before>** bloc fournit uniquement la colonne ContactID ; par conséquent, mise à jour utilise uniquement la valeur pour Rechercher l’enregistrement. Si vous deviez ajouter la valeur de LastName à ce bloc, le code de mise à jour (updategram) utiliserait à la fois les valeurs de ContactID et de LastName pour effectuer la recherche.  
  
 Dans ce mise à jour, le **\<after>** bloc fournit uniquement la valeur de la colonne LastName, car il s’agit de la seule valeur en cours de modification.  
  
##### <a name="to-test-the-updategram"></a>Pour tester le code de mise à jour  
  
1.  Copiez le modèle de code de mise à jour (updategram) ci-dessus et collez-le dans un fichier texte. Enregistrez le fichier sous le nom UpdateLastName.xml.  
  
2.  Créez et utilisez le script de test SQLXML 4.0 (Sqlxml4test.vbs) pour exécuter le code de mise à jour (updategram).  

     Pour plus d’informations, consultez [utilisation d’ADO pour exécuter des requêtes SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. Mise à jour de plusieurs enregistrements à l'aide de l'attribut updg:id  
 Dans cet exemple, le code de mise à jour (updategram) effectue deux mises à jour sur la table HumanResources.Shift de la base de données AdventureWorks :  
  
-   Il modifie le nom de l'équipe de jour d'origine qui commence à 7 h 09 en remplaçant « Day » par « Early Morning ».  
  
-   Il insère une nouvelle équipe nommée « Late Morning » qui commence à 10 h 00.  
  
 Dans mise à jour, l’attribut **attribut updg : ID** crée des associations entre les éléments des **\<before>** **\<after>** blocs et.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Notez que l’attribut **attribut updg : ID** couple la première instance de l' \<HumanResources.Shift> élément dans le **\<before>** bloc à la deuxième instance de l' \<HumanResources.Shift> élément dans le **\<after>** bloc.  
  
##### <a name="to-test-the-updategram"></a>Pour tester le code de mise à jour  
  
1.  Copiez le modèle de code de mise à jour (updategram) ci-dessus et collez-le dans un fichier texte. Enregistrez le fichier sous le nom UpdateMultipleRecords.xml.  
  
2.  Créez et utilisez le script de test SQLXML 4.0 (Sqlxml4test.vbs) pour exécuter le code de mise à jour (updategram).  
  
     Pour plus d’informations, consultez [utilisation d’ADO pour exécuter des requêtes SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. Spécification \<before> de plusieurs \<after> blocs et  
 Pour éviter toute ambiguïté, vous pouvez écrire le mise à jour dans l’exemple B à l’aide de plusieurs **\<before>** **\<after>** paires de blocs et. La spécification de **\<before>** **\<after>** paires et est un moyen de spécifier plusieurs mises à jour avec un minimum de confusion. En outre, si chacun des **\<before>** **\<after>** blocs et spécifie au plus un élément, vous n’êtes pas obligé d’utiliser l’attribut **attribut updg : ID** .  
  
> [!NOTE]  
>  Pour former une paire, la **\<after>** balise doit suivre immédiatement la **\<before>** balise correspondante.  
  
 Dans le mise à jour suivant, la première **\<before>** et la **\<after>** paire met à jour le nom du décalage pour l’équipe de jour. La seconde paire insère un nouvel enregistrement d'équipe.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Pour tester le code de mise à jour  
  
1.  Copiez le modèle de code de mise à jour (updategram) ci-dessus et collez-le dans un fichier texte. Enregistrez le fichier sous le nom UpdateMultipleBeforeAfter.xml.  
  
2.  Créez et utilisez le script de test SQLXML 4.0 (Sqlxml4test.vbs) pour exécuter le code de mise à jour (updategram).  
  
     Pour plus d’informations, consultez [utilisation d’ADO pour exécuter des requêtes SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. Spécification de plusieurs \<sync> blocs  
 Vous pouvez spécifier plusieurs **\<sync>** blocs dans un mise à jour. Chaque **\<sync>** bloc spécifié est une transaction indépendante.  
  
 Dans le mise à jour suivant, le premier **\<sync>** bloc met à jour un enregistrement dans la table Sales. Customer. Pour des raisons de simplicité, le code de mise à jour (updategram) spécifie uniquement les valeurs de colonne requises, la valeur d'identité (CustomerID) et la valeur mise à jour (SalesPersonID).  
  
 Le deuxième **\<sync>** bloc ajoute deux enregistrements à la table Sales. SalesOrderHeader. Pour cette table, SalesOrderID est une colonne de type IDENTITY. Par conséquent, mise à jour ne spécifie pas la valeur de SalesOrderID dans chacun des \<Sales.SalesOrderHeader> éléments.  
  
 La spécification de plusieurs **\<sync>** blocs est utile, car si le deuxième **\<sync>** bloc (une transaction) ne parvient pas à ajouter des enregistrements à la table Sales. SalesOrderHeader, le premier **\<sync>** bloc peut toujours mettre à jour l’enregistrement du client dans la table Sales. Customer.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Pour tester le code de mise à jour  
  
1.  Copiez le modèle de code de mise à jour (updategram) ci-dessus et collez-le dans un fichier texte. Enregistrez le fichier sous le nom UpdateMultipleSyncs.xml.  
  
2.  Créez et utilisez le script de test SQLXML 4.0 (Sqlxml4test.vbs) pour exécuter le code de mise à jour (updategram).  
  
     Pour plus d’informations, consultez [utilisation d’ADO pour exécuter des requêtes SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-a-mapping-schema"></a>E. Utilisation d'un schéma de mappage  
 Dans cet exemple, le mise à jour spécifie un schéma de mappage à l’aide de l’attribut **mapping-schema** . (Il n'y a aucun mappage par défaut ; en d'autres termes, le schéma de mappage fournit le mappage nécessaire des éléments et attributs du code de mise à jour (updategram) aux tables et colonnes de la base de données.)  
  
 Les éléments et attributs spécifiés dans le code de mise à jour (updategram) font référence aux éléments et attributs du schéma de mappage.  
  
 Le schéma de mappage XSD suivant contient les **\<Customer>** **\<Order>** éléments, et **\<OD>** qui mappent aux tables Sales. Customer, sales. SalesOrderHeader et Sales. SalesOrderDetail dans la base de données.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Ce schéma de mappage (UpdategramMappingSchema.xml) est spécifié dans le code de mise à jour (updategram) suivant. Le code de mise à jour (updategram) ajoute un article dans la table Sales.SalesOrderDetail pour une commande spécifique. Mise à jour comprend des éléments imbriqués : un **\<OD>** élément imbriqué à l’intérieur d’un **\<Order>** élément. La relation clé primaire/clé étrangère entre ces deux éléments est spécifiée dans le schéma de mappage.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Pour tester le code de mise à jour  
  
1.  Copiez le schéma de mappage ci-dessus et collez-le dans un fichier texte. Enregistrez le fichier sous le nom UpdategramMappingSchema.xml.  
  
2.  Copiez le modèle de code de mise à jour (updategram) ci-dessus et collez-le dans un fichier texte. Enregistrez le fichier sous le nom UpdateWithMappingSchema.xml dans le même dossier que celui utilisé pour l'enregistrement du schéma de mappage (UpdategramMappingSchema.xml).  
  
3.  Créez et utilisez le script de test SQLXML 4.0 (Sqlxml4test.vbs) pour exécuter le code de mise à jour (updategram).  
  
     Pour plus d’informations, consultez [utilisation d’ADO pour exécuter des requêtes SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Pour obtenir plus d’exemples de codes qui utilisent des schémas de mappage, consultez [spécification d’un schéma de mappage annoté dans un mise à jour &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. Utilisation d'un schéma de mappage avec les attributs IDREFS  
 Cet exemple montre comment les codes de mise à jour (updategrams) utilisent les attributs IDREFS du schéma de mappage pour mettre à jour des enregistrements dans plusieurs tables. Pour cet exemple, supposez que la base de données comporte les tables suivantes :  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 Dans la mesure où un étudiant peut s'inscrire à de nombreux cours et comme un cours peut avoir de nombreux étudiants, la troisième table, la table Enrollment, est requise pour représenter cette relation M:N.  
  
 Le schéma de mappage XSD suivant fournit une vue XML des tables à l’aide **\<Student>** des **\<Course>** éléments, et **\<Enrollment>** . Les attributs **IDREFS** dans le schéma de mappage spécifient la relation entre ces éléments. L’attribut **StudentIDList** de l' **\<Course>** élément est un attribut de type **IDREFS** qui fait référence à la colonne StudentID de la table d’inscription. De même, l’attribut **EnrolledIn** sur l' **\<Student>** élément est un attribut de type **IDREFS** qui fait référence à la colonne CourseID dans la table d’inscription.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Chaque fois que vous spécifiez ce schéma dans un code de mise à jour (updategram) et que vous insérez un enregistrement dans la table Course, le code de mise à jour (updategram) insère un nouvel enregistrement de cours dans la table Course. Si vous spécifiez un ou plusieurs nouveaux ID d'étudiants pour l'attribut StudentIDList, le code de mise à jour (updategram) insère également un enregistrement dans la table Enrollment pour chaque nouvel étudiant. Le code de mise à jour (updategram) s'assure qu'aucun doublon n'est ajouté à la table Enrollment.  
  
##### <a name="to-test-the-updategram"></a>Pour tester le code de mise à jour  
  
1.  Créez ces tables dans la base de données spécifiée dans la racine virtuelle :  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  Ajoutez les exemples de données suivants :  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  Copiez le schéma de mappage ci-dessus et collez-le dans un fichier texte. Enregistrez le fichier sous le nom SampleSchema.xml.  
  
4.  Enregistrez le code de mise à jour (SampleUpdategram) dans le même dossier que celui utilisé pour l'enregistrement du schéma de mappage à l'étape précédente. (Ce code de mise à jour (updategram) supprime un étudiant pour lequel StudentID="1" dans le cours CS102.)  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  Créez et utilisez le script de test SQLXML 4.0 (Sqlxml4test.vbs) pour exécuter le code de mise à jour (updategram).  
  
     Pour plus d’informations, consultez [utilisation d’ADO pour exécuter des requêtes SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
6.  Enregistrez et exécutez le code de mise à jour (updategram) suivant, comme décrit dans les étapes précédentes. Le code de mise à jour (updategram) rajoute l'étudiant pour lequel StudentID="1" dans le cours CS102 en insérant un enregistrement dans la table Enrollment.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  Enregistrez et exécutez le mise à jour suivant comme décrit dans les étapes précédentes. Ce code de mise à jour (updategram) insère trois nouveaux étudiants et les inscrit au cours CS101. À nouveau, la relation IDREFS insère des enregistrements dans la table Enrollment.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 Voici le schéma XDR équivalent :  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 Pour obtenir plus d’exemples de codes qui utilisent des schémas de mappage, consultez [spécification d’un schéma de mappage annoté dans un mise à jour &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Considérations sur la sécurité mise à jour &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
