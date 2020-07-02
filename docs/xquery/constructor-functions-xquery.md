---
title: Funções de Construtor (XQuery) | Microsoft Docs
description: Saiba mais sobre as funções de Construtor no XQuery que permitem criar instâncias dos tipos Atomic internos ou definidos pelo usuário do XSD.
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
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
ms.openlocfilehash: 56dd5919565d1cbb7d0b95ae4476aef9140cecd0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773715"
---
# <a name="constructor-functions-xquery"></a>Funções do construtor (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  De uma entrada especificada, as funções do construtor criam instâncias de qualquer tipo atômico interno XSD definido pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *$strval*  
 A cadeia de caracteres que será convertida.  
  
 *TYP*  
 Qualquer tipo XSD interno.  
  
## <a name="remarks"></a>Comentários  
 Há suporte para construtores de tipos base e XSD derivados atômicos. No entanto, os subtipos de **xs: Duration**, que inclui **xdt: yearMonthDuration e xdt: dayTimeDuration**e **xs: QName**, **xs: NMTOKEN**e **xs: Notation** não têm suporte. Tipos atômicos definidos pelo usuário, que estejam disponíveis nas coleções de esquemas associadas também estarão disponíveis, desde que eles sejam direta ou indiretamente derivados dos tipos a seguir.  
  
#### <a name="supported-base-types"></a>Tipos de base com suporte  
 Esses são os tipos base com suporte:  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs:gMonthDay  
  
-   xs:gDay  
  
-   xs:gMonth  
  
-   xs:hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>Tipos derivados com suporte  
 Estes são os tipos derivados com suporte:  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs:Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs:byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 O SQL Server também oferece suporte para dobra constante para invocações de funções de construção nas seguintes maneiras:  
  
-   Se o argumento for uma cadeia de caracteres literal, a expressão será avaliada durante a compilação. Quando o valor não atender às restrições de tipo, um erro estático será gerado.  
  
-   Se o argumento for um literal de outro tipo, a expressão será avaliada durante a compilação. Quando o valor não atender às restrições de tipo, uma sequência vazia será retornada.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>a. Usando a função dateTime() XQuery para recuperar descrições de produtos mais antigos  
 Neste exemplo, um documento XML de exemplo é atribuído primeiro a uma variável de tipo **XML** . Este documento contém três exemplos de `ProductDescription` elementos de> de <, com cada um contendo um <`DateCreated` elemento filho>.  
  
 A variável é então consultada para recuperar apenas aquelas descrições de produtos que tenham sido criados antes de uma data específica. Para fins de comparação, a consulta usa a função de construtor **xs: DateTime ()** para digitar as datas.  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O para... A estrutura de loop WHERE é usada para recuperar o \<ProductDescription> elemento que satisfaz a condição especificada na cláusula WHERE.  
  
-   A função de construtor **DateTime ()** é usada para construir valores de tipo **DateTime** para que eles possam ser comparados adequadamente.  
  
-   A consulta então constrói o XML resultante. Como você está construindo uma sequência de atributos, vírgulas e parênteses são usados na construção XML.  
  
 Este é o resultado:  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Construção XML &#40;&#41;XQuery](../xquery/xml-construction-xquery.md)   
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
