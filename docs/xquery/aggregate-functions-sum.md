---
title: Função SUM (XQuery) | Microsoft Docs
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
- sum function [XQuery]
- fn:sum function
ms.assetid: 12288f37-b54c-4237-b75e-eedc5fe8f96d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0f626eb9f5c1b654428175dc456910b183fe0c3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046842"
---
# <a name="aggregate-functions---sum"></a>Funções de Agregação – sum
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna a soma de uma sequência de números.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:sum($arg as xdt:anyAtomicType*) as xdt:anyAtomicType  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de valores atômicos cuja soma deve ser calculada.  
  
## <a name="remarks"></a>Comentários  
 Todos os tipos de valores atomizados que são passados para **SUM ()** têm que ser subtipos do mesmo tipo base. Os tipos base aceitos são os três tipos base numéricos internos ou xdt:untypedAtomic. Valores do tipo xdt:untypedAtomic são convertidos em xs:double. Se há uma mistura desses tipos, ou se outros valores de outros tipos são passados, um erro estático será gerado.  
  
 O resultado de **SUM ()** recebe o tipo base dos tipos passados como xs: Double no caso de XDT: untypedatomic, mesmo se a entrada for opcionalmente a sequência vazia. Se a entrada estiver estaticamente vazia, o resultado será 0 com o tipo estático e dinâmico de xs:integer.  
  
 O **SUM ()** função retorna a soma dos valores numéricos. Se um valor XDT: untypedatomic não puder ser convertido em xs: Double, o valor será ignorado na sequência de entrada *$arg*. Se a entrada for uma sequência vazia dinamicamente calculada, o valor 0 do tipo base usado será retornado.  
  
 A função retorna um erro de tempo de execução quando um estouro ou exceção fora do intervalo acontece.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas em várias **xml** colunas de tipo a [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-sum-xquery-function-to-find-the-total-combined-number-of-labor-hours-for-all-work-center-locations-in-the-manufacturing-process"></a>A. Usando a função sum() XQuery para localizar o número combinado total de horas de trabalho para todos os locais do centro de trabalho no processo de fabricação.  
 A consulta a seguir acha o total de horas de trabalho de todos os locais de centro de trabalho no processo de fabricação de todos os modelos de produtos nos quais as instruções de fabricação são armazenadas.  
  
```  
SELECT Instructions.query('         
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
  <ProductModel PMID= "{ sql:column("Production.ProductModel.ProductModelID") }"         
  ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >         
   <TotalLaborHrs>         
     { sum(//AWMI:Location/@LaborHours) }         
   </TotalLaborHrs>         
 </ProductModel>         
    ') as Result         
FROM Production.ProductModel         
WHERE Instructions is not NULL         
```  
  
 Este é o resultado parcial.  
  
```  
<ProductModel PMID="7" ProductModelName="HL Touring Frame">  
   <TotalLaborHrs>12.75</TotalLaborHrs>  
</ProductModel>  
<ProductModel PMID="10" ProductModelName="LL Touring Frame">  
  <TotalLaborHrs>13</TotalLaborHrs>  
</ProductModel>  
...  
```  
  
 Em vez de retornar o resultado como XML, você pode escrever a consulta para gerar resultados relacionais, como mostrado nesta consulta:  
  
```  
SELECT ProductModelID,         
        Name,         
        Instructions.value('declare namespace   
      AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
    sum(//AWMI:Location/@LaborHours)', 'float') as TotalLaborHours         
FROM Production.ProductModel         
WHERE Instructions is not NULL          
```  
  
 Este é um resultado parcial:  
  
```  
ProductModelID Name                 TotalLaborHours         
-------------- -------------------------------------------------  
7              HL Touring Frame           12.75                   
10             LL Touring Frame           13                      
43             Touring Rear Wheel         3                       
...  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Somente a versão de único argumento de **SUM ()** tem suporte.  
  
-   Se a entrada for uma sequência vazia dinamicamente calculada, o valor 0 do tipo base usado será retornado, em vez do tipo xs:integer.  
  
-   O **SUM ()** função mapeia todos os números inteiros para xs: decimal.  
  
-   O **SUM ()** não há suporte para a função em valores do tipo xs: Duration.  
  
-   Não há suporte para sequências que misturam tipos, atravessando os limites de tipo base.  
  
-   Sum, xs gera um erro de domínio.  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
