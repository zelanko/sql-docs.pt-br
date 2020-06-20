---
title: Recusar permissões em uma coleção de esquemas XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- denying permissions [SQL Server], XML server collections
ms.assetid: e2b300b0-e734-4c43-a4da-c78e6e5d4fba
author: rothja
ms.author: jroth
ms.openlocfilehash: 0791a9bd9c7f6b323886a38bed27bea84940770d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046709"
---
# <a name="deny-permissions-on-an-xml-schema-collection"></a>Recusar permissões em uma coleção de esquemas XML
  Permissões podem ser negadas para criar uma nova coleção de esquema XML ou para usar uma coleção existente.  
  
## <a name="denying-permission-to-create-an-xml-schema-collection"></a>Negando permissão para criar uma coleção de esquema XML  
 É possível negar permissão para criar uma coleção de esquema XML das seguintes maneiras:  
  
-   Negar a permissão ALTER no esquema relacional.  
  
-   Negar CONTROL no esquema relacional para negar todas as permissões no esquema relacional e em todos os objetos contidos nele.  
  
-   Negar ALTER ANY SCHEMA no banco de dados. Nesse caso, a entidade de segurança não pode criar uma coleção de esquema XML em nenhum outro lugar no banco de dados. Observe também que negar a permissão ALTER ou CONTROL no banco de dados nega todas as permissões em todos os objetos do banco de dados.  
  
## <a name="denying-permissions-on-an-xml-schema-collection-object"></a>Negando permissões em um objeto da coleção de esquema XML  
 A lista a seguir apresenta as permissões que podem ser negadas em uma coleção de esquema XML existente e seus resultados:  
  
-   Negar a permissão ALTER nega a capacidade de uma entidade de segurança de modificar o conteúdo da coleção de esquema XML.  
  
-   Negar a permissão CONTROL nega a capacidade de uma entidade de segurança de executar qualquer operação na coleção de esquema XML.  
  
-   Negar a permissão REFERENCES nega a capacidade da entidade de segurança de digitar ou restringir colunas e parâmetros de tipo xml usando a coleção de esquema XML. Ela também nega a capacidade da entidade de segurança de fazer referência a esta coleção de esquema XML a partir de outras coleções de esquema XML.  
  
-   Negar a permissão VIEW DEFINITION nega a capacidade da entidade de segurança de exibir o conteúdo de uma coleção de esquema XML.  
  
-   Negar a permissão EXECUTE nega a capacidade da entidade de segurança de inserir ou atualizar valores em colunas, variáveis e parâmetros que são de tipo ou restritas pela coleção de esquema XML. Também nega a capacidade da entidade de segurança de consultar os valores nestas colunas e variáveis de tipo xml.  
  
## <a name="examples"></a>Exemplos  
 Os cenários nos exemplos a seguir mostram como as permissões de esquema XML funcionam. Cada exemplo cria o banco de dados, os esquemas relacionais e os logons de teste necessários. Esses logons recebem as permissões necessárias na coleção de esquema XML. Cada exemplo faz a limpeza necessária no final.  
  
### <a name="a-preventing-a-user-from-creating-an-xml-schema-collection"></a>a. Impedindo que um usuário crie uma coleção de esquema XML  
 Uma das maneiras de impedir que um usuário crie uma coleção de esquema XML é negar a permissão ALTER em um esquema relacional. Isso é mostrado no exemplo a seguir.  
  
 O exemplo cria um usuário, `TestLogin1`, e um banco de dados. Ele também cria um esquema relacional, além do esquema `dbo` , no banco de dados. Inicialmente, a permissão `CREATE XML SCHEMA` permite que o usuário crie uma coleção de esquema em qualquer lugar no banco de dados. Em seguida, o exemplo nega permissão `ALTER` ao usuário em um dos esquemas relacionais. Isto impede que o usuário crie uma coleção de esquema XML naquele esquema relacional.  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
GO  
-- Now deny permission from TestLogin1 to alter myOtherDBSchema.  
setuser  
GO  
DENY ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
GO  
-- Now TestLogin1 cannot create xml schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
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
  
### <a name="b-denying-permissions-on-an-xml-schema-collection"></a>B. Negando permissões em uma coleção de esquemas XML  
 O exemplo a seguir mostra como uma permissão específica em uma coleção de esquema XML pode ser negada para um logon. Neste exemplo, a permissão REFERENCES é negada a um logon de teste em uma coleção de esquema XML.  
  
 O exemplo cria um usuário, `TestLogin1`, e um banco de dados. Ele também cria um esquema relacional, além do esquema `dbo` , no banco de dados. Inicialmente, a permissão `CREATE XML SCHEMA` permite que o usuário crie uma coleção de esquema em qualquer lugar no banco de dados.  
  
 A permissão `REFERENCES` na coleção de esquema XML permite que o `TestLogin1` use o esquema para criar uma coluna `xml` com tipo em uma tabela. Se a permissão `REFERENCES` na coleção de esquema XML for negada, ela impedirá que o `TestLogin1` use a coleção de esquema XML.  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, the following  
-- permission is required.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant permission to TestLogin1 to create a table and reference the XML schema collection.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also needs REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on the schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection   
TO TestLogin1  
GO  
  
--TestLogin1 can use the schema.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
-- Drop the table.  
DROP TABLE T  
GO  
-- Now deny REFERENCES permission to TestLogin1 on the schema created previously.  
SETUSER  
GO  
DENY REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection TO TestLogin1  
  
GO  
-- Now TestLogin1 cannot create xml schema collection  
SETUSER 'TestLogin1'  
GO  
-- Following statement fails. TestLogin1 does not have REFERENCES   
-- permission on the XML schema collection.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
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
  
## <a name="see-also"></a>Consulte Também  
 [Comparar XML digitado com XML não digitado](compare-typed-xml-to-untyped-xml.md)   
 [Coleções de esquemas XML &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)   
 [Requisitos e limitações de uso de coleções de esquema XML no servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)   
 [Permissões de objeto DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-object-permissions-transact-sql)   
 [Permissões de objeto GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql)   
 [Dados XML &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
