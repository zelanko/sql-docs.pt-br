---
title: Casos de uso gerais do XQuery | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e844425f0c512cfe7c15354bf1aeb100d6104e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68004528"
---
# <a name="general-xquery-use-cases"></a>Casos gerais de uso de XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico fornece exemplos gerais de uso de XQuery.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>a. Consultar descrições de catálogo para localizar produtos e pesos  
 A consulta a seguir retorna as IDs e os pesos de modelo do produto , se existentes, da descrição do catálogo de produtos. A consulta constrói XML que tenha a seguinte forma:  
  
```  
<Product ProductModelID="...">  
  <Weight>...</Weight>  
</Product>  
```  
  
 Esta é a consulta:  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A palavra-chave **namespace** no prólogo XQuery define um prefixo de namespace que é usado no corpo da consulta.  
  
-   O corpo da consulta constrói o XML exigido.  
  
-   Na cláusula WHERE, o método **exist ()** é usado para localizar apenas as linhas que contêm descrições do catálogo de produtos. Ou seja, o XML que contém o elemento `ProductDescription` <>.  
  
 Este é o resultado:  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 A consulta a seguir recupera as mesmas informações, mas apenas para os modelos de produto cuja descrição de catálogo inclui o peso `Weight` , o <> elemento, nas especificações, `Specifications` o elemento de> <. Este exemplo usa WITH XMLNAMESPACES para declarar o prefixo pd e sua associação de namespace. Dessa forma, a associação não é descrita no método **Query ()** e no método **exist ()** .  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 Na consulta anterior, o método **exist ()** do tipo de dados **XML** na cláusula WHERE verifica se há um elemento <`Weight`> no elemento <`Specifications`>.  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>B. Localizar IDs de modelos de produtos cujas descrições de catálogo incluem ângulo frontal e pequenas fotos  
 A descrição do catálogo de produtos XML inclui as imagens do produto `Picture` , o elemento <>. Cada foto tem várias propriedades. Isso inclui o ângulo de imagem, o `Angle` <> elemento e o tamanho, o elemento `Size`> <.  
  
 Para modelos de produtos cujas descrições de catálogo incluem ângulo frontal e pequenas fotos, a consulta constrói um XML com o seguinte formato:  
  
```  
< Product ProductModelID="...">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   Na cláusula WHERE, o método **exist ()** é usado para recuperar somente as linhas que têm descrições do catálogo de produtos com `Picture` o elemento <>.  
  
-   A cláusula WHERE usa o método **Value ()** duas vezes para comparar os valores dos elementos <`Size`> e <`Angle`>.  
  
 Este é um resultado parcial:  
  
```  
<p1:Product   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. Crie uma lista simples dos pares de nome e recurso do modelo de produto, com cada par incluído \<no elemento recursos>  
 Na descrição de catálogo de modelo de produto, o XML inclui várias características de produto. Todos esses recursos estão incluídos no elemento <`Features`>. A consulta usa a [construção XML (XQuery)](../xquery/xml-construction-xquery.md) para construir o XML necessário. A expressão nas chaves é substituída pelo resultado.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   $pd/P1: Features/* retorna somente os filhos do nó de elemento `Features` de <>, mas $PD/P1: Features/node () retorna todos os nós. Isso inclui os nós de elemento, nós de texto, as instruções de processamento e os comentários.  
  
-   Os dois loops FOR geram um produto Cartesiano do qual o nome de produto e a característica individual são retornados.  
  
-   O **NomeDoProduto** é um atributo. A construção XML nesta consulta retorna-o como um elemento.  
  
 Este é um resultado parcial:  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. Na descrição do catálogo de um modelo de produto, liste o nome do modelo de produto, a ID do modelo e \<os recursos agrupados dentro de um elemento de> do produto  
 Usando as informações armazenadas na descrição do catálogo do modelo do produto, a consulta a seguir lista o nome do modelo do produto, a ID do modelo e os \<recursos agrupados dentro de um elemento de> de produto.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é um resultado parcial:  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. Recuperar as descrições de recursos de modelos do produto  
 A consulta a seguir constrói XML que inclui um elemento `Product` <> que tem os atributos **ProducModelID**, **ProductModelName** e os dois primeiros recursos do produto. Especificamente, os dois primeiros recursos do produto são os dois primeiros elementos filho do elemento `Features` <>. Se houver mais recursos, ele retornará um elemento <`There-is-more/`> vazio.  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O para... A estrutura de loop de retorno recupera os dois primeiros recursos do produto. A função **Position ()** é usada para localizar a posição dos elementos na sequência.  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. Localizar nomes de elementos na descrição do catálogo de produtos que terminam com "ons"  
 A consulta a seguir pesquisa as descrições do catálogo e retorna todos os elementos no `ProductDescription` elemento <> cujo nome termina com "los".  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Este é um resultado parcial:  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. Localizar descrições resumidas que contêm a palavra "Aerodynamic"  
 A consulta a seguir recupera modelos de produto cujas descrições de catálogo contêm a palavra "Aerodinâmico" na descrição sumária:  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 Observe que a consulta SELECT especifica os métodos **Query ()** e **Value ()** do tipo de dados **XML** . Portanto, em vez de repetir a declaração namespaces duas vezes em dois prólogos de consulta diferentes, o prefixo pd será usado na consulta e será definido apenas uma vez usando WITH XMLNAMESPACES.  
  
 Observe o seguinte na consulta anterior:  
  
-   A cláusula WHERE é usada para recuperar apenas as linhas em que a descrição do catálogo contém a palavra "Aerodynamic" no `Summary` elemento <>.  
  
-   A função **Contains ()** é usada para ver se a palavra está incluída no texto.  
  
-   O método **Value ()** do tipo de dados **XML** compara o valor retornado por **Contains ()** como 1.  
  
 Este é o resultado:  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. Localizar modelos de produtos cujas descrições de catálogo não incluem fotos do modelo do produto  
 A consulta a seguir recupera ProductModelIDs para modelos de produto cujas descrições de catálogo não incluem `Picture` um elemento <>.  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   Se o método **exist ()** na cláusula WHERE retornar false (0), a ID do modelo do produto será retornada. Caso contrário, não é retornado.  
  
-   Como todas as descrições de produtos incluem um `Picture` elemento <>, o conjunto de resultados é vazio nesse caso.  
  
## <a name="see-also"></a>Consulte Também  
 [XQueries envolvendo hierarquia](../xquery/xqueries-involving-hierarchy.md)   
 [XQueries envolvendo a ordem](../xquery/xqueries-involving-order.md)   
 [XQueries manipulando dados relacionais](../xquery/xqueries-handling-relational-data.md)   
 [Pesquisa de cadeia de caracteres em XQuery](../xquery/string-search-in-xquery.md)   
 [Manipulando namespaces no XQuery](../xquery/handling-namespaces-in-xquery.md)   
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
