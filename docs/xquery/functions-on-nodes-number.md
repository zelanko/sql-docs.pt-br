---
title: Função Number (XQuery) | Microsoft Docs
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
author: rothja
ms.author: jroth
ms.openlocfilehash: 31a52f86692d5769fe22f4cf0b5a04ad324c3ac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67930113"
---
# <a name="functions-on-nodes---number"></a>Funções em Nós – number
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o valor numérico do nó indicado por *$ARG*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Nó cujo valor será retornado como um número.  
  
## <a name="remarks"></a>Comentários  
 Se *$ARG* não for especificado, o valor numérico do nó de contexto, convertido em Double, será retornado. No SQL Server, **fn: Number ()** sem um argumento só pode ser usado no contexto de um predicado dependente de contexto. Mais precisamente, só pode ser usado entre parênteses ([]). Por exemplo, a expressão a seguir retorna o `ROOT` elemento <>.  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 Se o valor do nó não for uma representação lexical válida de um tipo simples numérico, conforme definido no **esquema XML parte 2: tipos de datatipos, recomendação do W3C**, a função retornará uma sequência vazia. Não é oferecido suporte a NaN.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>a. Usando a função number() Xquery para recuperar o valor numérico de um atributo  
 A consulta a seguir recupera o valor numérico do atributo de tamanho de lote do primeiro local de centro de trabalho no processo de fabricação do Modelo do Produto 7.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in (//AWMI:root//AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"   
                   LotSizeA="{  $i/@LotSize }"  
                   LotSizeB="{  number($i/@LotSize) }"  
                   LotSizeC="{ number($i/@LotSize) + 1 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A função **Number ()** não é necessária, conforme mostrado pela consulta para o atributo **LotSizeA** . Isso é uma função XPath 1.0 e é incluída principalmente por razões de compatibilidade com versões anteriores.  
  
-   O XQuery para **LotSizeB** especifica a função Number e é redundante.  
  
-   A consulta para **muitos** ilustra o uso de um valor numérico em uma operação aritmética.  
  
 Este é o resultado:  
  
```  
ProductModelID   Result  
----------------------------------------------  
7              <Location LocationID="10"   
                         LotSizeA="100"   
                         LotSizeB="100"   
                         LotSizeC="101" />  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **Number ()** aceita apenas nós. Ela não aceita valores atômicos.  
  
-   Quando os valores não podem ser retornados como um número, a função **Number ()** retorna a sequência vazia em vez de Nan.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
