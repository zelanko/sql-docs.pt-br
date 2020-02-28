---
title: Função Previous (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 882a098aaabcd4610fc6623e9741f7eeaa4f53ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081183"
---
# <a name="report-builder-functions---previous-function"></a>Funções do Construtor de Relatórios – Função Previous
  Retorna o valor ou o valor de agregação especificado para a instância anterior de um item do escopo especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *expressão*  
 (**Variant** ou **Binary**) A expressão a ser usada para identificar os dados para os quais o valor anterior deve ser recuperado, por exemplo, `Fields!Fieldname.Value` ou `Sum(Fields!Fieldname.Value)`.  
  
 *escopo*  
 (**String**) Opcional. O nome de um grupo ou uma região de dados, ou nulo (**Nothing** em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica o escopo do qual o valor anterior especificado pela *expression*deve ser recuperado.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna uma **Variant** ou um **Binary**.  
  
## <a name="remarks"></a>Comentários  
 A função **Previous** retorna o valor anterior para a expressão avaliada no escopo especificado depois que toda a classificação e filtragem tiverem sido aplicadas.  
  
 Se a *expression* não contiver uma agregação, a função **Previous** será padronizada como o escopo atual para o item de relatório.  
  
 Em um grupo de detalhes, use **Previous** para especificar o valor de uma referência de campo na instância anterior da linha de detalhes.  
  
> [!NOTE]  
>  A função **Anterior** somente dá suporte a referências de campo no grupo de detalhes. Por exemplo, em uma caixa de texto no grupo de detalhes, `=Previous(Fields!Quantity.Value)` retorna os dados para o campo `Quantity` da linha anterior. Na primeira linha, esta expressão retorna um nulo (**Nothing** em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]).  
  
 Se *expression* contiver uma função de agregação que use um escopo padrão, **Previous** agregará os dados dentro da instância anterior do escopo especificado na chamada da função de agregação.  
  
 Se *expression* contiver uma função de agregação que especifique um escopo diferente do padrão, o parâmetro *scope* da função **Previous** deverá ser um escopo contentor para o escopo especificado na chamada da função de agregação.  
  
 As funções **Level**, **InScope**, **Aggregate** e **Previous** não podem ser usadas no parâmetro *expression*. Não há suporte para a especificação do parâmetro *recursive* para qualquer função de agregação.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir, quando colocado na linha de dados padrão de uma região de dados, fornece o valor do campo `LineTotal` na linha anterior.  
  
### <a name="code"></a>Código  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra uma expressão que calcula a soma das vendas em um dia específico do mês e o valor anterior para esse dia do mês em um ano anterior. A expressão é adicionada a uma célula em uma linha que pertence ao `GroupbyDay`do grupo filho. Seu grupo pai é `GroupbyMonth`, que tem um grupo pai `GroupbyYear`. A expressão exibe os resultados de GroupbyDay (o escopo padrão) e de `GroupbyYear` (o pai do grupo pai `GroupbyMonth`).  
  
 Por exemplo, para uma região de dados com um grupo pai chamado `Year`, seu grupo filho chamado `Month`e seu grupo filho chamado `Day` (3 níveis aninhados). A expressão `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` em uma linha associada ao grupo `Day` retorna o valor das vendas para o mesmo dia e mês do ano anterior.  
  
### <a name="code"></a>Código  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
