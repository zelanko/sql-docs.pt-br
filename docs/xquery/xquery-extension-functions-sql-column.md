---
title: 'SQL: função de coluna () (XQuery) | Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:column function
- sql:column() function
ms.assetid: e8f67bdf-b489-49a9-9d0f-2069c1750467
author: rothja
ms.author: jroth
ms.openlocfilehash: df46abb8efdd5761797a599cf5a8cdebe02e5158
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946017"
---
# <a name="xquery-extension-functions---sqlcolumn"></a>Funções de Extensão XQuery – sql:column()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Conforme descrito no tópico [associando dados relacionais dentro de XML](../t-sql/xml/binding-relational-data-inside-xml-data.md), você pode usar a função **SQL: Column (()** ao usar [métodos de tipo de dados XML](../t-sql/xml/xml-data-type-methods.md) para expor um valor relacional dentro do XQuery.  
  
 Por exemplo, o [método Query () (tipo de dados XML)](../t-sql/xml/query-method-xml-data-type.md) é usado para especificar uma consulta em uma instância XML que é armazenada em uma variável ou coluna do tipo **XML** . Às vezes, você também pode desejar que sua consulta use valores de outra coluna que não seja XML, para agrupar dados relacionais e XML. Para fazer isso, use a função **SQL: Column ()** .  
  
 O valor SQL será mapeado para um valor correspondente XQuery e seu tipo será um tipo base XQuery equivalente ao tipo de SQL correspondente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sql:column("columnName")  
```  
  
## <a name="remarks"></a>Comentários  
 Observe que a referência a uma coluna especificada na função **SQL: Column ()** dentro de um XQuery refere-se a uma coluna na linha que está sendo processada.  
  
 No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você só pode fazer referência a uma instância **XML** no contexto da expressão de origem de uma instrução XML-DML insert; caso contrário, você não pode fazer referência a colunas que são do tipo **XML** ou um tipo CLR definido pelo usuário.  
  
 Não há suporte para a função **SQL: Column ()** em operações de junção. Em vez disso, pode ser usada a operação APPLY.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-sqlcolumn-to-retrieve-the-relational-value-inside-xml"></a>a. Usando sql:column() para recuperar o valor relacional no XML  
 Na construção de XML, o exemplo a seguir ilustra como você pode recuperar valores de uma coluna relacional não XML para associar dados relacionais e XML.  
  
 A consulta constrói XML que tenha a seguinte forma:  
  
```xml
<Product ProductID="771" ProductName="Mountain-100 Silver, 38" ProductPrice="3399.99" ProductModelID="19"   
  ProductModelName="Mountain 100" />  
```  
  
 Observe o seguinte no XML construído:  
  
-   Os valores de atributo **ProductID**, **ProductName**e **ProductPrice** são obtidos da tabela **Product** .  
  
-   O valor do atributo **ProductModelID** é recuperado da tabela **ProductModel** .  
  
-   Para tornar a consulta mais interessante, o valor do atributo **ProductModelName** é obtido da coluna **CatalogDescription** do **tipo XML**. Como as informações do catálogo de modelo do produto XML não são armazenadas para todos os modelos de produtos, a instrução `if` será usada para recuperar o valor somente se ele existir.  
  
    ```sql
    SELECT P.ProductID, CatalogDescription.query('  
    declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           <Product   
               ProductID=       "{ sql:column("P.ProductID") }"  
               ProductName=     "{ sql:column("P.Name") }"  
               ProductPrice=    "{ sql:column("P.ListPrice") }"  
               ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
               { if (not(empty(/pd:ProductDescription))) then  
                 attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
                else   
                   ()  
    }  
            </Product>  
    ') as Result  
    FROM Production.ProductModel PM, Production.Product P  
    WHERE PM.ProductModelID = P.ProductModelID  
    AND   CatalogDescription is not NULL  
    ORDER By PM.ProductModelID  
    ```  
  
 Observe o seguinte na consulta anterior:  
  
-   Como os valores são recuperados em duas tabelas diferentes, a cláusula FROM especifica duas tabelas. A condição na cláusula WHERE filtra o resultado e recupera apenas produtos cujos modelos de produto tenham descrições de catálogo.  
  
-   A palavra-chave **namespace** no [prólogo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define o prefixo do namespace XML, "PD", que é usado no corpo da consulta. Observe que os aliases de tabela, "P" e "PM", são definidos na cláusula FROM da própria consulta.  
  
-   A função **SQL: Column ()** é usada para trazer valores não XML dentro de XML.  
  
 Este é o resultado parcial:  
  
```  
ProductID               Result  
-----------------------------------------------------------------  
771         <Product ProductID="771"                   ProductName="Mountain-100 Silver, 38"   
                  ProductPrice="3399.99" ProductModelID="19"   
                  ProductModelName="Mountain 100" />  
...  
```  
  
 A consulta a seguir constrói XML que contenha informações específicas do produto. Tais informações incluem ProductID, ProductName, ProductPrice e, se disponível, ProductModelName de todos os produtos que pertencem a um modelo de produto específico, ProductModelID=19. Em seguida, o XML é atribuído @x à variável do tipo **XML** .  
  
```sql
declare @x xml  
SELECT @x = CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <Product   
           ProductID=       "{ sql:column("P.ProductID") }"  
           ProductName=     "{ sql:column("P.Name") }"  
           ProductPrice=    "{ sql:column("P.ListPrice") }"  
           ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
           { if (not(empty(/pd:ProductDescription))) then  
             attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
            else   
               ()  
}  
        </Product>  
')   
FROM Production.ProductModel PM, Production.Product P  
WHERE PM.ProductModelID = P.ProductModelID  
And P.ProductModelID = 19  
select @x  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de extensão SQL Server XQuery](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [Comparar XML digitado com XML não digitado](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Criar instâncias de dados XML](../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
