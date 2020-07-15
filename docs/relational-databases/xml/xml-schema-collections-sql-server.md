---
title: Coleções de esquema XML (SQL Server) | Microsoft Docs
description: Saiba como a coleção de esquema XML armazena esquemas XML importados para validar instâncias XML e digite os dados XML conforme eles são armazenados em um banco de dados do SQL Server.
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- xml_schema_namespace function
- XML schema collections [SQL Server], about XML schema collections
- metadata [SQL Server], XML schema collections
- queries [XML in SQL Server], XML schema collections
- schema collections [SQL Server]
- schemas [SQL Server], XML
- XML [SQL Server], schema collections
- XML schema collections [SQL Server]
- schema collections [SQL Server], about XML schema collections
ms.assetid: 659d41aa-ccec-4554-804a-722a96ef25c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2db7f06f0e68b1a03bf4b2a205666fcf90a58d32
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729770"
---
# <a name="xml-schema-collections-sql-server"></a>Coleções de esquema XML (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Como descrito no tópico [xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md), o SQL Server fornece armazenamento nativo de dados XML por meio do tipo de dados **xml**. Opcionalmente, é possível associar esquemas XSD a uma variável ou a uma coluna do tipo **xml** por meio de uma coleção de esquemas XML. A coleção de esquema XML armazena os esquemas XML importados e, em seguida, é usada para fazer o seguinte:  
  
-   Validar instâncias XML  
  
-   Definir o tipo dos dados XML conforme eles são armazenados no banco de dados  
  
 Observe que a coleção de esquema XML é uma entidade de metadados como uma tabela no banco de dados. É possível criar, modificar e descartá-la. Esquemas especificados em uma instrução [CREATE XML SCHEMA COLLECTION (Transact-SQL)](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) são importadas automaticamente no objeto da coleção de esquema XML recém-criado. É possível importar esquemas adicionais ou componentes do esquema em um objeto de coleção existente no banco de dados usando a instrução [ALTER XML SCHEMA COLLECTION (Transact-SQL)](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) .  
  
 Como descrito no tópico, [XML com tipo vs. sem tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md), o XML armazenado em uma coluna ou variável à qual um esquema está associado é denominado XML **com tipo** porque o esquema fornece as informações necessárias do tipo de dados para os dados da instância. O SQL Server usa essas informações de tipo para otimizar o armazenamento de dados.  
  
 O mecanismo do processamento de consultas também usa o esquema para verificação de tipo e otimizar modificação de dados e consultas.  
  
 Além disso, o SQL Server usa a coleção de esquema XML associada, no caso de **xml**com tipo para validar a instância XML. Se a instância XML estiver de acordo com o esquema, o banco de dados permitirá que a instância seja armazenada no sistema com suas informações de tipo. Caso contrário, a instância será rejeitada.  
  
 É possível usar a função intrínseca XML_SCHEMA_NAMESPACE para recuperar a coleção de esquema que está armazenada no banco de dados. Para obter mais informações, veja [Exibir uma coleção de esquemas XML armazenados](../../relational-databases/xml/view-a-stored-xml-schema-collection.md).  
  
 Também é possível usar a coleção de esquema XML para digitar variáveis, parâmetros e colunas XML.  
  
##  <a name="ddl-for-managing-schema-collections"></a><a name="ddl"></a> DDL para gerenciar coleções de esquemas  
 Você pode criar coleções de esquemas XML no banco de dados e associá-las a variáveis e colunas do tipo **xml** . Para gerenciar coleções de esquema no banco de dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece as seguintes instruções DDL:  
  
-   [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) Importa os componentes de esquema para um banco de dados.  
  
-   [ALTER XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) Modifica os componentes de esquema em uma coleção de esquema XML existente.  
  
