---
title: ALTER XML SCHEMA COLLECTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_XML_SCHEMA_COLLECTION_TSQL
- ALTER XML SCHEMA COLLECTION
dev_langs:
- TSQL
helpviewer_keywords:
- schema collections [SQL Server], altering
- xml_schema_namespace function
- adding schema components
- ALTER XML SCHEMA COLLECTION statement
- XML schemas [SQL Server], adding
- XML schema collections [SQL Server], modifying
- schema collections [SQL Server], adding components
- XML schema collections [SQL Server], adding components
- importing schemas
- XML schema collections [SQL Server], altering
- schema collections [SQL Server], modifying
- multiple schema namespaces
ms.assetid: e311c425-742a-4b0d-b847-8b974bf66d53
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 832b8a0c0d66a1e9754366e7735ebbac84b3ac7b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895554"
---
# <a name="alter-xml-schema-collection-transact-sql"></a>ALTER XML SCHEMA COLLECTION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Adiciona novos componentes de esquema a uma coleção de esquema XML existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER XML SCHEMA COLLECTION [ relational_schema. ]sql_identifier ADD 'Schema Component'  
```  
  
## <a name="arguments"></a>Argumentos  
 *relational_schema*  
 Identifica o nome de esquema relacional. Se não for especificado, o esquema relacional padrão será usado.  
  
 *sql_identifier*  
 É o identificador SQL para a coleção de esquema XML.  
  
 **'** *Schema Component* **'**  
 É o componente de esquema a ser inserido.  
  
## <a name="remarks"></a>Comentários  
 Use ALTER XML SCHEMA COLLECTION para adicionar novos esquemas XML cujos namespaces ainda não estejam na coleção de esquema XML ou para adicionar novos componentes a namespaces existentes na coleção.  
  
 O exemplo a seguir adiciona um novo \<element> ao namespace existente `https://MySchema/test_xml_schema` na coleção `MyColl`.  
  
```  
-- First create an XML schema collection.  
CREATE XML SCHEMA COLLECTION MyColl AS '  
   <schema   
    xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="https://MySchema/test_xml_schema">  
      <element name="root" type="string"/>   
  </schema>'  
-- Modify the collection.   
ALTER XML SCHEMA COLLECTION MyColl ADD '  
  <schema xmlns="http://www.w3.org/2001/XMLSchema"   
         targetNamespace="https://MySchema/test_xml_schema">   
     <element name="anotherElement" type="byte"/>   
 </schema>';  
```  
  
 `ALTER XML SCHEMA` adiciona o elemento `<anotherElement>` ao namespace `https://MySchema/test_xml_schema` definido anteriormente.  
  
 Se alguns componentes que você deseja adicionar à coleção fizerem referência a componentes que já estão na mesma coleção, use `<import namespace="referenced_component_namespace" />`. No entanto, não é válido usar o namespace do esquema atual em `<xsd:import>` e, portanto, os componentes do mesmo namespace de destino do namespace do esquema atual são importados automaticamente.  
  
 Para remover coleções, use [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md).  
  
 Se a coleção de esquemas já tiver um curinga de validação incerta ou um elemento do tipo **xs:anyType**, a adição de um novo elemento global, tipo ou declaração de atributo à coleção de esquemas causará a revalidação de todos os dados armazenados que são restritos pela coleção de esquemas.  
  
## <a name="permissions"></a>Permissões  
 Para alterar uma XML SCHEMA COLLECTION, requer a permissão ALTER na coleção.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-xml-schema-collection-in-the-database"></a>a. Criando uma coleção de esquema XML no banco de dados  
 O exemplo a seguir cria uma coleção de esquema XML `ManuInstructionsSchemaCollection`. A coleção tem apenas um namespace de esquema.  
  
```  
-- Create a sample database in which to load the XML schema collection.  
CREATE DATABASE SampleDB;  
GO  
USE SampleDB;  
GO  
CREATE XML SCHEMA COLLECTION ManuInstructionsSchemaCollection AS  
N'<?xml version="1.0" encoding="UTF-16"?>  
<xsd:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   xmlns          ="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   elementFormDefault="qualified"   
   attributeFormDefault="unqualified"  
   xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
  
    <xsd:complexType name="StepType" mixed="true" >  
        <xsd:choice  minOccurs="0" maxOccurs="unbounded" >   
            <xsd:element name="tool" type="xsd:string" />  
            <xsd:element name="material" type="xsd:string" />  
            <xsd:element name="blueprint" type="xsd:string" />  
            <xsd:element name="specs" type="xsd:string" />  
            <xsd:element name="diag" type="xsd:string" />  
        </xsd:choice>   
    </xsd:complexType>  
  
    <xsd:element  name="root">  
        <xsd:complexType mixed="true">  
            <xsd:sequence>  
                <xsd:element name="Location" minOccurs="1" maxOccurs="unbounded">  
                    <xsd:complexType mixed="true">  
                        <xsd:sequence>  
                            <xsd:element name="step" type="StepType" minOccurs="1" maxOccurs="unbounded" />  
                        </xsd:sequence>  
                        <xsd:attribute name="LocationID" type="xsd:integer" use="required"/>  
                        <xsd:attribute name="SetupHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="MachineHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LaborHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LotSize" type="xsd:decimal" use="optional"/>  
                    </xsd:complexType>  
                </xsd:element>  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>' ;  
GO  
-- Verify - list of collections in the database.  
SELECT *  
FROM sys.xml_schema_collections;  
-- Verify - list of namespaces in the database.  
SELECT name  
FROM sys.xml_schema_namespaces;  
  
-- Use it. Create a typed xml variable. Note the collection name   
-- that is specified.  
DECLARE @x xml (ManuInstructionsSchemaCollection);  
GO  
--Or create a typed xml column.  
CREATE TABLE T (  
        i int primary key,   
        x xml (ManuInstructionsSchemaCollection));  
GO  
-- Clean up.  
DROP TABLE T;  
GO  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
Go  
USE master;  
GO  
DROP DATABASE SampleDB;  
```  
  
 Opcionalmente, você pode atribuir a coleção de esquema a uma variável e especificar a variável na instrução `CREATE XML SCHEMA COLLECTION` do seguinte modo:  
  
