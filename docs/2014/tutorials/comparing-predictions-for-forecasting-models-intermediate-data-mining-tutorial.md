---
title: Comparando previsões para modelos de previsão (tutorial de mineração de dados intermediários) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ead8a1fe-60d8-4017-8fb8-6fe32168e46d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 26cc445d3bad5c628628353d5c0c84ffa4755e97
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63066326"
---
# <a name="comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial"></a>Comparando previsões para modelos de previsão (Tutorial de mineração de dados intermediário)
  Nas etapas anteriores deste tutorial, você criou vários modelos de série temporal:  
  
-   Previsões para cada combinação de região e modelo, com base somente em dados para o modelo e a região individuais.  
  
-   Previsões para cada região, com base em dados atualizados.  
  
-   Previsões mundiais para todos os modelos, com base em dados agregados.  
  
-   Previsões para o modelo M200 na região América do Norte, com base no modelo agregado.  
  
 Para resumir os recursos para previsões de série temporal, você revisará as alterações para ser como o uso das opções para estender ou substituir dados afetou os resultados da previsão.  
  
 [EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
##  <a name="comparing-the-original-results-with-results-after-adding-data"></a><a name="bkmk_EXTEND"></a>Comparando os resultados originais com os resultados depois de adicionar dados  
 Vamos examinar os dados apenas da linha de produtos M200 na região do Pacífico, para ver como a atualização do modelo com novos dados afeta os resultados. Lembre-se de que a série de dados original terminava em junho de 2004, e nós obtivemos novos dados para julho, agosto e setembro.  
  
-   A primeira coluna mostra os novos dados que foram adicionados.  
  
-   A segunda coluna mostra a previsão para julho e posteriormente com base na série de dados original.  
  
-   A terceira coluna mostra a previsão com base nos dados estendidos.  
  
|**M200 Pacífico**|Dados de vendas reais atualizados|Previsão antes da adição dos dados|Previsão estendida|  
|----------------------|-----------------------------|------------------------------------|-------------------------|  
|7-25-2008|**65**|32|**65**|  
|8-25-2008|**54**|37|**54**|  
|9-25-2008|**61**|32|**61**|  
|10-25-2008|Sem dados|36|32|  
|11-25-2008|Sem dados|31|41|  
|12-25-2008|Sem dados|34|32|  
  
 Você observará que as previsões que usam os dados estendidos (mostrados aqui em negrito) repetem exatamente os pontos de dados reais. A repetição ocorre por design. Contanto que haja pontos de dados reais para usar, a consulta de previsão retornará os valores reais e mostrará novos valores de previsão somente depois que os novos pontos de dados reais tiverem ficado obsoletos.  
  
 Em geral, o algoritmo pondera as alterações nos novos dados mais fortemente do que nos dados iniciais do modelo. Porém, neste caso, os novos números de vendas representam um aumento de apenas 20-30% sobre o período anterior. Então, só houve um pequeno aumento nas vendas projetadas, depois das quais as projeções de vendas caíram novamente, mais alinhados com a tendência dos meses anteriores aos novos dados.  
  
##  <a name="comparing-the-original-and-cross-prediction-results"></a><a name="bkmk_REPLACE"></a>Comparando os resultados original e de previsão cruzada  
 Lembre-se de que o modelo de mineração original revelou grandes diferenças entre as regiões e as linhas de produtos. Por exemplo, as vendas para o modelo M200 foram muito fortes, ao passo que as vendas para o modelo T1000 foram bastante baixas em todas as regiões. Além disso, algumas séries não tinham muitos dados. As séries foram irregulares, o que significa que elas não tinham o mesmo ponto de partida.  
  
 ![Séries que preveem a quantidade M200 e T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "Séries que preveem a quantidade M200 e T1000")  
  
 Então, como as previsões mudaram quando você fez suas projeções com base no modelo geral, que é baseado em vendas mundiais, e não nos conjuntos de dados originais? Para não perder informações nem distorcer as previsões, você pode salvar os resultados a uma tabela, unir a tabela de previsões à tabela de dados históricos, e traçar um gráfico dos dois conjuntos de dados históricos e previsões.  
  
 O diagrama a seguir é baseado apenas uma linha de produto, a M200. O gráfico compara as previsões do modelo de mineração inicial com as previsões usando o modelo de mineração agregado.  
  
 ![Gráfico do Excel comparando previsões](../../2014/tutorials/media/m200-predictions-compared.gif "Gráfico do Excel comparando previsões")  
  
 Neste diagrama, é possível ver que o modelo de mineração agregado preserva a variação e as tendências gerais em valores ao mesmo tempo em que minimiza as flutuações nas séries de dados individuais.  
  
## <a name="conclusion"></a>Conclusão  
 Você aprendeu a criar e personalizar um modelo de série temporal que pode ser usado para previsão.  
  
 Você aprendeu atualizar seus modelos de série temporal sem precisar reprocessá-los, adicionando novos dados e criando previsões usando o parâmetro EXTEND_MODEL_CASES.  
  
 Você aprendeu a criar modelos que podem ser usados para previsão cruzada, usando o parâmetro REPLACE_MODEL_CASES e aplicando o modelo a uma série de dados diferente.  
  
## <a name="see-also"></a>Consulte Também  
 [Tutorial de mineração de dados intermediário &#40;Analysis Services de mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Exemplos de consulta de modelos de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
