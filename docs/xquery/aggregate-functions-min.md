---
title: Função min (XQuery) | Microsoft Docs
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
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
author: rothja
ms.author: jroth
ms.openlocfilehash: 29e5718debadb4725bc9d9ebcd499c261ed23d54
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67985753"
---
# <a name="aggregate-functions---min"></a>Funções de Agregação – min
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna de uma sequência de valores atômicos, *$ARG*, um item cujo valor é menor que o de todos os outros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de itens dos quais retornar o valor mínimo.  
  
## <a name="remarks"></a>Comentários  
 Todos os tipos de valores Atom que são passados para **min ()** precisam ser subtipos do mesmo tipo base. Os tipos base que são aceitos são os tipos que dão suporte à operação **gt** . Esses tipos incluem os três tipos base numéricos internos, os tipos base de data/hora, xs:string, xs:boolean e xdt:untypedAtomic. Valores do tipo xdt:untypedAtomic são convertidos em xs:double. Se houver uma mistura desses tipos, ou se outros valores de outros tipos forem passados, um erro estático será gerado.  
  
 O resultado de **min ()** recebe o tipo base do passado em tipos, como xs: Double no caso de xdt: untypedAtomic. Se a entrada estiver estaticamente vazia, o vazio será implícito e um erro estático será retornado.  
  
 A função **min ()** retorna um valor na sequência que é menor do que qualquer outra na sequência de entrada. Para valores xs:string, a ordenação de ponto de código Unicode padrão está sendo usada. Se um valor de xdt: untypedAtomic não puder ser convertido em xs: Double, o valor será ignorado na sequência de entrada, *$ARG*. Se a entrada for uma sequência vazia calculada dinamicamente, a sequência vazia será retornada.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. Usando a função min() XQuery para localizar o local de centro de trabalho com menos horas de trabalho  
 A consulta a seguir recupera todos os locais de centro de trabalho no processo de fabricação do modelo de produto (ProductModelID=7) com menos horas de trabalho. Geralmente, como mostrado a seguir, um único local é retornado. Se vários locais tivessem um número igual de horas de trabalho mínimas, todos eles seriam retornados.  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  for   $Location in /AWMI:root/AWMI:Location  
  where $Location/@LaborHours =  
          min( /AWMI:root/AWMI:Location/@LaborHours )  
return  
  <Location WCID=     "{ $Location/@LocationID }"   
              LaborHrs= "{ $Location/@LaborHours }" />  
  ') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A palavra-chave **namespace** no prólogo XQuery define um prefixo de namespace. Esse prefixo é então usado no corpo do XQuery.  
  
 O corpo do XQuery constrói o XML que tem um \<elemento de> local com os atributos WCID e **LaborHrs** .  
  
-   A consulta também recupera os valores ProductModelID e nome.  
  
 Este é o resultado:  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **min ()** mapeia todos os inteiros para xs: decimal.  
  
-   Não há suporte para a função **min ()** em valores do tipo xs: Duration.  
  
-   Não há suporte para sequências que misturam tipos, atravessando os limites de tipo base.  
  
-   Não há suporte para opção sintática que fornece ordenação.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