```  
DECLARE @MySchemaCollection nvarchar(max);  
SET @MySchemaCollection  = N' copy the schema collection here';  
CREATE XML SCHEMA COLLECTION AS @MySchemaCollection;   
```  
  
 A variável do exemplo é do tipo `nvarchar(max)`. A variável também pode ser do tipo de dados **xml** e, nesse caso, ela é convertida implicitamente em uma cadeia de caracteres.  
  
 Para obter mais informações, veja [Exibir uma coleção de esquemas XML armazenados](../../relational-databases/xml/view-a-stored-xml-schema-collection.md).  
  
 Você pode armazenar coleções de esquemas em uma coluna do tipo **xml**. Neste caso, para criar a coleção de esquema XLX, execute as seguintes etapas:  
  
1.  Recupere a coleção de esquemas da coluna usando uma instrução SELECT e atribua-a a uma variável do tipo **xml** ou de um tipo **varchar**.  
  
2.  Especifique o nome da variável na instrução CREATE XML SCHEMA COLLECTION.  
  
 A instrução CREATE XML SCHEMA COLLECTION armazena somente os componentes de esquema reconhecidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; nem tudo que está contido no esquema XML é armazenado no banco de dados. Portanto, se desejar que a coleção de esquema XML volte a ser exatamente igual a quando for fornecida, recomendamos que você salve os esquemas XML em uma coluna de banco de dados ou em alguma outra pasta do computador.  
  
### <a name="b-specifying-multiple-schema-namespaces-in-a-schema-collection"></a>B. Especificando vários namespaces de esquema em uma coleção de esquemas  
 Você pode especificar vários esquemas XML ao criar uma coleção de esquema XML. Por exemplo:  
  
```  
CREATE XML SCHEMA COLLECTION N'  
<xsd:schema>....</xsd:schema>  
<xsd:schema>...</xsd:schema>';  
```  
  
 O exemplo a seguir cria a coleção de esquema XML `ProductDescriptionSchemaCollection` que inclui dois namespaces de esquema XML.  
  
```  
CREATE XML SCHEMA COLLECTION ProductDescriptionSchemaCollection AS   
'<xsd:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"  
    xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
    elementFormDefault="qualified"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
    <xsd:element name="Warranty"  >  
        <xsd:complexType>  
            <xsd:sequence>  
                <xsd:element name="WarrantyPeriod" type="xsd:string"  />  
                <xsd:element name="Description" type="xsd:string"  />  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>  
 <xs:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    elementFormDefault="qualified"   
    xmlns:mstns="https://tempuri.org/XMLSchema.xsd"   
    xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" >  
    <xs:import   
namespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" />  
    <xs:element name="ProductDescription" type="ProductDescription" />  
        <xs:complexType name="ProductDescription">  
            <xs:sequence>  
                <xs:element name="Summary" type="Summary" minOccurs="0" />  
            </xs:sequence>  
            <xs:attribute name="ProductModelID" type="xs:string" />  
            <xs:attribute name="ProductModelName" type="xs:string" />  
        </xs:complexType>  
        <xs:complexType name="Summary" mixed="true" >  
            <xs:sequence>  
                <xs:any processContents="skip" namespace="http://www.w3.org/1999/xhtml" minOccurs="0" maxOccurs="unbounded" />  
            </xs:sequence>  
        </xs:complexType>  
</xs:schema>'  
;  
GO   
-- Clean up  
DROP XML SCHEMA COLLECTION ProductDescriptionSchemaCollection;  
GO  
```  
  
### <a name="c-importing-a-schema-that-does-not-specify-a-target-namespace"></a>C. Importando um esquema que não especifica um namespace de destino  
 Se um esquema que não contém um atributo **targetNamespace** for importado em uma coleção, seus componentes serão associados ao namespace de destino da cadeia de caracteres vazia, conforme mostrado no exemplo a seguir. A não associação de um ou mais esquemas importados na coleção resulta na associação de vários componentes de esquema (possivelmente não relacionados) ao namespace padrão da cadeia de caracteres vazia.  
  
```  
-- Create a collection that contains a schema with no target namespace.  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  xmlns:ns="http://ns">  
<element name="e" type="dateTime"/>  
</schema>';  
GO  
-- query will return the names of all the collections that   
--contain a schema with no target namespace  
SELECT sys.xml_schema_collections.name   
FROM   sys.xml_schema_collections   
JOIN   sys.xml_schema_namespaces   
ON     sys.xml_schema_collections.xml_collection_id =   
       sys.xml_schema_namespaces.xml_collection_id   
WHERE  sys.xml_schema_namespaces.name='';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Requisitos e limitações para o uso de Coleções de Esquemas XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
