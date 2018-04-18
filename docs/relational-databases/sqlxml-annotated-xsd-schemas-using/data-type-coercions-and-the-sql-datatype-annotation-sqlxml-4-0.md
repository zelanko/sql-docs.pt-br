---
title: 'Coerções de tipo de dados e o SQL: DataType anotação (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- type attribute
- sql:datatype
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- xsd:type
- datatype annotation
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XSD schemas [SQLXML], mapping data types
ms.assetid: db192105-e8aa-4392-b812-9d727918c005
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8a2dc2c3d91eea67e9e08a87d5aa7735a1b45b1f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>Coerções de tipo de dados e a anotação de sql:datatype (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Em um esquema XSD, o **xsd: Type** atributo especifica o tipo de dados XSD de um elemento ou atributo. Quando um esquema XSD é usado para extrair dados do banco de dados, o tipo de dados especificado é usado para formatar os dados.  
  
 Além de especificar um tipo XSD em um esquema, você também pode especificar um Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados usando o **SQL: DataType** anotação. O **xsd: Type** e **SQL: DataType** atributos controlam o mapeamento entre tipos de dados XSD e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.  
  
## <a name="xsdtype-attribute"></a>Atributo xsd:type  
 Você pode usar o **xsd: Type** atributo para especificar o tipo de dados XML de um atributo ou elemento que mapeia para uma coluna. O **xsd: Type** afeta o documento que é retornado do servidor e também a consulta XPath que é executada. Quando uma consulta XPath é executada em um esquema de mapeamento contém **xsd: Type**, XPath usa o tipo de dados especificado ao processar a consulta. Para obter mais informações sobre como XPath usa **xsd: Type**, consulte [mapeamento de tipos de dados XSD para tipos de dados XPath &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md).  
  
 Em um documento retornado, todos os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são convertidos em representações de cadeia de caracteres. Alguns tipos de dados exigem conversões adicionais. A tabela a seguir lista as conversões que são usadas para várias **xsd: Type** valores.  
  
|Tipo de dados XSD|Conversão do SQL Server|  
|-------------------|---------------------------|  
|Booliano|CONVERT(bit, COLUMN)|  
|Data|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|Decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|Hora|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|Todos os outros|Nenhuma conversão adicional|  
  
> [!NOTE]  
>  Alguns dos valores retornados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode não ser compatível com os tipos de dados XML que são especificados usando **xsd: Type**, porque a conversão não é possível (por exemplo, converter "XYZ" em um  **decimal** tipo de dados) ou porque o valor excede o intervalo desse tipo de dados (por exemplo, -100000 convertido em um **UnsignedShort** tipo XSD). Conversões de tipo incompatíveis podem resultar em documentos XML que não são válidos ou em erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>Mapeando dos tipos de dados do SQL Server para os tipos de dados XSD  
 A seguinte tabela mostra um mapeamento óbvio de tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tipos de dados XSD. Se você souber o tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta tabela fornecerá o tipo XSD correspondente que você pode especificar no esquema XSD.  
  
|Tipo de dados do SQL Server|Tipo de dados XSD|  
|--------------------------|-------------------|  
|**bigint**|**long**|  
|**binary**|**base64Binary**|  
|**bit**|**booleano**|  
|**char**|**cadeia de caracteres**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**image**|**base64Binary**|  
|**Int**|**Int**|  
|**money**|**decimal**|  
|**nchar**|**cadeia de caracteres**|  
|**ntext**|**cadeia de caracteres**|  
|**nvarchar**|**cadeia de caracteres**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**smallint**|**short**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**cadeia de caracteres**|  
|**sysname**|**cadeia de caracteres**|  
|**text**|**cadeia de caracteres**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**unsignedByte**|  
|**varbinary**|**base64Binary**|  
|**varchar**|**cadeia de caracteres**|  
|**uniqueidentifier**|**cadeia de caracteres**|  
  
## <a name="sqldatatype-annotation"></a>Anotação sql:datatype  
 O **SQL: DataType** anotação é usada para especificar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados; essa anotação deve ser especificado quando:  
  
-   Você está carregando em massa em uma **dateTime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coluna a partir de um XSD **dateTime**, **data**, ou **tempo** tipo. Nesse caso, você deve identificar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tipo de dados de coluna usando **SQL: DataType = "dateTime"**. Esta regra também se aplica a diagramas de atualização.  
  
-   Você está carregando em massa em uma coluna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **uniqueidentifier** tipo e o valor XSD é um GUID que inclui chaves ({e}). Quando você especifica **SQL: DataType = "uniqueidentifier"**, as chaves são removidas do valor antes que ele seja inserido na coluna. Se **SQL: DataType** não for especificado, o valor é enviado com as chaves e a inserção ou atualização falhará.  
  
-   O tipo de dados XML **base64Binary** mapeado para vários [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados (**binário**, **imagem**, ou **varbinary**). Para mapear o tipo de dados XML **base64Binary** para um determinado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados, use o **SQL: DataType** anotação. Essa anotação especifica o tipo de dados explícito do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da coluna para a qual o atributo é mapeado. Isto é útil quando os dados estão sendo armazenados nos bancos de dados. Especificando o **SQL: DataType** anotação, você pode identificar explícita [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  
  
 Geralmente é recomendável que você especifique **SQL: DataType** no esquema.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [requisitos para executar exemplos do SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-xsdtype"></a>A. Especificando xsd:type  
 Este exemplo mostra como um XSD **data** tipo é especificado usando o **xsd: Type** atributo no esquema afeta o documento XML resultante. O esquema fornece uma exibição XML da tabela Sales.SalesOrderHeader no banco de dados AdventureWorks.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader">  
     <xsd:complexType>  
       <xsd:attribute name="SalesOrderID" type="xsd:string" />   
       <xsd:attribute name="CustomerID"   type="xsd:string" />   
       <xsd:attribute name="OrderDate"    type="xsd:date" />   
       <xsd:attribute name="DueDate"  />   
       <xsd:attribute name="ShipDate"  type="xsd:time" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Nesse esquema de XSD, há três atributos que retornam um valor de data de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o esquema:  
  
-   Especifica **xsd: Type = data** no **OrderDate** de atributo, a parte de data do valor retornado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o **OrderDate** atributo será exibido.  
  
-   Especifica **xsd: Type = hora** no **ShipDate** de atributo, a parte de hora do valor retornado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o **ShipDate** atributo será exibido.  
  
-   Não especifique **xsd: Type** no **DueDate** de atributo, o mesmo valor que é retornado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é exibido.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como xsdType.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como xsdTypeT.xml no mesmo diretório onde você salvou xsdType.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="xsdType.xml">  
        /Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (xsdType.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\xsdType.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43659"   
         CustomerID="676"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
  <Order SalesOrderID="43660"   
         CustomerID="117"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
 ...  
</ROOT>  
```  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader">  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="CustomerID"  />  
    <AttributeType name="OrderDate" dt:type="date" />  
    <AttributeType name="DueDate" />  
    <AttributeType name="ShipDate" dt:type="time" />  
  
    <attribute type="SalesOrderID" sql:field="OrderID" />  
    <attribute type="CustomerID" sql:field="CustomerID" />  
    <attribute type="OrderDate" sql:field="OrderDate" />  
    <attribute type="DueDate" sql:field="DueDate" />  
    <attribute type="ShipDate" sql:field="ShipDate" />  
</ElementType>  
</Schema>  
```  
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>B. Especificando o tipo de dados de SQL usando sql:datatype  
 Para obter um exemplo de funcionamento, consulte o exemplo G em [exemplos de carregamento em massa XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md). Nesse exemplo, um valor de GUID que inclui "{" e "}" é carregado em massa. Especifica o esquema neste exemplo **SQL: DataType** para identificar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tipo de dados como **uniqueidentifier**. Este exemplo ilustra quando **SQL: DataType** deve ser especificado no esquema.  
  
  
