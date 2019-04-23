---
title: Função Previous (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e3e856bf37328c5abaf4edd5bf296c1d557a2be7
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59971642"
---
# <a name="previous-function-report-builder-and-ssrs"></a>Função Previous (Construtor de Relatórios e SSRS)
  Retorna o valor ou o valor de agregação especificado para a instância anterior de um item do escopo especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expressão*  
 (`Variant` ou `Binary`) A expressão a ser usada para identificar os dados para os quais o valor anterior deve ser recuperado, por exemplo, `Fields!Fieldname.Value` ou `Sum(Fields!Fieldname.Value)`.  
  
 *escopo*  
 (`String`) Opcional. O nome de um grupo ou região de dados ou nulo (`Nothing` na [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica o escopo do qual recuperar o valor anterior especificado pela *expressão*.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna uma `Variant` ou um `Binary`.  
  
## <a name="remarks"></a>Comentários  
 A função `Previous` retorna o valor anterior para a expressão avaliada no escopo especificado depois que toda a classificação e filtragem tiverem sido aplicadas.  
  
 Se *expressão* não contiver uma agregação, o `Previous` função usa como padrão o escopo atual para o item de relatório.  
  
 Em um grupo de detalhes, use `Previous` para especificar o valor de uma referência de campo na instância anterior da linha de detalhes.  
  
> [!NOTE]  
>  O `Previous` função só dá suporte a referências de campo no grupo de detalhes. Por exemplo, em uma caixa de texto no grupo de detalhes, `=Previous(Fields!Quantity.Value)` retorna os dados para o campo `Quantity` da linha anterior. Na primeira linha, esta expressão retorna um nulo (`Nothing` em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]).  
  
 Se *expressão* contém uma função de agregação que usa um escopo padrão, `Previous` agregará os dados dentro da instância anterior do escopo especificado na agregação chamada de função.  
  
 Se *expressão* contém uma função de agregação que especifica um escopo diferente do padrão, o *escopo* parâmetro para o `Previous` função deve ser um escopo contentor para o escopo especificado em a chamada de função de agregação.  
  
 As funções `Level`, `InScope`, `Aggregate` e `Previous` não pode ser usada a *expressão*parâmetro. Não há suporte para a especificação do parâmetro *recursive* para qualquer função de agregação.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
