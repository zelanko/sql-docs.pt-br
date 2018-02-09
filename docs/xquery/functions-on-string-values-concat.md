---
title: "Função concat (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:concat function
- concat function [XQuery]
ms.assetid: d50afd20-a297-445e-be9e-13b48017e7ca
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f4970f431b3929268414fd78d7e834d7a835919
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-string-values---concat"></a>Funções em valores de cadeia de caracteres - concat
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
  
## <a name="remarks"></a>Remarks  
 A função requer pelo menos dois argumentos. Se um argumento for uma sequência vazia, será tratado como a cadeia de caracteres de comprimento zero.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados e, em alguns casos, o URI do namespace padrão para funções. Para obter mais informações, consulte a seção "XQuery funções têm consciência de substitutos" no tópico [alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte também [nível de compatibilidade de ALTER DATABASE &#40; Transact-SQL &#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de banco de dados de exemplo AdventureWorks.  
  
### <a name="a-using-the-concat-xquery-function-to-concatenate-strings"></a>A. Uso da função concat() XQuery para concatenar cadeias de caracteres  
 Para um modelo de produto específico, essa consulta retorna uma cadeia de caracteres criada concatenando o período de garantia e a descrição de garantia. No documento de descrição do catálogo, o elemento <`Warranty`> é composto pelos elementos filho <`WarrantyPeriod`> e <`Description`>.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
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
  
-   Na cláusula SELECT, CatalogDescription é uma **xml** coluna de tipo. Portanto, o [método Query () (tipo de dados XML)](../t-sql/xml/query-method-xml-data-type.md), instructions, é usado. A instrução XQuery é especificada como o argumento para o método de consulta.  
  
-   O documento contra o qual a consulta é executada usa namespaces. Portanto, o **namespace** palavra-chave é usada para definir o prefixo do namespace. Para obter mais informações, consulte [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md).  
  
 Este é o resultado:  
  
```  
<Product ProductModelID="28" ProductModelName="Road-450">1 year-parts and labor</Product>  
```  
  
 A consulta anterior recupera informações de um produto específico. A consulta a seguir recupera as mesmas informações de todos os produtos para os quais são armazenadas descrições do catálogo XML. O **exist ()** método o **xml** tipo de dados na cláusula WHERE retornará True se o documento XML nas linhas tiver um <`ProductDescription`> elemento.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
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
  
 Observe que o valor booliano retornado pelo **exist ()** método o **xml** tipo é comparado com 1.  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **concat ()** função no SQL Server aceita somente valores do tipo xs: String. Outros valores precisam ser explicitamente convertidos em xs:string ou xdt:untypedAtomic.  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
