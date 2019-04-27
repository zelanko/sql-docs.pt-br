---
title: Criar instâncias de dados XML | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- type casting string instances [XML in SQL Server]
- XML [SQL Server], typed
- xml data type [SQL Server], generating instances
- casting string instances [XML in SQL Server]
- typed XML
- generating XML instances [SQL Server]
- XML [SQL Server], generating instances
- white space [XML in SQL Server]
ms.assetid: dbd6c06f-db6e-44a7-855a-6a55bf374907
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae842748d2d510c5c00f329f5e28cd49a0c86ef3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637604"
---
# <a name="create-instances-of-xml-data"></a>Criar instâncias de dados XML
  Este tópico descreve como gerar instâncias XML.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode gerar instâncias XML das seguintes maneiras:  
  
-   Instâncias de cadeia de caracteres de conversão de tipos.  
  
-   Usando a instrução SELECT com a cláusula FOR XML.  
  
-   Usando atribuições de constantes.  
  
-   Usando carregamento em massa.  
  
## <a name="type-casting-string-and-binary-instances"></a>Instâncias de cadeia de caracteres de conversão de tipos e binárias  
 Você pode analisar qualquer um dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados de cadeia de caracteres como [**n**] [**var**]**char**, **texto de [n]**,  **varbinary**, e **imagem**, para o `xml` tipo de dados, convertendo (CAST) ou convertendo (CONVERT) a cadeia de caracteres para o `xml` tipo de dados. XML sem-tipo é verificado para confirmar se está bem formado. Se não houver um esquema associado a `xml` tipo, validação também é executado. Para obter mais informações, consulte [Comparar XML digitado com XML não digitado](compare-typed-xml-to-untyped-xml.md).  
  
 Documentos de XML podem ser codificados com diferentes codificações (por exemplo, UTF-8, UTF-16, Windows-1252). O seguinte descreve as regras de como os tipos de origem de cadeia de caracteres e binários interagem com a codificação do documento XML e como o analisador se comporta.  
  
 Como **nvarchar** pressupõe uma codificação Unicode de dois bytes, como UTF-16 ou UCS-2, o analisador XML tratará o valor da cadeia de caracteres como um documento ou fragmento XML codificado em Unicode de dois bytes. Isso indica que o documento XML precisa ser codificado em uma codificação Unicode bem como ser compatível com o tipo de dados da origem Um documento XML codificado em UTF-16 pode ter uma BOM (marca de ordem de byte), mas isso não é necessário, pois o contexto do tipo de origem torna claro que ele pode ser apenas um documento codificado em Unicode de dois bytes.  
  
 O conteúdo de uma cadeia de caracteres **varchar** é tratado como um documento/fragmento XML codificado em um byte pelo analisador XML. Como a cadeia de caracteres de origem **varchar** tem uma página de código associada, o analisador usará essa página de código para a codificação, se nenhuma codificação explícita for especificada no próprio XML. Se uma instância XML tiver uma BOM ou uma declaração de codificação, a BOM ou declaração precisará ser consistente com a página de código, caso contrário o analisador relatará um erro.  
  
 O conteúdo de **varbinary** é tratado como um fluxo de codepoint que é passado diretamente ao analisador XML. Assim, o documento ou fragmento XML precisa fornecer a BOM ou outras informações embutidas de codificação. O analisador examinará o fluxo apenas para determinar a codificação. Isso significa que XML codificado em UTF-16 precisa fornecer a BOM de UTF-16 e que uma instância sem BOM e sem uma codificação de declaração será interpretada como UTF-8.  
  
 Se a codificação do documento XML não for conhecida antecipadamente e os dados forem passados como cadeias de caracteres ou binários em vez de dados XML antes da conversão em XML, será recomendável tratar os dados como **varbinary**. Por exemplo, ao ler dados de um arquivo XML usando OpenRowset(), deve-se especificar os dados a serem lidos como um valor **varbinary(max)** :  
  
