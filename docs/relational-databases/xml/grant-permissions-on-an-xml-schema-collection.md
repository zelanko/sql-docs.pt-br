---
title: "Conceder permissões em uma coleção de esquemas XML | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- granting permissions [SQL Server], XML schema collections
- ALTER permission
ms.assetid: ffbb829c-3b8f-4e5d-97d9-ab4059aab0db
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d05c9c0f30602f0cdcfe29a7d94adb31e7600804
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="grant-permissions-on-an-xml-schema-collection"></a>Conceder permissões em uma coleção de esquemas XML
  É possível conceder permissões para criar uma coleção de esquema XML e também permissões em um objeto da coleção de esquemas XML.  
  
## <a name="granting-permission-to-create-an-xml-schema-collection"></a>Concedendo permissão para criar uma coleção de esquema XML  
 Para criar uma coleção de esquema XML, são necessárias as seguintes permissões:  
  
-   A entidade de segurança requer permissão CREATE XML SCHEMA COLLECTION no nível de banco de dados.  
  
-   Como as coleções de esquema XML estão no escopo do esquema relacional, a entidade de segurança deve ter permissão ALTER no esquema relacional.  
  
 As seguintes permissões permitem que uma entidade de segurança crie uma coleção de esquema XML em um esquema relacional em um banco de dados em um servidor:  
  
-   Permissão CONTROL no servidor  
  
-   Permissão ALTER ANY DATABASE no servidor  
  
-   Permissão ALTER no banco de dados  
  
-   Permissão CONTROL no banco de dados  
  
-   Permissões ALTER ANY SCHEMA e CREATE XML SCHEMA COLLECTION no banco de dados  
  
-   Permissões ALTER ou CONTROL no esquema relacional e CREATE XML SCHEMA COLLECTION no banco de dados  
  
 Esse último método de permissões é usado no exemplo seguinte.  
  
 O proprietário do esquema relacional se torna o proprietário da coleção de esquema XML criada naquele esquema. Esse proprietário tem controle total sobre a coleção de esquema XML. Portanto esse proprietário pode modificar a coleção de esquema XML, digitar uma coluna xml ou descartar a coleção e esquema XML.  
  
## <a name="granting-permissions-on-an-xml-schema-collection-object"></a>Concedendo permissões em um objeto da coleção de esquema XML  
 As seguintes permissões são permitidas na coleção de esquema XML:  
  
-   A permissão ALTER é necessária ao modificar o conteúdo de uma coleção de esquema XML existente usando uma instrução ALTER XML SCHEMA COLLECTION.  
  
-   A permissão CONTROL permite que um usuário execute qualquer operação na coleção de esquema XML.  
  
-   A permissão TAKE OWNERSHIP é necessária para transferir a propriedade da coleção de esquemas XML de uma entidade de segurança para outra.  
  
-   A permissão REFERENCES autoriza a entidade de segurança a usar a coleção de esquema XML para digitar ou restringir colunas de tipo **xml** em tabelas, exibições e parâmetros. A permissão REFERENCES também é necessária quando uma coleção de esquemas XML faz referência à outra.  
  
-   A permissão VIEW DEFINITION permite que a entidade de segurança consulte o conteúdo de uma coleção de esquema XML por meio de XML_SCHEMA_NAMESPACE ou de exibições de catálogo, desde que a entidade de segurança tenha uma das permissões ALTER, REFERENCES ou CONTROL na coleção.  
  
-   A permissão EXECUTE é necessária para validar valores inseridos ou atualizados pela entidade de segurança na coleção de esquema XML que está digitando ou restringindo as variáveis, parâmetros e colunas de tipo **xml** . Essa permissão também é necessária para consultar o XML armazenado nessas colunas e variáveis.  
  
## <a name="examples"></a>Exemplos  
 Os cenários nos exemplos seguintes ilustram como as permissões de esquema XML funcionam. Cada exemplo cria o banco de dados, os esquemas relacionais e os logons de teste necessários. Esses logons recebem as permissões necessárias na coleção de esquema XML. Cada exemplo faz a limpeza necessária no final.  
  
### <a name="a-granting-permissions-to-create-an-xml-schema-collection"></a>A. Concedendo permissões para criar uma coleção de esquema XML  
 O exemplo a seguir mostra como conceder permissões para que uma entidade de segurança possa criar uma coleção de esquemas XML. O exemplo cria um banco de dados de exemplo e um usuário de teste, `TestLogin1`. `TestLogin1` recebe a permissão `ALTER` no esquema relacional e a permissão `CREATE XML SCHEMA COLLECTION` no banco de dados. Com essas permissões, `TestLogin1` pode criar com êxito uma coleção de esquemas XML de exemplo.  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Execute CREATE XML SCHEMA COLLECTION.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="root" type="xsd:byte"/>  
