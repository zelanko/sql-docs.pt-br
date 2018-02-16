---
title: "Matriz de classificação (Analysis Services – mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- displaying mining accuracy
- confusion matrix [data mining]
- classification matrix [Analysis Services]
- accuracy testing [data mining]
ms.assetid: 5c12f202-2ed9-41fa-bee2-0f7ab3ff058a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7897c756eb0aa9aa53ed56356052974e53afd601
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="classification-matrix-analysis-services---data-mining"></a>Matriz de classificação (Analysis Services - Mineração de dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Uma *matriz de classificação* é criada classificando-se todos os casos do modelo em categorias, determinando se o valor previsto correspondeu ao valor real. Todos os casos em cada categoria são contabilizados e os totais são exibidos na matriz. A matriz de classificação é uma ferramenta padrão para avaliação de modelos estatísticos e é muitas vezes chamada de *matriz de confusão*.  
  
 O gráfico que é criado quando você escolhe a opção **Matriz de Classificação** compara valores reais com previstos para cada estado previsto que você especifica. As linhas na matriz representam os valores previstos para o modelo, sendo que as colunas representam os valores atuais. As categorias usadas na análise são *falsos positivos*, *verdadeiros positivos*, *falsos negativos*e *verdadeiros negativos*  
  
 Uma matriz de classificação é uma ferramenta importante para avaliar os resultados de previsão porque facilita o entendimento e reage aos efeitos de previsões erradas. Ao exibir a quantidade e os percentuais em cada célula desta matriz, você pode consultar rapidamente com que frequência o modelo é previsto com precisão.  
  
 Esta seção explica como criar uma matriz de classificação e como interpretar os resultados.  
  
## <a name="understanding-the-classification-matrix"></a>Entendendo a matriz de classificação  
 Considere o modelo que você criou como parte do Tutorial de mineração de dados básico. O modelo [TM_DecisionTree], usado para ajudar a criar uma campanha de mala direta, e pode ser usado para prever os clientes com maior probabilidade de comprar uma bicicleta. Para testar a utilidade esperada deste modelo, use um conjunto de dados para qual os valores do atributo de resultado, [Bike Buyer], já é conhecido. Normalmente, você usaria o conjunto de dados de teste que foi reservado durante a criação da estrutura de mineração usada para treinar o modelo.  
  
 Há somente dois resultados possíveis: sim (é provável que o cliente compre uma bicicleta), e não (o cliente provavelmente não comprará uma bicicleta). Portanto, a matriz de classificação resultante é relativamente simples.  
  
## <a name="interpreting-the-results"></a>Interpretando os resultados  
 A tabela a seguir mostra a matriz de classificação para o modelo TM_DecisionTree. Lembre-se de que, para este atributo previsível, 0 significa Não e 1 significa Sim.  
  
|Previsto|0 (Real)|1 (Real)|  
|---------------|------------------|------------------|  
|0|362|144|  
|1|121|373|  
  
 A primeira célula de resultado, que contém o valor 362, indica o número de *verdadeiros positivos* para obter o valor 0. Como 0 indica que o cliente não comprou a bicicleta, essa estatística indica que o modelo previu o valor correto para pessoas que não compram bicicletas em 362 casos.  
  
 A célula logo abaixo dessa, que contém o valor 121, indica o número de *falsos positivos*ou quantas vezes o modelo previu que alguém compraria uma bicicleta, mas a compra não se concretizou.  
  
 A célula que contém o valor 144 indica o número de *falsos positivos* para o valor 1. Como 1 significa que o cliente não comprou a bicicleta, essa estatística indica que em 144 casos, o modelo previu que alguém não compraria a bicicleta, mas na verdade a compra se concretizou.  
  
 Finalmente, a célula que contém o valor 373 indica o número de verdadeiros positivos para o valor de destino 1. Em outras palavras, em 373 casos, o modelo previu corretamente que alguém compraria uma bicicleta.  
  
 Somando os valores das células que são diagonalmente adjacentes, você pode determinar a exatidão geral do modelo. Uma diagonal mostra o número de previsões corretas, e a outra diagonal mostra o número de previsões incorretas.  
  
### <a name="using-multiple-predictable-values"></a>Usando vários valores previsíveis  
 O caso [Bike Buyer] é especialmente fácil de ser interpretado porque há apenas dois valores possíveis. Quando o atributo previsível tem vários valores possíveis, a matriz de classificação adiciona uma nova coluna a cada valor real possível e depois calcula o número de correspondências para cada valor previsto. A tabela a seguir mostra os resultados em um modelo diferente, onde três valores (0, 1 e 2) são possíveis.  
  
|Previsto|0 (Real)|1 (Real)|2 (Real)|  
|---------------|------------------|------------------|------------------|  
|0|111|3|5|  
|1|2|123|17|  
|2|19|0|20|  
  
 Apesar de a adição de mais colunas tornar o relatório aparentemente mais complexo, detalhes adicionais podem ser úteis quando queremos avaliar o custo cumulativo de uma previsão incorreta. Para criar somas nas diagonais ou comparar resultados para diferentes combinações de linhas, você pode clicar no botão **Copiar** , presente na guia **Matriz de Classificação** , e colar o relatório no Excel. Como alternativa, você pode usar um cliente, como o Cliente de Mineração de Dados para Excel, que dá suporte ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, para criar um relatório de classificação diretamente no Excel que inclua contagens e porcentagens. Para obter mais informações, consulte [Mineração de Dados do SQL Server](http://go.microsoft.com/fwlink/?LinkID=77733).  
  
## <a name="restrictions-on-the-classification-matrix"></a>Restrições na matriz de classificação  
 Uma matriz de classificação só pode ser usada com atributos previsíveis discretos.  
  
 Embora você possa adicionar vários modelos ao selecionar modelos na guia **Seleção de Entrada** do designer **Gráfico de Precisão de Mineração** , a guia **Matriz de Classificação** exibirá uma matriz separada para cada modelo.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Os tópicos a seguir contêm mais informações sobre como você pode criar e usar matrizes de classificação e outros gráficos.  
  
|Tópicos|Links|  
|------------|-----------|  
|Fornece um passo a passo sobre como criar um gráfico de comparação de precisão para o modelo Mala Direta Dirigida.|[Tutorial de mineração de dados básicos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)<br /><br /> [Testando a precisão com gráficos de comparação de precisão &#40;Tutorial de mineração de dados básicos&#41;](http://msdn.microsoft.com/library/822d414b-4a39-473f-80c3-53476e30655a)|  
|Explica os tipos de gráficos relacionados.|[Gráfico de comparação de precisão &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de ganho &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de dispersão &#40; Analysis Services – mineração de dados &#41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|Descreve usos de validação cruzada para modelos de mineração e estruturas de mineração.|[Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Descreve as etapas para criar gráficos de comparação de precisão e outros gráficos de exatidão.|[Teste e validação de tarefas e instruções &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Teste e validação &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
