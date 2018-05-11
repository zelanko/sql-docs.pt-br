---
title: Ferramentas de mineração de dados | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 88ba4cfe18d0f4e4ce0d4ac35b708968cc30a70a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="data-mining-tools"></a>Ferramentas de mineração de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece as seguintes ferramentas que podem ser usadas para criar soluções de mineração de dados:  
  
-   O **Assistente de Mineração de Dados** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] facilita a criação de estruturas e modelos de mineração usando fontes de dados relacionais ou dados multidimensionais em cubos.  
  
     No assistente, você escolhe dados para usar e em seguida aplica técnicas específicas de mineração de dados como clustering, redes neurais ou modelagem de série temporal.  
  
-   Os**visualizadores de modelos** são fornecidos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], para explorar seus modelos de mineração depois que são criados.  Você pode procurar modelos usando visualizadores feitos especialmente para cada algoritmo ou se aprofundar mais na análise usando o visualizador de conteúdo do modelo.  
  
-   O **Construtor de Consultas de Previsão** é fornecido no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para ajudá-lo a criar consultas de previsão. Você também pode testar a precisão de modelos em um conjunto de dados de validação ou dados externos, ou usar validação cruzada para avaliar a qualidade de seu conjunto de dados.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é a interface onde você gerencia as soluções de mineração de dados existentes que foram implantadas em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Você pode reprocessar estruturas e modelos para atualizar os dados neles.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contém ferramentas que você pode usar para limpar dados, automatizar tarefas tais como a criação de previsões e a atualização de modelos, e para criar soluções de mineração de texto.  
  
 As seções a seguir oferecem mais informações sobre as ferramentas de mineração de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="data-mining-wizard"></a>Assistente de Mineração de Dados  
 Use o Assistente de Mineração de Dados para começar a criar soluções de mineração de dados. O assistente é fácil e rápido, e foi criado para guiá-lo no processo de criação de uma estrutura de mineração de dados e um modelo de mineração inicial relacionado; além disso, inclui as tarefas de seleção de um tipo de algoritmo e uma fonte de dados, bem como de definição dos dados de caso usados para a análise.  
  
 **Para obter mais informações:** [Assistente de Mineração de Dados &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)  
  
## <a name="data-mining-designer"></a>Designer de Mineração de Dados  
 Após ter criado uma estrutura de mineração e um modelo de mineração usando o Assistente de Mineração de Dados, você pode utilizar o Designer de Mineração de Dados do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para trabalhar com modelos e estruturas existentes.  
  
 O designer inclui ferramentas para estas tarefas:  
  
-   Modifique as propriedades de estruturas de mineração, adicione colunas e crie aliases de coluna, altere o método de compartimento ou a distribuição de valores esperada.  
  
-   Adicione novos modelos a uma estrutura existente; copie modelos, altere as propriedades do modelo ou metadados, ou defina filtros em um modelo de mineração.  
  
-   Procure os padrões e as regras dentro do modelo; explore associações ou árvores de decisão. Obter estatísticas detalhadas sobre  
  
     Os visualizadores padrão são fornecidos para cada momento diferente do modelo, para ajudá-lo a analisar seus dados e explorar os padrões revelados pela mineração de dados.  
  
-   Valide modelos criando gráficos de comparação de precisão ou analisando a curva de lucro para modelos. Compare modelos usando matrizes de classificação ou valide um conjunto de dados e seus modelos usando validação cruzada.  
  
-   Crie previsões e consultas de conteúdo em modelos de mineração existentes. Crie consultas únicas ou configure consultas para gerar previsões para tabelas inteiras de dados externos.  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Depois que você criar e implantar modelos de mineração em um servidor, pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerenciar o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospeda os objetos de mineração de dados. Você também pode continuar executando tarefas que usam o modelo, como explorar os modelos, processar novos dados e criar previsões.  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] também contém editores de consulta que você pode usar para criar e executar consultas de extensões DMX ou para trabalhar com objetos de mineração de dados usando XMLA.  
  
## <a name="integration-services-data-mining-tasks-and-transformations"></a>Tarefas e transformações de serviços de mineração de dados de integração  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece muitos componentes que dão suporte à mineração de dados.  
  
 Algumas ferramentas no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são criadas para ajudar a automatizar tarefas comuns de mineração de dados, incluindo previsão, criação de modelo e processamento. Por exemplo:  
  
-   Crie um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que automaticamente atualiza o modelo toda vez que o conjunto de dados é atualizado com novos clientes  
  
-   Execute a segmentação personalizada ou amostragem personalizada de registros de casos.  
  
-   Automaticamente gere modelos passados em parâmetros.  
  
 Porém, você também pode usar a mineração de dados em um fluxo de trabalho de pacote, como uma entrada para outros processos. Por exemplo:  
  
-   Use valores de probabilidade gerados pelo modelo para pesar pontuações para mineração de texto ou outras tarefas de classificação.  
  
-   Automaticamente gere previsões com base em dados anteriores e use esses valores para avaliar a validade de novos dados.  
  
-   Usando regressão logística para segmentar clientes de entrada por risco.  
  
 **Para obter mais informações:** [Projetos relacionados a soluções de mineração de dados](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados & #40; DMX & #41; Referência](../../dmx/data-mining-extensions-dmx-reference.md)   
 [Tutoriais e tarefas do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Tarefas do Visualizador do modelo e instruções de mineração](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Soluções de mineração de dados](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
