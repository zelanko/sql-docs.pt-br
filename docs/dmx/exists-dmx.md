---
title: Existe (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 936612dba4f466c5bc78f20f5a3ea07954a20a1c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37998578"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna **verdadeira** se a subconsulta especificada retornar pelo menos uma linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *subquery*  
 Uma instrução SELECT do formulário SELECT * FROM \<nome da coluna > [onde \<lista de predicados >].  
  
## <a name="result-type"></a>Tipo de Resultado  
 Retorna **verdadeira** se o conjunto de resultados retornado pela subconsulta contiver pelo menos uma linha; caso contrário, retornará **falso**.  
  
## <a name="remarks"></a>Remarks  
 Você pode usar a palavra-chave NOT antes de EXISTS: por exemplo, `WHERE NOT EXISTS (<subquery>)`.  
  
 A lista de colunas adicionada ao argumento de subconsulta de EXISTS é irrelevante; a função verifica somente a existência de uma linha que satisfaz a condição.  
  
## <a name="examples"></a>Exemplos  
 Você pode usar EXISTS e NOT EXISTS para verificar as condições em uma tabela aninhada. Isso é útil ao criar um filtro que controla os dados usados para treinar ou testar um modelo de mineração de dados. Para obter mais informações, consulte [Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 O exemplo a seguir se baseia a `[Association]` estrutura de mineração e modelo de mineração que você criou na [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). A consulta retorna somente os casos onde o cliente comprou pelo menos um kit de conserto.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 Outra maneira de exibir os mesmos dados que são retornados por essa consulta é abrir o modelo no Visualizador de associação, o conjunto de itens com o botão direito **kit de consertos = existente**, selecione o **Detalhar** opção e, em seguida, Selecione **somente casos de modelo**.  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Sintaxe de filtro e exemplos de modelo &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)  
  
  
