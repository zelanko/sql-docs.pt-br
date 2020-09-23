---
description: Método consulta() (Tipo de dados xml)
title: Método consulta() (Tipo de dados xml)
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query method
- query() method
ms.assetid: f48f6f7b-219f-463a-bf36-bc10f21afaeb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: af8a312db85630c9f7e527b47ad876daf9520eef
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116604"
---
# <a name="query-method-xml-data-type"></a>Método consulta() (Tipo de dados xml)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Especifica uma consulta XQuery em instância do tipo de dados **xml**. O resultado é do tipo **xml**. O método retorna uma instância de XML sem-tipo.  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
query ('XQuery')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
XQuery  
É uma cadeia de caracteres, uma expressão XQuery, que consulta nós XML, como elementos e atributos, em uma instância XML.  
  
## <a name="examples"></a>Exemplos  
Esta seção fornece exemplos de uso do método query() do tipo de dados **xml**.  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>a. Usando o método query() em relação a uma variável de tipo xml  
O exemplo a seguir declara uma variável **\@myDoc** do tipo **xml** e atribui uma instância XML a essa variável. O método **query()** é, em seguida, usado para especificar uma consulta XQuery no documento.  
  
A consulta recupera o elemento filho <`Features`> do elemento <`ProductDescription`>:  
  
```sql
DECLARE @myDoc XML  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc.query('/Root/ProductDescription/Features')  
```  
  
A saída a seguir mostra o resultado:  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### <a name="b-using-the-query-method-against-an-xml-type-column"></a>B. Usando o método query() em relação a uma coluna do tipo XML  
No seguinte exemplo, o método **query()** é usado para especificar uma consulta XQuery na coluna **CatalogDescription** do tipo **xml** no banco de dados **AdventureWorks**:  
  
```sql
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
Observe os seguintes itens na consulta anterior:  
  
-   A coluna CatalogDescription é uma coluna **xml** digitada, o que significa que tem uma coleção de esquemas associada a ela. No [Prólogo do XQuery](../../xquery/modules-and-prologs-xquery-prolog.md), a palavra-chave **namespace** define o prefixo que é usado posteriormente no corpo da consulta.  
  
-   O método **query()** constrói o XML, um elemento <`Product`> que tem um atributo **ProductModelID**, no qual o valor do atributo **ProductModelID** é recuperado do banco de dados. Para obter mais informações sobre a construção de XML, consulte [Construção de XML &#40;XQuery&#41;](../../xquery/xml-construction-xquery.md).  
  
-   O [método exist() (tipo de dados XML)](../../t-sql/xml/exist-method-xml-data-type.md) na cláusula WHERE localiza somente as linhas que contêm o elemento <`Warranty`> no XML. Novamente, a palavra-chave **namespace** define dois prefixos de namespace.  
  
A saída a seguir mostra o resultado parcial:  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
Observe que os métodos query() e exist() declaram o prefixo PD. Nesses casos, você pode usar WITH XMLNAMESPACES para definir primeiro os prefixos e usá-los na consulta.  
  
```sql
WITH XMLNAMESPACES 
(  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM
)  
SELECT CatalogDescription.query('<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />')
       AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/PD:ProductDescription/PD:Features/WM:Warranty ') = 1;
```  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
