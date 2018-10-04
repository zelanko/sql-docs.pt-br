---
title: número de função (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dbe1476f9b05d6ebaf3e919244fb759137cb2402
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650934"
---
# <a name="functions-on-nodes---number"></a>Funções em Nós – number
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o valor numérico do nó que é indicado por *$arg*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Nó cujo valor será retornado como um número.  
  
## <a name="remarks"></a>Comentários  
 Se *$arg* não é especificado, o valor numérico do nó de contexto, convertido em um duplo, será retornado. No SQL Server **fn:number()** sem um argumento só pode ser usado no contexto de um predicado dependente de contexto. Mais precisamente, só pode ser usado entre parênteses ([]). Por exemplo, a expressão a seguir retorna o elemento <`ROOT`>.  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 Se o valor do nó não for uma representação léxica válida de um tipo numérico simple, conforme definido em **XML Schema Part 2: Datatypes, recomendação do W3C**, a função retorna uma sequência vazia. Não é oferecido suporte a NaN.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. Usando a função number() Xquery para recuperar o valor numérico de um atributo  
 A consulta a seguir recupera o valor numérico do atributo de tamanho de lote do primeiro local de centro de trabalho no processo de fabricação do Modelo do Produto 7.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
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
  
-   O **Number ()** função não é necessária, conforme mostrado pela consulta para o **LotSizeA** atributo. Isso é uma função XPath 1.0 e é incluída principalmente por razões de compatibilidade com versões anteriores.  
  
-   O XQuery para **LotSizeB** Especifica a função de número e é redundante.  
  
-   A consulta para **LotSizeD** ilustra o uso de um valor numérico em uma operação aritmética.  
  
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
  
-   O **Number ()** função aceita somente nós. Ela não aceita valores atômicos.  
  
-   Quando os valores não podem ser retornados como um número, o **Number ()** função retorna a sequência vazia em vez de NaN.  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