```  
select CAST(x as XML)   
from OpenRowset(BULK 'filename.xml', SINGLE_BLOB) R(x)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] representa XML internamente em uma representação binária eficiente que usa codificação UTF-16. A codificação fornecida pelo usuário não é preservada, mas é considerada durante o processo de análise.  
  
### <a name="type-casting-clr-user-defined-types"></a>Tipos de dado CLR definidos pelo usuário para conversão de tipo  
 Se um tipo de dado CLR definido pelo usuário tiver uma serialização XML, as instâncias daquele tipo poderão ser convertidas explicitamente em um tipo de dados XML. Para obter mais detalhes sobre serialização XML de um tipo da dado CLR definido pelo usuário, consulte [Serialização XML de objetos de banco de dados CLR](../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md).  
  
### <a name="white-space-handling-in-typed-xml"></a>Tratamento de espaço em branco em XML com tipo  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], espaço em branco dentro do conteúdo do elemento será considerado insignificante se ele ocorrer dentro de uma sequência de dados de caracteres de apenas espaço em branco delimitada por marcação, como marcas de início e de fim, e não tiver a entidade definida. (Seções de CDATA são ignoradas.) Esse tratamento de espaço em branco é diferente de como o espaço em branco é descrito na especificação do XML 1.0 publicada pelo World Wide Web Consortium (W3C). Isso é porque o analisador XML no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhece apenas um número limitado de subconjuntos de DTD, conforme definido no XML 1.0. Para obter mais informações sobre os subconjuntos de DTD limitados que têm suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [CAST e CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
 Por padrão, o analisador XML descarta espaço em branco insignificante quando converte dados de cadeia de caracteres em XML se uma das seguintes situações for verdadeira:  
  
-   `The xml:space` o atributo não está definido em um elemento ou em seus elementos ancestrais.  
  
-   O atributo `xml:space` em efeito em um elemento ou em um de seus elementos ancestrais tem o valor de padrão.  
  
 Por exemplo:   
  
```  
declare @x xml  
set @x = '<root>      <child/>     </root>'  
select @x   
```  
  
 Esse é o resultado:  
  
```  
<root><child/></root>  
```  
  
 Porém, é possível alterar esse comportamento. Para preservar espaço em branco para uma instância DT XML, use o operador CONVERT e seu parâmetro opcional *style* definido como um valor de 1. Por exemplo:  
  
```  
SELECT CONVERT(xml, N'<root>      <child/>     </root>', 1)  
```  
  
 Se o parâmetro *style* não for usado ou seu valor estiver definido como 0, espaço em branco insignificante não será preservado para a conversão da instância DT xml. Para obter mais informações sobre como usar o operador CONVERT e seu parâmetro *style* ao converter dados de cadeia de caracteres em instâncias DT xml, consulte [CAST and CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
### <a name="example-cast-a-string-value-to-typed-xml-and-assign-it-to-a-column"></a>Exemplo: Converter um valor de cadeia de caracteres em xml tipado e atribuí-lo a uma coluna  
 O exemplo a seguir converte uma variável de cadeia de caracteres que contém um fragmento XML para o `xml` tipo de dados e, em seguida, armazena-o no `xml` coluna de tipo:  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
go  
DECLARE  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
```  
  
 A operação de inserção a seguir converte implicitamente de uma cadeia de caracteres para o `xml` tipo:  
  
```  
INSERT INTO T VALUES (3, @s)   
```  
  
 Você pode explicitamente cast () a cadeia de caracteres para o `xml` tipo:  
  
```  
INSERT INTO T VALUES (3, cast (@s as xml))  
```  
  
 Ou é possível usar convert(), conforme mostrado a seguir:  
  
```  
INSERT INTO T VALUES (3, convert (xml, @s))   
```  
  
### <a name="example-convert-a-string-to-typed-xml-and-assign-it-to-a-variable"></a>Exemplo: Converter uma cadeia de caracteres em xml tipado e atribuí-lo a uma variável  
 No exemplo a seguir, uma cadeia de caracteres é convertida `xml` de tipo e atribuído a uma variável do `xml` tipo de dados:  
  
```  
declare @x xml  
declare  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
set @x =convert (xml, @s)  
select @x  
```  
  
