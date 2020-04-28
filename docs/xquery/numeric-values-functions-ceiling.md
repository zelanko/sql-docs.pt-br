---
title: Função de teto (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
author: rothja
ms.author: jroth
ms.openlocfilehash: fe18f488b83c1a8c9236c642751c1dc80bfe7e6c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946574"
---
# <a name="numeric-values-functions---ceiling"></a>Funções de Valores Numéricos – ceiling 
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
 Se o tipo de *$ARG* for um dos três tipos de base numéricos, **xs: float**, **xs: Double**ou **xs: decimal**, o tipo de retorno será o mesmo que o tipo de *$ARG* .  
  
 Se o tipo de *$ARG* for um tipo derivado de um dos tipos numéricos, o tipo de retorno será o tipo numérico base.  
  
 Se a entrada para as funções fn: Floor, fn: teto ou fn: round for **xdt: untypedAtomic**, ela será implicitamente convertida em **xs: Double**.  
  
 Qualquer outro tipo gera um erro estático.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-ceiling-xquery-function"></a>A. Usando a função ceiling() XQuery  
 Para o modelo de produto 7, essa consulta retorna uma lista de locais de centro de trabalho no processo de fabricação do modelo de produto. Para cada local de centro de trabalho, a consulta retorna a ID do local, as horas de trabalho e o tamanho de lote, se documentados. A consulta usa a função de **teto** para retornar as horas de trabalho como valores do tipo **decimal**.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
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
  
-   **Instruções** é uma coluna de tipo **XML** . Portanto, o [método Query () (tipo de dados XML)](../t-sql/xml/query-method-xml-data-type.md) é usado para especificar XQuery. A instrução XQuery é especificada como o argumento para o método de consulta.  
  
-   **para... Return** é um constructo de loop. Na consulta, o loop **for** identifica uma lista de elementos \<de localização>. Para cada local do centro de trabalho, a instrução **Return** no loop **for** descreve o XML a ser gerado:  
  
    -   Um \<elemento de> local que tem os atributos LocationID e LaborHrs. A expressão correspondente dentro dos colchetes ({ }) recupera os valores exigidos do documento.  
  
    -   A expressão {i/@LotSize $} recupera o atributo de lotes do documento, se presente.  
  
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
  
-   A função **teto ()** mapeia todos os valores inteiros para xs: decimal.  
  
## <a name="see-also"></a>Consulte Também  
 [Função Floor &#40;&#41;XQuery](../xquery/numeric-values-functions-floor.md)   
 [Função round &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)  
  
  