-   [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md) Exclui uma coleção de esquema XML completa e todos os seus componentes.  
  
 Para usar uma coleção de esquema XML e os esquemas contidos nela, você deve primeiro criar a coleção e os esquemas usando a instrução CREATE XML SCHEMA COLLECTION. Após a criação da coleção de esquema, é possível criar variáveis e colunas do tipo **xml** e associar a coleção de esquema a elas. Observe que depois que uma coleção de esquema é criada, são armazenados vários componentes de esquema nos metadados. Também é possível usar ALTER XML SCHEMA COLLECTION para adicionar mais componentes a esquemas existentes ou adicionar novos esquemas a uma coleção existente.  
  
 Para descartar a coleção de esquema, use a instrução DROP XML SCHEMA COLLECTION. Ela descarta todos os esquemas que estão contidos na coleção e remove o objeto da coleção. Observe que, antes de conseguir remover uma coleção de esquema, as condições descritas em [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md) deverão ser atendidas.  
  
##  <a name="understanding-schema-components"></a><a name="components"></a> Compreendendo componentes de esquema  
 Quando a instrução CREATE XML SCHEMA COLLECTION é usada, vários componentes de esquema são importados no banco de dados. Os componentes de esquema incluem elementos, atributos e definições de tipo de esquema. Quando a instrução DROP XML SCHEMA COLLECTION é usada, a coleção completa é removida.  
  
 CREATE XML SCHEMA COLLECTION salva os componentes do esquema em várias tabelas do sistema.  
  
 Por exemplo, considere o seguinte esquema:  
  
```xml
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            targetNamespace="uri:Cust_Orders2"  
            xmlns="uri:Cust_Orders2" >  
  <xsd:attribute name="SomeAttribute" type="xsd:int" />  
  <xsd:complexType name="SomeType" />  
  <xsd:complexType name="OrderType" >  
    <xsd:sequence>  
      <xsd:element name="OrderDate" type="xsd:date" />  
      <xsd:element name="RequiredDate" type="xsd:date" />  
      <xsd:element name="ShippedDate" type="xsd:date" />  
    </xsd:sequence>  
    <xsd:attribute name="OrderID" type="xsd:ID" />  
    <xsd:attribute name="CustomerID"  />  
    <xsd:attribute name="EmployeeID"  />  
  </xsd:complexType>  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order" type="OrderType"  
                     maxOccurs="unbounded" />  
       </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
      <xsd:attribute name="OrderIDList" type="xsd:IDREFS" />  
  </xsd:complexType>  
  <xsd:element name="Customer" type="CustomerType" />  
</xsd:schema>  
```  
  
 O esquema anterior mostra os diferentes tipos de componentes que podem ser armazenados no banco de dados. Esses esquemas incluem `SomeAttribute`, `SomeType`, `OrderType`, `CustomerType`, `Customer`, `Order`, `CustomerID`, `OrderID`, `OrderDate`, `RequiredDate`e `ShippedDate`.  
  
### <a name="component-categories"></a>Categorias de componentes  
 Os componentes de esquema armazenados no banco de dados se enquadram nas seguintes categorias:  
  
-   ELEMENT  
  
-   ATTRIBUTE  
  
-   TYPE (para tipos simples ou complexos)  
  
-   ATTRIBUTEGROUP  
  
-   MODELGROUP  
  
 Por exemplo:  
  
-   **SomeAttribute** é um componente de ATTRIBUTE.  
  
-   **SomeType**, **OrderType**e **CustomerType** são componentes de TYPE.  
  
-   **Customer** é um componente de ELEMENT.  
  
 Quando você importa um esquema no banco de dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não armazena o próprio esquema. Em vez disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena os vários componentes individuais. Ou seja, a marca \<Schema> não é armazenada, apenas os componentes que estão definidos dentro dela são preservados. Todos os elementos do esquema não são preservados. Se a marca \<Schema> contiver atributos que especificam o comportamento padrão dos componentes dela, eles serão movidos para os componentes do esquema dentro dela durante o processo de importação, conforme mostrado na tabela a seguir.  
  
