---
title: Função string-length (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- string-length function
- fn:string-length function
ms.assetid: 7cd69c8b-cf2c-478c-b9a3-e0e14e1aa8aa
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8193643e59c89d1bdc2877e72105f83a1fd6df3f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670205"
---
# <a name="functions-on-string-values---string-length"></a>Funções em Valores da Cadeia de Caracteres – string-length
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o comprimento da cadeia de caracteres em caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:string-length() as xs:integer  
fn:string-length($arg as xs:string?) as xs:integer  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Cadeia de caracteres de origem cujo comprimento será computado.  
  
## <a name="remarks"></a>Comentários  
 Se o valor de *$arg* é uma sequência vazia, um **xs: Integer** valor 0 será retornado.  
  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados. Se o nível de compatibilidade for 110 ou posterior, cada par substituto será contado como um único caractere. Em níveis de compatibilidade anteriores, eles são contados como dois caracteres. Para obter mais informações, consulte [nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
 Se o valor contiver um caractere Unicode de 4 bytes, representado por dois caracteres substitutos, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contará os caracteres substitutos individualmente.  
  
 O **string-length()** sem um parâmetro só pode ser usado dentro de um predicado. Por exemplo, a consulta a seguir retorna o elemento <`ROOT`>:  
  
```  
DECLARE @x xml;  
SET @x='<ROOT>Hello</ROOT>';  
SELECT @x.query('/ROOT[string-length()=5]');  
```  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados e, em alguns casos, o URI do namespace padrão para funções. Para obter mais informações, consulte a seção "XQuery funções têm consciência de substitutos" no tópico [alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte também [nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-string-length-xquery-function-to-retrieve-products-with-long-summary-descriptions"></a>A. Usando uma função string-length() XQuery para recuperar produtos com longas descrições resumidas  
 Para produtos cuja descrição resumida é maior que 50 caracteres, a consulta a seguir recupera a ID do produto, o comprimento da descrição resumida e o próprio resumo, o elemento <`Summary`>.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT CatalogDescription.query('  
      <Prod ProductID= "{ /pd:ProductDescription[1]/@ProductModelID }" >  
       <LongSummary SummaryLength =   
           "{string-length(string( (/pd:ProductDescription/pd:Summary)[1] )) }" >  
           { string( (/pd:ProductDescription/pd:Summary)[1] ) }  
       </LongSummary>  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('string-length( string( (/pd:ProductDescription/pd:Summary)[1]))', 'decimal') > 200;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A condição na cláusula WHERE recupera só as linhas em que a descrição resumida armazenada no documento XML é mais longa que 200 caracteres. Ele usa o [método Value () (tipo de dados XML)](../t-sql/xml/value-method-xml-data-type.md).  
  
-   A cláusula SELECT simplesmente constrói o XML desejado. Ele usa o [método Query () (tipo de dados XML)](../t-sql/xml/query-method-xml-data-type.md) para construir o XML e especificar a expressão XQuery necessária para recuperar dados do documento XML.  
  
 Este é um resultado parcial:  
  
```  
Result  
-------------------  
<Prod ProductID="19">  
      <LongSummary SummaryLength="214">Our top-of-the-line competition   
             mountain bike. Performance-enhancing options include the  
             innovative HL Frame, super-smooth front suspension, and   
             traction for all terrain.  
      </LongSummary>  
</Prod>  
...  
```  
  
### <a name="b-using-the-string-length-xquery-function-to-retrieve-products-whose-warranty-descriptions-are-short"></a>B. Usando a função string-length() XQuery para recuperar produtos cujas descrições de garantia sejam curtas  
 Para produtos cujas descrições de garantia tenham menos que 20 caracteres, a consulta a seguir recupera XML que inclui a ID do produto, o comprimento, a descrição de garantia, e o elemento <`Warranty`> em si.  
  
 A garantia é um dos recursos do produto. Um elemento filho opcional <`Warranty`> segue após o elemento <`Features`>.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for   $ProdDesc in /pd:ProductDescription,  
            $pf in $ProdDesc/pd:Features/wm:Warranty  
      where string-length( string(($pf/wm:Description)[1]) ) < 20  
      return   
          <Prod >  
             { $ProdDesc/@ProductModelID }  
             <ShortFeature FeatureDescLength =   
                             "{string-length( string(($pf/wm:Description)[1]) ) }" >  
                 { $pf }  
             </ShortFeature>  
          </Prod>  
     ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription')=1;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   **PD** e **wm** são os prefixos de namespace usados nessa consulta. Eles identificam os mesmos namespaces utilizados no documento que está sendo consultado.  
  
-   O XQuery especifica um loop FOR aninhado. O loop FOR externo é necessário, pois você deseja recuperar o **ProductModelID** atributos da <`ProductDescription`> elemento. O loop FOR interno é necessário, porque você deseja somente aqueles produtos que têm descrições de recursos de garantia com menos de 20 caracteres.  
  
 Este é o resultado parcial:  
  
```  
Result  
-------------------------  
<Prod ProductModelID="19">  
  <ShortFeature FeatureDescLength="15">  
    <wm:Warranty   
       xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
      <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
      <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
   </ShortFeature>  
</Prod>  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
