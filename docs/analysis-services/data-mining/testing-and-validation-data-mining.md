---
title: "Teste e validação (mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- testing data mining models
- comparing mining models
- continuous attribute charts
- data mining [Analysis Services], models
- charts [Analysis Services]
- predictive modeling [Analysis Services]
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- confidence scores [data mining]
- displaying mining accuracy
- predictions [Analysis Services], comparing mining models
- scoring [data mining]
- lift charts [Analysis Services]
- classification matrix [Analysis Services]
- CRISP-DM
- accuracy testing [data mining]
ms.assetid: 197144f5-21ed-4009-b448-fe412fb3916c
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf43af38fc18b67c37ec5409ccb90a1d8e798259
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="testing-and-validation-data-mining"></a>Teste e validação (mineração de dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
A validação é o processo de avaliar como seus modelos de mineração são executados nos dados reais. É importante validar seus modelos de mineração entendendo suas qualidades e características antes de implantá-los em um ambiente de produção.  
  
 Esta seção apresenta alguns conceitos básicos relacionados à qualidade do modelo e descreve as estratégias para a validação de modelo fornecidas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter uma visão geral de como a validação de modelo funciona no processo de mineração de dados mais amplo, consulte [Soluções de mineração de dados](../../analysis-services/data-mining/data-mining-solutions.md).  
  
## <a name="methods-for-testing-and-validation-of-data-mining-models"></a>Métodos para teste e validação de modelos de mineração de dados  
 Há muitas abordagens para avaliar a qualidade e as características de um modelo de mineração de dados.  
  
-   Use várias medidas de validade estatística para determinar se há problemas nos dados ou no modelo.  
  
-   Separe os dados em conjuntos de treinamentos e testes para testar a exatidão das previsões.  
  
-   Peça a especialistas comerciais para revisarem os resultados do modelo de mineração de dados a fim de determinar se os padrões descobertos são significativos no cenário de negócios de destino  
  
 Todos esses métodos são úteis na metodologia de mineração de dados e são usados iterativamente ao criar, testar e refinar modelos para responder a um problema específico. Não há nenhuma regra abrangente que possa dizer quando um modelo é bom o bastante o quando tem dados suficientes.  
  
## <a name="definition-of-criteria-for-validating-data-mining-models"></a>Definição de critérios para validar modelos de mineração de dados  
 As medidas de mineração de dados geralmente entram nas categorias de exatidão, confiabilidade e utilidade.  
  
 *Exatidão* é uma medida que mostra se o modelo correlaciona um resultado com os atributos nos dados fornecidos. Há várias medidas de exatidão, mas todas dependem dos dados que são usados. Na verdade, os valores podem ser ausentes ou aproximados, ou os dados podem ter sido alterados por vários processos. Especialmente na fase de exploração e desenvolvimento, você pode decidir aceitar uma determinada quantidade de erros nos dados, especialmente se os dados tiverem características bastante uniformes. Por exemplo, um modelo que prevê vendas para uma loja específica baseado nas vendas anteriores pode estar fortemente correlacionado e ser bastante preciso, mesmo que a loja tenha usado sempre o método de contabilidade errado. Portanto, as medidas de exatidão devem ser equilibradas pelas avaliações de confiança.  
  
 A*confiança* avalia o modo como um modelo de mineração de dados é executado em conjuntos de dados diferentes. Um modelo de mineração de dados é confiável se gerar o mesmo tipo de previsões ou localizar os mesmos tipos gerais de padrões independentemente dos dados de teste fornecidos. Por exemplo, o modelo que você gerar para a loja que usou o método de contabilidade errado não pode ser generalizado para outras lojas e, portanto, não é confiável.  
  
 A*utilidade* inclui várias métricas que informam se o modelo fornece informações úteis. Por exemplo, um modelo de mineração de dados que correlaciona o local da loja com as vendas pode ser exato e confiável, mas não útil, porque você não pode generalizar esse resultado adicionando mais lojas no mesmo local. Além disso, ele não responde à questão empresarial fundamental de por que certos locais têm mais de vendas. Você também pode descobrir que um modelo que parece ter êxito na verdade é insignificante, porque se baseia em correlações cruzadas nos dados.  
  
## <a name="tools-for-testing-and-validation-of-mining-models"></a>Ferramentas para teste e validação de modelos de mineração  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte a várias abordagens para a validação de soluções de mineração de dados, dando suporte a todas as fases da metodologia de teste de mineração de dados.  
  
-   Particionando dados em conjuntos de treinamento e de teste.  
  
-   Filtrando modelos para treinar e testar diferentes combinações dos mesmos dados de origem.  
  
-   Medindo *comparação de precisão* e *ganho*. Um *gráfico de comparação de precisão* é um método de visualização da melhoria obtida com o uso de um modelo de mineração de dados, quando você o compara com uma detecção aleatória.  
  
-   Executando a *validação cruzada* de conjuntos de dados  
  
-   Gerando *matrizes de classificação*. Esses gráficos classificam bons e maus palpites em uma tabela para poder medir com rapidez e facilidade a exatidão da previsão do valor de destino pelo modelo.  
  
-   Criando *dispersões* para avaliar o ajuste de uma fórmula de regressão.  
  
-   Criando *gráficos de ganho* que associam ganhos ou custos financeiros ao uso de um modelo de mineração para que você possa saber o valor das recomendações.  
  
 Essas métricas não pretendem responder se o modelo de mineração de dados atende sua necessidade comercial; em vez disso, essas métricas fornecem medidas objetivas que você pode usar para avaliar a confiabilidade de seus dados para análises preditivas e orientar sua decisão de usar ou não uma iteração específica no processo de desenvolvimento.  
  
 Os tópicos nesta seção fornecem uma visão geral de cada método e orientam o processo de medir a exatidão de modelos que você compila usando a Mineração de Dados do SQL Server.  
  
### <a name="related-topics"></a>Tópicos relacionados  
  
|Tópicos|Links|  
|------------|-----------|  
|Saiba configurar um conjunto de dados de testes usando um assistente ou comandos DMX|[Conjuntos de dados de treinamento e teste](../../analysis-services/data-mining/training-and-testing-data-sets.md)|  
|Saiba testar a distribuição e a representatividade dos dados em uma estrutura de mineração|[Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Saiba mais sobre os tipos de gráfico de precisão fornecidos.|[Gráfico de comparação de precisão &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de ganho &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de dispersão &#40; Analysis Services – mineração de dados &#41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|Saiba criar uma matriz de classificação, às vezes chamada de matriz de confusão, para avaliar o número de verdadeiros e falsos positivos e negativos.|[Matriz de classificação &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de mineração de dados](../../analysis-services/data-mining/data-mining-tools.md)   
 [Soluções de mineração de dados](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Teste e validação de tarefas e instruções &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