|Nome do atributo|Comportamento|  
|--------------------|--------------|  
|**attributeFormDefault**|O atributo **form** aplicado a todas as declarações de atributo no esquema em que ele ainda não está presente e o valor é definido como o valor do atributo **attributeFormDefault** .|  
|**elementFormDefault**|O atributo **form** aplicado a todas as declarações de elemento no esquema em que ele ainda não está presente e o valor é definido como o valor do atributo **elementFormDefault** .|  
|**blockDefault**|O atributo **block** aplicado a todas as declarações de elemento e às definições de tipo em que ele ainda não está presente e o valor é definido como o valor do atributo **blockDefault** .|  
|**finalDefault**|O atributo **final** aplicado a todas as declarações de elemento e às definições de tipo em que ele ainda não está presente e o valor está definido como o valor do atributo **finalDefault** .|  
|**targetNamespace**|Informações sobre os componentes que pertencem ao namespace de destino são armazenadas nos metadados.|  
| &nbsp; | &nbsp; |
  
##  <a name="permissions-on-an-xml-schema-collection"></a><a name="perms"></a> Permissões em uma coleção de esquema XML  
 Você deve ter as permissões necessárias para fazer o seguinte:  
  
-   Criar/carregar a coleção de esquema XML  
  
-   Modificar a coleção de esquema XML  
  
-   Descartar a coleção de esquema XML  
  
-   Usar a coleção de esquema XML para digitar colunas, variáveis e parâmetros de tipo **xml** ou usá-la em restrições de tabela ou coluna  
  
 O modelo de segurança do SQL permite a permissão CONTROL em todos os objetos. O usuário autorizado dessa permissão obtém todas as outras permissões no objeto. O proprietário do objeto também tem todas as permissões no objeto.  
  
 O proprietário e o usuário autorizado da permissão CONTROL em um objeto podem conceder qualquer permissão no objeto. Um usuário que não é um proprietário e não tem a permissão CONTROL ainda pode conceder permissão em um objeto quando WITH GRANT OPTION estiver especificada. Por exemplo, assuma que o Usuário A tem a permissão REFERENCES na coleção de esquema XML S, através da WITH GRANT OPTION, mas nenhuma outra permissão em S. O Usuário A pode conceder a permissão REFERENCES ao Usuário B na coleção de esquema S.  
  
 O modelo de segurança também permite permissões para criar e usar coleções de esquema XML ou transferir a propriedade de um usuário para outro. Os tópicos a seguir descrevem as permissões de coleção de esquema XML.  
  
-   [Conceder permissões em uma Coleção de Esquemas XML](../../relational-databases/xml/grant-permissions-on-an-xml-schema-collection.md)  
  
     Este tópico discute como conceder permissões para criar uma coleção de esquema XML e como conceder permissões em um objeto de coleção de esquema XML.  
  
-   [Revogar permissões em uma Coleção de Esquemas XML](../../relational-databases/xml/revoke-permissions-on-an-xml-schema-collection.md)  
  
     Este tópico discute como a revogação de permissões pode ser usada para evitar a criação de uma coleção de esquema XML e como revogar permissões em um objeto de coleção de esquema XML.  
  
-   [Recusar permissões em uma Coleção de Esquemas XML](../../relational-databases/xml/deny-permissions-on-an-xml-schema-collection.md)  
  
     Este tópico discute como negar permissões para criar uma coleção de esquema XML e como negar permissões em um objeto de coleção de esquema XML.  
  
