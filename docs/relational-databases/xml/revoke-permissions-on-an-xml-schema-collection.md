---
title: Revogar permissões em uma coleção de esquemas XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- revoking permissions [SQL Server]
ms.assetid: 4e542b70-2d56-4a65-8a39-96a1ed477ca6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d2cdfdf47aad32c9fc669ae054cf84c061c0ee5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000758"
---
# <a name="revoke-permissions-on-an-xml-schema-collection"></a>Revogar permissões em uma coleção de esquemas XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  A permissão para criar uma coleção de esquema XML pode ser revogada usando uma das seguintes opções:  
  
-   Revogar a permissão ALTER para o esquema relacional. Em seguida, a entidade de segurança não pode criar uma coleção de esquema XML no esquema relacional. Porém a entidade de segurança ainda pode fazer isso em outros esquemas relacionais no mesmo banco de dados.  
  
-   Revogar a permissão ALTER ANY SCHEMA no banco de dados para a entidade de segurança. Em seguida, a entidade de segurança não pode criar uma coleção de esquema XML em nenhum outro lugar no banco de dados.  
  
-   Revogar a permissão CREATE XML SCHEMA COLLECTION ou ALTER XML SCHEMA COLLECTION no banco de dados para a entidade de segurança. Isto impede que a entidade de segurança importe uma coleção de esquema XML dentro do banco de dados. O mesmo efeito é obtido com a revogação da permissão ALTER ou CONTROL no banco de dados.  
  
## <a name="revoking-permissions-on-an-existing-xml-schema-collection-object"></a>Revogando permissões em um objeto de coleção de esquema XML existente  
 A lista a seguir apresenta as permissões que podem ser revogadas em uma coleção de esquema XML e seus resultados:  
  
-   A revogação da permissão ALTER revoga a capacidade de uma entidade de segurança de modificar o conteúdo da coleção de esquema XML.  
  
-   A revogação da permissão TAKE OWNERSHIP revoga a capacidade da entidade de segurança de transferir a propriedade da coleção de esquema XML.  
  
-   A revogação da permissão REFERENCES revoga a capacidade da entidade de segurança de usar a coleção de esquema XML para digitar ou restringir colunas de tipo xml em tabelas, exibições e parâmetros. Ela também revoga a permissão para fazer referência a esta coleção de esquema a partir de outras coleções de esquema XML.  
  
-   A revogação da permissão VIEW DEFINITION revoga a capacidade da entidade de segurança de exibir o conteúdo de uma coleção de esquema XML.  
  
-   A revogação da permissão EXECUTE revoga a capacidade da entidade de segurança de inserir ou atualizar valores em colunas, variáveis e parâmetros que são de tipo ou restringidas pela coleção XML. Ela também revoga a capacidade de consultar essas colunas, variáveis ou parâmetros de tipo **xml** .  
  
## <a name="examples"></a>Exemplos  
 Os cenários nos exemplos seguintes ilustram como as permissões de esquema XML funcionam. Cada exemplo cria o banco de dados, os esquemas relacionais e os logons de teste necessários. Esses logons recebem as permissões necessárias na coleção de esquema XML. Cada exemplo faz a limpeza necessária no final.  
  
### <a name="a-revoking-permissions-to-create-an-xml-schema-collection"></a>A. Revogando permissões para criar uma coleção de esquemas XML  
 Este exemplo cria um logon e um banco de dados de exemplo. Ele também adiciona um esquema relacional no banco de dados. Inicialmente, o logon recebe permissão ALTER nos dois esquemas relacionais e outras permissões necessárias para criar coleções de esquema XML. Em seguida, o exemplo revoga a permissão ALTER em um dos esquemas relacionais do banco de dados. Isso impede que o logon crie uma coleção de esquema XML.  
  
```  
setuser  
go  
create login TestLogin1 with password='SQLSvrPwd1'  
go  
create database SampleDBForSchemaPermissions  
go  
use SampleDBForSchemaPermissions  
go  
-- Create another relational schema in the db (in addition to dbo schema)  
CREATE SCHEMA myOtherDBSchema  
go  
CREATE USER TestLogin1  
go  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed  
-- CREATE XML SCHEMA is a database level permission  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
go  
-- Now TestLogin1 can import an XML schema collection in both relational schemas.  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- TestLogin1 can create XML schema collection in myOtherDBSchema relational schema  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- Let us drop XML schema collections from both relational schemas  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
go  
DROP XML SCHEMA COLLECTION dbo.myTestSchemaCollection  
go  
-- now REVOKE permission from TestLogin1 to alter myOtherDBSchema  
setuser  
go  
REVOKE ALTER ON SCHEMA::myOtherDBSchema FROM TestLogin1  
go  
-- now TestLogin1 cannot create xml schema collection in myOtherDBSchema  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- TestLogin1 can still create XML schema collections in dbo  
-- It cannot create XML schema collections anywhere in the database  
-- if we REVOKE CREATE XML SCHEMA COLLECTION permission  
SETUSER  
go  
REVOKE CREATE XML SCHEMA COLLECTION FROM TestLogin1  
go  
  
setuser 'TestLogin1'  
go  
-- the following now should fail  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- Final cleanup  
SETUSER  
go  
USE master  
go  
DROP DATABASE SampleDBForSchemaPermissions  
go  
DROP LOGIN TestLogin1  
Go  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Coleções de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Requisitos e limitações de uso de coleções de esquema XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
