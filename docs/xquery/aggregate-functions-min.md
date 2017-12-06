---
title: "Função min (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
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
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81faade44725c2a3b09a7cc474c28d087e51bbed
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="aggregate-functions---min"></a>Agregar funções - min
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna de uma sequência de valores atômicos, *$arg*, o item cujo valor é menor do que todos os outros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de itens dos quais retornar o valor mínimo.  
  
## <a name="remarks"></a>Comentários  
 Todos os tipos de valores atomizados que são passados para **min ()** precisam ser subtipos do mesmo tipo base. Tipos base aceitos são os tipos que oferecem suporte a **gt** operação. Esses tipos incluem os três tipos base numéricos internos, os tipos base de data/hora, xs:string, xs:boolean e xdt:untypedAtomic. Valores do tipo xdt:untypedAtomic são convertidos em xs:double. Se houver uma mistura desses tipos, ou se outros valores de outros tipos forem passados, será gerado um erro estático.  
  
 O resultado de **min ()** recebe o tipo base dos tipos passados como xs: Double no caso de XDT: untypedatomic. Se a entrada estiver estaticamente vazia, o vazio será implícito e um erro estático será retornado.  
  
 O **min ()** função retorna o valor na sequência que é menor do que qualquer outro na sequência de entrada. Para valores xs:string, o agrupamento de ponto de código Unicode padrão está sendo usado. Se um valor XDT: untypedatomic não pode ser convertido em xs: Double, o valor será ignorado na sequência de entrada, *$arg*. Se a entrada for uma sequência vazia calculada dinamicamente, a sequência vazia será retornada.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. Usando a função min() XQuery para localizar o local de centro de trabalho com menos horas de trabalho  
 A consulta a seguir recupera todos os locais de centro de trabalho no processo de fabricação do modelo de produto (ProductModelID=7) com menos horas de trabalho. Geralmente, como mostrado a seguir, um único local é retornado. Se vários locais tivessem um número igual de horas de trabalho mínimas, todos eles seriam retornados.  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
-   O **namespace** palavra-chave no prólogo do XQuery define um prefixo de namespace. Esse prefixo é então usado no corpo do XQuery.  
  
 O corpo do XQuery constrói o XML que tem um \<local > elemento com WCID e **LaborHrs** atributos.  
  
-   A consulta também recupera os valores ProductModelID e nome.  
  
 Este é o resultado:  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **min ()** função mapeia todos os inteiros para xs: decimal.  
  
-   O **min ()** não há suporte para a função em valores do tipo xs: Duration.  
  
-   Não há suporte para sequências que misturam tipos, atravessando os limites de tipo base.  
  
-   Não há suporte para opção sintática que fornece agrupamento.  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