</xsd:schema>'  
GO  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="b-granting-permission-to-use-an-existing-xml-schema-collection"></a>B. Concedendo permissão para usar uma coleção de esquema XML existente  
 O exemplo seguinte mostra ainda mais o modelo de permissão para a coleção de esquema XML. Ele mostra como permissões diferentes são necessárias para criar e usar a coleção de esquema XML.  
  
 O exemplo cria um banco de dados de teste e um logon, `TestLogin1`. `TestLogin1` cria uma coleção de esquemas XML no banco de dados. Em seguida, o logon cria uma tabela e usa a coleção de esquemas XML para criar uma coluna do tipo xml. Em seguida, o usuário insere dados e os consulta. Todas essas etapas requerem as permissões de esquema necessárias conforme mostrado no código.  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- Grant permission to the user.  
SETUSER  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Now user can execute the previous CREATE XML SCHEMA COLLECTION statement.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
  
-- Create a table by using the collection to type an XML column.   
--TestLogin1 must have permission to create a table.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also must have REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myTestSchemaCollection   
TO TestLogin1  
GO  
-- Now user can create a table and use the XML schema collection to create   
-- a typed XML column.  
SETUSER 'TestLogin1'  
GO  
CREATE TABLE MyTestTable (xmlCol xml (dbo.myTestSchemaCollection))  
GO  
-- To insert data in the table, the user needs EXECUTE permission on the XML schema collection.  
-- GRANT EXECUTE permission to TestLogin2 on the xml schema collection.  
SETUSER  
GO  
GRANT EXECUTE ON XML SCHEMA COLLECTION::myTestSchemaCollection   
TO TestLogin1  
GO  
-- TestLogin1 does not own the dbo schema. This user must have INSERT permission.  
GRANT INSERT TO TestLogin1  
GO  
-- Now the user can insert data into the table.  
SETUSER 'TestLogin1'  
GO  
INSERT INTO MyTestTable VALUES('  
<telephone xmlns="http://schemas.adventure-works.com/Additional/ContactInfo">111-1111</telephone>  
')  
GO  
-- To query the table, TestLogin1 must have permissions: SELECT on the table and EXECUTE on the XML schema collection.  
SETUSER  
GO  
GRANT SELECT TO TestLogin1  
GO  
-- TestLogin1 already has EXECUTE permission on the schema (granted before inserting a record in the table).  
SELECT xmlCol.query('declare default element namespace "http://schemas.adventure-works.com/Additional/ContactInfo" /telephone[1]')  
FROM MyTestTable  
GO  
-- To show that the user must have EXECUTE permission to query, revoke the  
-- previously granted permission and return the query.  
SETUSER  
GO  
REVOKE EXECUTE ON XML SCHEMA COLLECTION::myTestSchemaCollection to TestLogin1  
Go  
-- Now TestLogin1 cannot execute the query.  
SETUSER 'TestLogin1'  
GO  
SELECT xmlCol.query('declare default element namespace "http://schemas.adventure-works.com/Additional/ContactInfo" /telephone[1]')  
FROM MyTestTable  
GO  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="c-granting-alter-permission-on-an-xml-schema-collection"></a>C. Concedendo permissão ALTER em uma coleção de esquema XML  
 Um usuário precisa ter a permissão ALTER para modificar uma coleção de esquema XML existente no banco de dados. O exemplo a seguir mostra como conceder a permissão `ALTER` .  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- Grant permission to the user.  
SETUSER  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Now user can execute the previous CREATE XML SCHEMA COLLECTION statement.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant ALTER permission to TestLogin1.  
setuser  
GO  
GRANT ALTER ON XML SCHEMA COLLECTION::myTestSchemaCollection TO TestLogin1  
GO  
-- TestLogin1 should be able to add components to the collection.  
SETUSER 'TestLogin1'  
GO  
ALTER XML SCHEMA COLLECTION myTestSchemaCollection ADD '  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns="http://schemas.adventure-works.com/Additional/ContactInfo"   
elementFormDefault="qualified">  
 <xsd:element name="pager" type="xsd:string"/>  
</xsd:schema>  
'  
Go  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="d-granting-take-ownership-permission-on-an-xml-schema-collection"></a>D. Concedendo a permissão TAKE OWNERSHIP em uma coleção de esquemas XML  
 O exemplo a seguir mostra como transferir a propriedade do esquema XML de um usuário para outro. Para tornar o exemplo mais interessante, os usuários neste trabalho de exemplo trabalham em diferentes esquemas relacionais padrão.  
  
 Este exemplo faz o seguinte:  
  
-   Cria um banco de dados com dois esquemas relacionais ( `dbo` e `myOtherDBSchema`).  
  
-   Cria dois usuários, `TestLogin1` e `TestLogin2`. `TestLogin2` se torna o proprietário do esquema relacional `myOtherDBSchema` .  
  
-   `TestLogin1` cria uma coleção de esquemas XML no esquema relacional `dbo` .  
  
-   `TestLogin1` concede a permissão `TAKE OWNERSHIP` na coleção de esquemas XML para `TestLogin2`.  
  
-   `TestLogin2` se torna o proprietário da coleção de esquemas XML no `myOtherDBSchema`, sem alterar o esquema relacional da coleção de esquemas XML.  
  
```  
CREATE LOGIN TestLogin1 with password='SQLSvrPwd1'  
GO  
CREATE LOGIN TestLogin2 with password='SQLSvrPwd2'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
-- Create users in the database. Note TestLogin2's default schema is  
-- myOtherDBSchema.  
CREATE USER TestLogin1  
GO  
CREATE USER TestLogin2 WITH DEFAULT_SCHEMA=myOtherDBSchema  
GO  
-- TestLogin2 will own myOtherDBSchema relational schema.  
ALTER AUTHORIZATION ON SCHEMA::myOtherDBSchema TO TestLogin2  
GO  
  
-- For TestLogin1 to create XML schema collection, the following  
-- permission is required.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- Now TestLogin1 can create an XML schema collection.  
setuser 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
 <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"   
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
 </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
  
-- Grant TAKE OWNERSHIP to TestLogin2.  
SETUSER  
GO  
GRANT TAKE OWNERSHIP ON XML SCHEMA COLLECTION::dbo.myTestSchemaCollection   
TO TestLogin2  
GO  
-- Verify the owner. Note the UserName and Principal_id is null.   
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
       sys.schemas.name as RelSchemaName,*   
FROM   sys.xml_schema_collections   
      JOIN sys.schemas   
      ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
-- TestLogin2 can take ownership now.  
setuser 'TestLogin2'  
GO  
ALTER AUTHORIZATION ON XML SCHEMA COLLECTION::dbo.myTestSchemaCollection   
TO TestLogin2  
GO  
-- Note that although TestLogin2 is the owner,the XML schema collection   
-- is still in dbo.  
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
      sys.schemas.name as RelSchemaName,*   
FROM sys.xml_schema_collections JOIN sys.schemas   
     ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
  
-- TestLogin2 moves the collection from dbo to myOtherDBSchema relational schema.  
-- TestLogin2 already has all necessary permissions.  
-- 1) TestLogin2 owns the destination relational schema so he can alter it.  
-- 2) TestLogin2 owns the XML schema collection (therefore, has CONTROL permission).  
ALTER SCHEMA myOtherDBSchema  
TRANSFER XML SCHEMA COLLECTION::dbo.myTestSchemaCollection  
GO  
  
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
       sys.schemas.name as RelSchemaName,*   
FROM   sys.xml_schema_collections JOIN sys.schemas   
       ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
DROP LOGIN TestLogin2  
go   
```  
  
### <a name="e-granting-view-definition-permission-on-an-xml-schema-collection"></a>E. Concedendo permissão VIEW DEFINITION em uma coleção de esquema XML  
 Este exemplo mostra como conceder permissões VIEW DEFINITION para uma coleção de esquema XML:  
  
```  
SETUSER  
GO  
USE master  
GO  
IF EXISTS( SELECT * FROM sysdatabases WHERE name='permissionsDB' )  
   DROP DATABASE permissionsDB  
GO  
IF EXISTS( SELECT * FROM sys.sql_logins WHERE name='schemaUser' )  
   DROP LOGIN schemaUser  
GO  
CREATE DATABASE permissionsDB  
GO  
CREATE LOGIN schemaUser WITH PASSWORD='Pass#123',DEFAULT_DATABASE=permissionsDB  
GO  
GRANT CONNECT SQL TO schemaUser  
GO  
USE permissionsDB  
GO  
CREATE USER schemaUser WITH DEFAULT_SCHEMA=dbo  
GO  
CREATE XML SCHEMA COLLECTION MySC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns"  
xmlns:ns="http://ns">  
  
   <simpleType name="ListOfIntegers">  
      <list itemType="integer"/>  
   </simpleType>  
  
   <element name="root" type="ns:ListOfIntegers"/>  
  
   <element name="gRoot" type="gMonth"/>  
  
</schema>  
'  
GO  
-- schemaUser cannot see the contents of the collection.  
SETUSER 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
  
-- Grant schemaUser VIEW DEFINITION and REFERENCES permissions  
-- on the XML schema collection.  
SETUSER  
GO  
GRANT VIEW DEFINITION ON XML SCHEMA COLLECTION::dbo.MySC TO schemaUser  
GO  
GRANT REFERENCES ON XML SCHEMA COLLECTION::dbo.MySC TO schemaUser  
GO  
-- Now schemaUser can see the content of the collection.  
SETUSER 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
-- Revoke schemaUser VIEW DEFINITION permissions  
-- on the XML schema collection.  
SETUSER  
GO  
REVOKE VIEW DEFINITION ON XML SCHEMA COLLECTION::dbo.MySC FROM schemaUser  
GO  
-- Now schemaUser cannot see the contents of   
-- the collection.  
setuser 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Coleções de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Requisitos e limitações de uso de coleções de esquema XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
