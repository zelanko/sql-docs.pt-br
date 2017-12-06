---
title: "Função Ceiling (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f470dc4c609fb4f9fcfda2203a546feb233c593b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="numeric-values-functions---ceiling"></a>Funções de valores numéricas - limite 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o menor número sem uma parte fracionária que não seja menos que o valor de seu argumento. Se o argumento for uma sequência vazia, ele retornará a sequência vazia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:ceiling ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Número ao qual a função é aplicada.  
  
## <a name="remarks"></a>Comentários  
 Se o tipo de *$arg* é um de três tipos base numéricos, **xs: float**, **xs: Double**, ou **xs: decimal**, o tipo de retorno é o mesmo que o *$arg* tipo.  
  
 Se o tipo de *$arg* é um tipo que é derivado de um dos tipos numéricos, o tipo de retorno é o tipo numérico básico.  
  
 Se a entrada para as funções fn: Floor, FN: Ceiling ou FN: round for **XDT: untypedatomic**, ela será convertida implicitamente para **xs: Double**.  
  
 Qualquer outro tipo gera um erro estático.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-ceiling-xquery-function"></a>A. Usando a função ceiling() XQuery  
 Para o modelo de produto 7, essa consulta retorna uma lista de locais de centro de trabalho no processo de fabricação do modelo de produto. Para cada local de centro de trabalho, a consulta retorna a ID do local, as horas de trabalho e o tamanho de lote, se documentados. A consulta usa o **ceiling** função para retornar as horas de trabalho como valores do tipo **decimal**.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
     for $i in /AWMI:root/AWMI:Location  
     return   
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ ceiling($i/@LaborHours) }" >  
                    {   
                      $i/@LotSize  
                    }    
       </Location>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O prefixo do namespace AWMI significa Adventure Works Manufacturing Instructions. Esse prefixo se refere ao mesmo namespace usado no documento sendo examinado.  
  
-   **Instruções** é um **xml** coluna de tipo. Portanto, o [método Query () (tipo de dados XML)](../t-sql/xml/query-method-xml-data-type.md) é usado para especificar o XQuery. A instrução XQuery é especificada como o argumento para o método de consulta.  
  
-   **para... retornar** é uma construção de loop. Na consulta, o **para** loop identifica uma lista de \<local > elementos. Para cada local de centro de trabalho, o **retornar** instrução o **para** loop descreve o XML gerado:  
  
    -   Um \<local > elemento que tem os atributos LocationID e LaborHrs. A expressão correspondente dentro dos colchetes ({ }) recupera os valores exigidos do documento.  
  
    -   O {$i/@LotSize } expressão recupera o atributo LotSize do documento, se houver.  
  
    -   Este é o resultado:  
  
```  
ProductModelID Result    
-------------- ------------------------------------------------------  
7      <Location LocationID="10" LaborHrs="3" LotSize="100"/>  
       <Location LocationID="20" LaborHrs="2" LotSize="1"/>     
       <Location LocationID="30" LaborHrs="1" LotSize="1"/>     
       <Location LocationID="45" LaborHrs="1" LotSize="20"/>  
       <Location LocationID="60" LaborHrs="3" LotSize="1"/>     
       <Location LocationID="60" LaborHrs="4" LotSize="1"/>  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **Ceiling** função mapeia todos os valores inteiros para xs: decimal.  
  
## <a name="see-also"></a>Consulte também  
 [Floor função &#40; XQuery &#41;](../xquery/numeric-values-functions-floor.md)   
 [Função &#40; ida e volta XQuery &#41;](../xquery/numeric-values-functions-round.md)  
  
  
