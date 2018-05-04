---
title: Designer de mineração de dados | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f14ec670668253fa9e37db9647d5ef511150816
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-designer"></a>Designer de Mineração de Dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O Designer de Mineração de Dados é o ambiente primário para trabalhar com modelos de mineração no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Você pode acessar o designer selecionando uma estrutura de mineração existente ou usando o Assistente de Mineração de Dados para criar uma nova estrutura e um novo modelo de mineração. É possível usar o Designer de Mineração de Dados para executar as seguintes tarefas:  
  
-   Modificar a estrutura de mineração e o modelo de mineração criados inicialmente pelo Assistente de Mineração de Dados.  
  
-   Criar novos modelos baseados em uma estrutura de mineração existente.  
  
-   Treinar e procurar modelos de mineração.  
  
-   Comparar modelos usando gráficos de exatidão.  
  
-   Criar consultas de previsão baseadas em modelos de mineração.  
  
## <a name="mining-structure-tab"></a>Guia Estrutura de Mineração  
 Use a guia **Estrutura de Mineração** para adicionar colunas e modificar as propriedades de uma estrutura de mineração existente. As seguintes tarefas e tópicos fornecem mais informações sobre o trabalho com estruturas de mineração:  
  
 [Estruturas de mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
 [Tarefas de estrutura de mineração e instruções](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>Guia Modelos de Mineração  
 Use a guia **Modelos de Mineração** para administrar modelos de mineração existentes e criar novos modelos. Os modelos de mineração sempre se baseiam em uma estrutura de mineração existente.  
  
 Na guia **Modelos de Mineração** , é possível alterar o tipo de algoritmo, adicionar ou remover colunas associadas à estrutura de modelo, ajustar as propriedades de coluna específicas do algoritmo, especificar o uso da coluna de modelo de mineração e ajustar os parâmetros de algoritmo associados ao modelo de mineração. Também é possível processar a estrutura de mineração junto com os modelos selecionados ou todos os modelos associados.  
  
 Consulte os seguintes tópicos para obter mais informações sobre o trabalho com modelos de mineração:  
  
 [Modelos de mineração & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
 [Tutoriais e tarefas do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>Guia Visualizador do Modelo de Mineração  
 Use a guia **Visualizador do Modelo de Mineração** para explorar seus modelos de mineração visualmente. Cada modelo de mineração é associado a um visualizador personalizado que exibe o conteúdo específico desse modelo. Você também pode exibir o conteúdo de modelo de mineração usando o visualizador de conteúdo.  
  
 Consulte os seguintes tópicos para obter mais informações sobre a exploração de modelos de mineração com os visualizadores de mineração de dados:  
  
 [Visualizadores do modelo de mineração de dados](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
 [Tarefas do Visualizador do modelo e instruções de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>Guia Gráfico de Precisão de Mineração  
 Use a guia **Gráfico de Precisão de Mineração** para testar a precisão de previsão de um único modelo de mineração ou comparar a eficiência de vários modelos de mineração contidos em uma estrutura de mineração. A guia contém ferramentas para filtrar dados, selecionar modelos de mineração e exibir os resultados em um gráfico de comparação de precisão, gráfico de ganho ou matriz de classificação.  
  
 Consulte os seguintes tópicos para obter mais informações sobre o teste e a validação de modelos de mineração:  
  
 [Teste e validação &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
 [Teste e validação de tarefas e instruções &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>Guia Previsão do Modelo de Mineração  
 A guia **Previsão do Modelo de Mineração** inclui o Construtor de Consultas de Previsão, que pode ser usado para criar uma consulta de previsão de extensões DMX. A guia contém ferramentas para especificar modelos de mineração e tabelas de entrada, mapear as colunas no modelo de mineração para colunas na tabela de entrada, adicionar funções a uma consulta e especificar critérios para cada coluna.  
  
 Depois de criar uma consulta, você pode usar diferentes exibições na guia para exibir os resultados da consulta e modificar a consulta manualmente. Você também pode salvar os resultados da consulta em uma tabela de um banco de dados.  
  
 Consulte os seguintes tópicos para obter mais informações sobre a criação de consultas de mineração de dados:  
  
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)  
  
 [Tutoriais e tarefas de consulta de mineração de dados](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>Consulte também  
 [Soluções de mineração de dados](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
