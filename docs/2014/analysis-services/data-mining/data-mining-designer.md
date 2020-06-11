---
title: Designer de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], modifying
- data mining editor [Analysis Services]
- Data Mining Designer
- data mining [Analysis Services], modifying
ms.assetid: 2540db5b-2bf3-4b6c-87c8-79c48d71acce
author: minewiskan
ms.author: owend
ms.openlocfilehash: 98176d54f6cdf29be5c06563ec1dbd7fd6275724
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523158"
---
# <a name="data-mining-designer"></a>Data Mining Designer
  O designer de mineração de dados é o ambiente primário no qual você trabalha com modelos de mineração no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você pode acessar o designer selecionando uma estrutura de mineração existente ou usando o Assistente de Mineração de Dados para criar uma nova estrutura e um novo modelo de mineração. É possível usar o Designer de Mineração de Dados para executar as seguintes tarefas:  
  
-   Modificar a estrutura de mineração e o modelo de mineração criados inicialmente pelo Assistente de Mineração de Dados.  
  
-   Criar novos modelos baseados em uma estrutura de mineração existente.  
  
-   Treinar e procurar modelos de mineração.  
  
-   Comparar modelos usando gráficos de exatidão.  
  
-   Criar consultas de previsão baseadas em modelos de mineração.  
  
## <a name="mining-structure-tab"></a>Guia Estrutura de Mineração  
 Use a guia **Estrutura de Mineração** para adicionar colunas e modificar as propriedades de uma estrutura de mineração existente. As seguintes tarefas e tópicos fornecem mais informações sobre o trabalho com estruturas de mineração:  
  
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](mining-structures-analysis-services-data-mining.md)  
  
 [Tarefas e instruções da estrutura de mineração](mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>Guia Modelos de Mineração  
 Use a guia **Modelos de Mineração** para administrar modelos de mineração existentes e criar novos modelos. Os modelos de mineração sempre se baseiam em uma estrutura de mineração existente.  
  
 Na guia **Modelos de Mineração** , é possível alterar o tipo de algoritmo, adicionar ou remover colunas associadas à estrutura de modelo, ajustar as propriedades de coluna específicas do algoritmo, especificar o uso da coluna de modelo de mineração e ajustar os parâmetros de algoritmo associados ao modelo de mineração. Também é possível processar a estrutura de mineração junto com os modelos selecionados ou todos os modelos associados.  
  
 Consulte os seguintes tópicos para obter mais informações sobre o trabalho com modelos de mineração:  
  
 [Modelos de mineração &#40;Analysis Services – Data Mining&#41;](mining-models-analysis-services-data-mining.md)  
  
 [Tarefas e instruções do modelo de mineração](mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>Guia Visualizador do Modelo de Mineração  
 Use a guia **Visualizador do Modelo de Mineração** para explorar seus modelos de mineração visualmente. Cada modelo de mineração é associado a um visualizador personalizado que exibe o conteúdo específico desse modelo. Você também pode exibir o conteúdo de modelo de mineração usando o visualizador de conteúdo.  
  
 Consulte os seguintes tópicos para obter mais informações sobre a exploração de modelos de mineração com os visualizadores de mineração de dados:  
  
 [Visualizadores do Modelo de Mineração de Dados](data-mining-model-viewers.md)  
  
 [Tarefas e instruções do visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>Guia Gráfico de Precisão de Mineração  
 Use a guia **Gráfico de Precisão de Mineração** para testar a precisão de previsão de um único modelo de mineração ou comparar a eficiência de vários modelos de mineração contidos em uma estrutura de mineração. A guia contém ferramentas para filtrar dados, selecionar modelos de mineração e exibir os resultados em um gráfico de comparação de precisão, gráfico de ganho ou matriz de classificação.  
  
 Consulte os seguintes tópicos para obter mais informações sobre o teste e a validação de modelos de mineração:  
  
 [Teste e validação &#40;Mineração de dados&#41;](testing-and-validation-data-mining.md)  
  
 [Tarefas de teste e validação e instruções &#40;Mineração de dados&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>Guia Previsão do Modelo de Mineração  
 A guia **Previsão do Modelo de Mineração** inclui o Construtor de Consultas de Previsão, que pode ser usado para criar uma consulta de previsão de extensões DMX. A guia contém ferramentas para especificar modelos de mineração e tabelas de entrada, mapear as colunas no modelo de mineração para colunas na tabela de entrada, adicionar funções a uma consulta e especificar critérios para cada coluna.  
  
 Depois de criar uma consulta, você pode usar diferentes exibições na guia para exibir os resultados da consulta e modificar a consulta manualmente. Você também pode salvar os resultados da consulta em uma tabela de um banco de dados.  
  
 Consulte os seguintes tópicos para obter mais informações sobre a criação de consultas de mineração de dados:  
  
 [Consultas de mineração de dados](data-mining-queries.md)  
  
 [Tarefas e instruções de consulta de Data Mining](data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Soluções de mineração de dados](data-mining-solutions.md)  
  
  
