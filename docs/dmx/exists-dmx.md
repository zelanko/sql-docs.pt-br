---
title: Existe (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: df52a83c2e60395e72b6f81903d0372d1dc05614
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670244"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retornará **true** se a subconsulta especificada retornar pelo menos uma linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *subconsulta*  
 Uma instrução SELECT do formulário selecione * do \< nome da coluna> [onde a \< lista de predicados>].  
  
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
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Sintaxe de filtro de modelo e exemplos &#40;Analysis Services – Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
  
