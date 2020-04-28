---
title: Função concat (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:concat function
- concat function [XQuery]
ms.assetid: d50afd20-a297-445e-be9e-13b48017e7ca
author: rothja
ms.author: jroth
ms.openlocfilehash: 063eca49a6a4d69e84e8a3d05221b632d0690bef
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68099835"
---
# <a name="functions-on-string-values---concat"></a>Funções em Valores da Cadeia de Caracteres – concat
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Aceita zero ou mais cadeias de caracteres como argumentos e retorna uma cadeia de caracteres criada concatenando os valores de cada um desses argumentos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:concat ($string as xs:string?  
           ,$string as xs:string?  
           [, ...]) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$string*  
 Cadeia de caracteres opcional para concatenar.  
  
## <a name="remarks"></a>Comentários  
 A função requer pelo menos dois argumentos. Se um argumento for uma sequência vazia, será tratado como a cadeia de caracteres de comprimento zero.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados e, em alguns casos, o URI do namespace padrão para funções. Para obter mais informações, consulte a seção "as funções do XQuery são de reconhecimento de substitutos" no tópico [alterações significativas em mecanismo de banco de dados recursos no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte também o [nível de compatibilidade de ALTER DATABASE &#40;&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [agrupamento e suporte a Unicode](../relational-databases/collations/collation-and-unicode-support.md)do Transact-SQL.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados de exemplo AdventureWorks.  
  
### <a name="a-using-the-concat-xquery-function-to-concatenate-strings"></a>A. Uso da função concat() XQuery para concatenar cadeias de caracteres  
 Para um modelo de produto específico, essa consulta retorna uma cadeia de caracteres criada concatenando o período de garantia e a descrição de garantia. No documento de descrição do catálogo, o `Warranty` elemento <> é composto de <`WarrantyPeriod`> e <`Description` elementos filho>.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"  
        ProductModelName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE  PD.ProductModelID=28  
  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   Na cláusula SELECT, CatalogDescription é uma coluna de tipo **XML** . Portanto, o [método Query () (tipo de dados XML)](../t-sql/xml/query-method-xml-data-type.md), instruções. Query (), é usado. A instrução XQuery é especificada como o argumento para o método de consulta.  
  
-   O documento contra o qual a consulta é executada usa namespaces. Portanto, a palavra-chave **namespace** é usada para definir o prefixo do namespace. Para obter mais informações, consulte [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md).  
  
 Este é o resultado:  
  
```  
<Product ProductModelID="28" ProductModelName="Road-450">1 year-parts and labor</Product>  
```  
  
 A consulta anterior recupera informações de um produto específico. A consulta a seguir recupera as mesmas informações de todos os produtos para os quais são armazenadas descrições do catálogo XML. O método **exist ()** do tipo de dados **XML** na cláusula WHERE retornará true se o documento XML nas linhas tiver um elemento <`ProductDescription`>.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"   
        ProductName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE CatalogDescription.exist('//pd:ProductDescription ') = 1  
  
```  
  
 Observe que o valor booliano retornado pelo método **exist ()** do tipo **XML** é comparado com 1.  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **concat ()** em SQL Server só aceita valores do tipo xs: String. Outros valores precisam ser explicitamente convertidos em xs:string ou xdt:untypedAtomic.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
