---
description: Exists (DMX)
title: Existe (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a0fa41dfff8edc6ddddeb420027a436f235e54a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353332"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Retornará **true** se a subconsulta especificada retornar pelo menos uma linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *subquery*  
 Uma instrução SELECT do formulário selecione * em \<column name> [Where \<predicate list> ].  
  
## <a name="result-type"></a>Tipo de resultado  
 Retornará **true** se o conjunto de resultados retornado pela subconsulta contiver pelo menos uma linha; caso contrário, retornará **false**.  
  
## <a name="remarks"></a>Comentários  
 Você pode usar a palavra-chave NOT antes de EXISTS: por exemplo, `WHERE NOT EXISTS (<subquery>)`.  
  
 A lista de colunas adicionada ao argumento de subconsulta de EXISTS é irrelevante; a função verifica somente a existência de uma linha que satisfaz a condição.  
  
## <a name="examples"></a>Exemplos  
 Você pode usar EXISTS e NOT EXISTS para verificar as condições em uma tabela aninhada. Isso é útil ao criar um filtro que controla os dados usados para treinar ou testar um modelo de mineração de dados. Para obter mais informações, consulte [Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining).  
  
 O exemplo a seguir é baseado na `[Association]` estrutura de mineração e no modelo de mineração que você criou no [tutorial de mineração de dados básico](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). A consulta retorna somente os casos onde o cliente comprou pelo menos um kit de conserto.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 Outra maneira de exibir os mesmos dados retornados por essa consulta é abrir o modelo no Visualizador de associação, clicar com o botão direito do mouse no **Kit de patch do conjunto = existing**, selecionar a opção **Drill-through** e, em seguida, selecionar **somente casos de modelo**.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;&#41;DMX ](../dmx/functions-dmx.md)   
 [Sintaxe de filtro de modelo e exemplos &#40;Analysis Services – Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
  
