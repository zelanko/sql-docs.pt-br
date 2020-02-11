---
title: Tutorial de mineração de dados básico | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 6602edb6-d160-43fb-83c8-9df5dddfeb9c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d434df95a26485d4d7795d3ab960b8d2457b8ff6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63185578"
---
# <a name="basic-data-mining-tutorial"></a>Tutorial de mineração de dados básico
  Bem-vindo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ao tutorial de mineração de dados básico. [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece um ambiente integrado para criar modelos de data mining e fazer previsões. Neste tutorial, você concluirá um cenário para uma campanha de mala direta na qual usará o aprendizado automatizado para analisar e prever o comportamento de compra do cliente. O tutorial demonstra como usar três dos algoritmos de mineração de dados mais importantes: clustering, árvores de decisão, e Naive Bayes. Você também aprenderá a analisar suas descobertas usando os visualizadores do modelo de mineração e a criar previsões e gráficos de precisão usando as ferramentas de Data Mining incluídas no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. A empresa fictícia, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], é usada para todos os exemplos.  
  
 Quando você estiver confortável usando as ferramentas de Data Mining, recomendamos que também conclua o [tutorial de mineração de dados intermediário &#40;Analysis Services-&#41;de mineração de dados ](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). As lições demonstram como usar previsão, análise da cesta de compras, série temporal, modelos de associação, tabelas aninhadas, e clustering de sequência.  
  
## <a name="tutorial-scenario"></a>Cenário do tutorial  
 Nesse tutorial, você é funcionário da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] , que recebeu a tarefa de saber mais sobre os clientes da empresa, com base nos históricos das compras, e usar esses dados históricos para desenvolver previsões que poderão ser usadas em marketing. A empresa nunca tinha realizado a mineração de dados antes, por isso você deve criar um novo banco de dados especificamente para a mineração de dados e definir vários modelos de mineração.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial ensina como criar e trabalhar com vários tipos diferentes de métodos automatizados de aprendizado. Você também aprenderá como criar uma cópia de um modelo de mineração, e aplicar um filtro aos dados de entrada para obter resultados diferentes. Depois, você poderá comparar os resultados de ambos os modelos, usando um gráfico de comparação de precisão. Por fim, você usará o detalhamento para recuperar dados adicionais da estrutura de mineração subjacente.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] A mineração de dados inclui os seguintes recursos que ajudam você a desenvolver e comparar facilmente vários modelos de previsão e, em seguida, executar ações nos resultados:  
  
-   *Conjuntos de testes de controle-* Ao criar uma estrutura de mineração, agora você pode dividir os dados na estrutura de mineração em conjuntos de treinamento e teste. Isso permite testar modelos em conjuntos de dados semelhantes e comparar a exatidão de modelos relacionados.  
  
-   *Filtros do modelo de mineração-* Agora você pode anexar filtros a um modelo de mineração e aplicar o filtro durante o treinamento e o teste. Isso permite criar facilmente modelos relacionados em diferentes subconjuntos dos dados.  
  
-   *Detalhamento para casos de estrutura e colunas de estrutura-* Agora você pode facilmente mover de padrões gerais no modelo de mineração para detalhes acionáveis na fonte de dados.  
  
 Ele se divide nas lições a seguir:  
  
 [Lição 1: preparando o Analysis Services de dados &#40;o tutorial básico de Data Mining&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 Nesta lição, você aprenderá a criar um novo banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , a adicionar uma fonte de dados e uma exibição da fonte de dados, bem como a preparar o novo banco de dados para ser usado com a mineração de dados.  
  
 [Lição 2: criando uma estrutura de endereçamento direcionada &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 Nesta lição, você aprenderá a criar uma estrutura de modelo de mineração que poderá ser usada como parte de um cenário de mala direta.  
  
 [Lição 3: Adicionando e processando modelos](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 Nesta lição, você aprenderá a adicionar modelos a uma estrutura. Os modelos criados por você serão desenvolvidos com os seguintes algoritmos:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)]Árvores de decisão  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)]Clustering  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)]Naive Bayes  
  
 [Lição 4: explorando os modelos de mala direta direcionados &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 Nesta lição, você aprenderá a explorar e a interpretar as descobertas de cada modelo usando os Visualizadores.  
  
 [Lição 5: testando modelos &#40;o tutorial de mineração de dados básico&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 Nesta lição, você fará uma cópia de um dos modelos de mala direta, adicionará um filtro de modelo de mineração para restringir os dados de treinamento a um determinado conjunto de clientes e avaliará a viabilidade do modelo.  
  
 [Lição 6: Criando e trabalhando com previsões &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 Na última lição do Tutorial de mineração de dados básico, você usará o modelo para prever que clientes têm mais probabilidade de comprar uma bicicleta. Em seguida, você detalhará os casos subjacentes para obter informações de contato.  
  
## <a name="requirements"></a>Requisitos  
 Verifique se os seguintes itens estão instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   O banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
 Para aumentar a segurança, os bancos de dados de exemplo não são instalados com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para instalar os bancos de dados oficiais do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], visite a página [Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417) e selecione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Ao trabalhar com um tutorial, talvez você ache mais fácil ir e voltar entre as etapas se adicionar os botões **Próximo tópico** e **Tópico anterior** à barra de ferramentas do visualizador de documentos.  
  
## <a name="see-also"></a>Consulte Também  
 [Soluções de mineração de dados](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [Tarefas e instruções do modelo de mineração](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Criando e consultando modelos de mineração de dados com DMX: Tutoriais &#40;Analysis Services&#41;de mineração de dados](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