## <a name="using-the-select-statement-with-a-for-xml-clause"></a>Usando a instrução SELECT com a cláusula FOR XML  
 É possível usar a cláusula FOR XML em uma instrução SELECT para retornar resultados como XML. Por exemplo:  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = (SELECT Column1, Column2  
               FROM   Table1, Table2  
               WHERE   Some condition  
               FOR XML AUTO)  
 ...  
```  
  
 A instrução SELECT retorna um fragmento XML textual que, em seguida, é analisado durante a atribuição para o `xml` variável de tipo de dados.  
  
 Você também pode usar o [diretiva TYPE](type-directive-in-for-xml-queries.md) na cláusula FOR XML que retorna um FOR XML diretamente como resultado da consulta `xml` tipo:  
  
```  
Declare @xmlDoc xml  
SET @xmlDoc = (SELECT ProductModelID, Name  
               FROM   Production.ProductModel  
               WHERE  ProductModelID=19  
               FOR XML AUTO, TYPE)  
SELECT @xmlDoc  
```  
  
 Esse é o resultado:  
  
```  
<Production.ProductModel ProductModelID="19" Name="Mountain-100" />...  
```  
  
 No exemplo a seguir, a tipado `xml` resultado de uma consulta FOR XML é inserido em um `xml` coluna de tipo:  
  
```  
CREATE TABLE T1 (c1 int, c2 xml)  
go  
INSERT T1(c1, c2)  
SELECT 1, (SELECT ProductModelID, Name  
           FROM Production.ProductModel  
           WHERE ProductModelID=19  
           FOR XML AUTO, TYPE)  
SELECT * FROM T1  
go  
```  
  
 Para obter mais informações sobre FOR XML, consulte [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md).  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna instâncias de tipo de dados `xml`ao cliente como um resultado das diferentes construções do servidor como consultas FOR XML que usam a diretiva TYPE ou onde o tipo de dados `xml` é usado para retornar XML de colunas, variáveis e parâmetros de saída SQL. No código do aplicativo cliente, o provedor ADO.NET solicita que essas informações de tipo de dados `xml` sejam enviadas em uma codificação binária do servidor. Porém, se você estiver usando FOR XML sem a diretiva TYPE, os dados XML retornarão como um tipo de cadeia de caracteres. De qualquer forma, o provedor cliente sempre poderá controlar qualquer formulário de XML.  
  
## <a name="using-constant-assignments"></a>Usando atribuições de constantes  
 Uma constante de cadeia de caracteres pode ser usada onde uma instância das `xml` tipo de dados é esperado. Isso é o mesmo que uma CAST implícita de cadeia de caracteres em XML. Por exemplo:   
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
-- Or  
SET @xmlDoc = N'<?xml version="1.0" encoding="ucs-2"?><doc/>'  
```  
  
 O exemplo anterior converte implicitamente a cadeia de caracteres para o `xml` tipo de dados e atribui a um `xml` variável de tipo.  
  
 O exemplo a seguir insere uma cadeia de caracteres constante em um `xml` coluna de tipo:  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
INSERT INTO T VALUES (3, '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>')   
```  
  
> [!NOTE]  
>  Para XML com tipo, o XML é validado em relação ao esquema especificado. Para obter mais informações, consulte [Comparar XML digitado com XML não digitado](compare-typed-xml-to-untyped-xml.md).  
  
## <a name="using-bulk-load"></a>Usando carregamento em massa  
 A funcionalidade [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql) aprimorada permite carregar documentos XML em massa no banco de dados. Você pode carregar instâncias XML em massa de arquivos no `xml` colunas de tipo no banco de dados. Para obter exemplos de funcionamento, consulte [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md). Para obter mais informações sobre carregamento de documentos XML, consulte [Carregar dados XML](load-xml-data.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Recuperar e consultar dados XML](retrieve-and-query-xml-data.md)|Descreve as partes de instâncias XML que não são preservadas quando são armazenadas em bancos de dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Comparar XML digitado com XML não digitado](compare-typed-xml-to-untyped-xml.md)   
 [Métodos de tipo de dados xml](/sql/t-sql/xml/xml-data-type-methods)   
 [Linguagem de modificação de dados XML &#40;XML DML&#41;](/sql/t-sql/xml/xml-data-modification-language-xml-dml)   
 [Dados XML &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