##  <a name="getting-information-about-xml-schemas-and-schema-collections"></a><a name="info"></a> Adquirindo Informações sobre esquemas XML e coleções de esquemas  
 Coleções de esquema XML são enumeradas na exibição do catálogo sys.xml_schema_collections. A coleção de esquema XML "sys" está definida pelo sistema. Ela contém os namespaces predefinidos que podem ser usados em todas as coleções de esquema XML definidas pelo usuário sem precisar carregá-las explicitamente. Essa lista contém os namespaces para xml, xs, xsi, fn e xdt. Duas outras exibições do catálogo são sys.xml_schema_namespaces, que enumera todos os namespaces dentro de cada coleção de esquema XML, e sys.xml_components, que enumera todos os componentes do esquema XML dentro de cada esquema XML.  
  
 A função interna **XML_SCHEMA_NAMESPACE**, *schemaName, XmlSchemacollectionName, namespace-uri*, produz uma instância de tipo de dados **xml**. Essa instância contém fragmentos de esquema XML estão contidos em uma coleção de esquema XML, exceto os esquemas XML predefinidos.  
  
 É possível enumerar o conteúdo de uma coleção de esquema XML das seguintes maneiras:  
  
-   Escreva consultas Transact-SQL nas exibições do catálogo apropriadas para coleções de esquema XML.  
  
-   Use a função interna **XML_SCHEMA_NAMESPACE()** . É possível aplicar métodos de tipo de dados **xml** na saída dessa função. No entanto não é possível modificar os esquemas XML subjacentes.  
  
 Esses são ilustrados nos exemplos a seguir.  
  
### <a name="example-enumerate-the-xml-namespaces-in-an-xml-schema-collection"></a>Exemplo: Enumerar os namespaces XML em uma coleção de esquemas XML  
 Use a consulta a seguir para a coleção de esquema XML "myCollection":  
  
```sql
SELECT XSN.name  
FROM    sys.xml_schema_collections XSC JOIN sys.xml_schema_namespaces XSN  
    ON (XSC.xml_collection_id = XSN.xml_collection_id)  
WHERE    XSC.name = 'myCollection'     
```  
  
### <a name="example-enumerate-the-contents-of-an-xml-schema-collection"></a>Exemplo: Enumerar o conteúdo de uma coleção de esquemas XML  
 A instrução a seguir enumera o conteúdo da coleção de esquema XML "myCollection" dentro do esquema relacional dbo.  
  
```sql
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection')  
```  
  
 Esquemas XML individuais dentro da coleção podem ser obtidos como instâncias de tipo de dados **xml** especificando o namespace de destino como o terceiro argumento para **XML_SCHEMA_NAMESPACE()** . Isso é mostrado no exemplo a seguir.  
  
### <a name="example-output-a-specified-schema-from-an-xml-schema-collection"></a>Exemplo: Gerar um esquema especificado com base em uma coleção de esquemas XML  
 A instrução a seguir produz o esquema XML com o namespace de destino _pretend_ https/\/www.microsoft.com/was-books from the XML schema collection "myCollection" dentro do esquema relacional dbo.  
  
```sql
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection',   
N'https://www.microsoft.com/was-books')  
```  
  
### <a name="querying-xml-schemas"></a>Consultando esquemas XML  
 É possível consultar esquemas XML carregados em coleções de esquema XML das seguintes maneiras:  
  
-   Escreva consultas Transact-SQL em exibições do catálogo para namespaces de esquema XML.  
  
-   Crie uma tabela que contém uma coluna de tipo de dados **xml** para armazenar seus esquemas XML e também para carregá-los no sistema de tipo XML. É possível consultar a coluna XML usando os métodos de tipo de dados **xml** . Além disso, é possível construir um índice XML nessa coluna. No entanto, com essa abordagem, o aplicativo deve manter consistência entre os esquemas XML armazenados na coluna XML e no sistema de tipo XML. Por exemplo, se você descartar o namespace do esquema XML do sistema de tipo XML, também deverá descartá-lo da tabela para preservar a consistência.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir uma coleção de esquemas XML armazenados](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [Pré-processar um esquema para mesclar esquemas incluídos](../../relational-databases/xml/preprocess-a-schema-to-merge-included-schemas.md)   
 [Requisitos e limitações para o uso de Coleções de Esquemas XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
