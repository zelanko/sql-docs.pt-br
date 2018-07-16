---
title: Tutorial de mineração de dados básico | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 6602edb6-d160-43fb-83c8-9df5dddfeb9c
caps.latest.revision: 48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5711bc105432b0d23f5fd2fd2b429449c2549258
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314966"
---
# <a name="basic-data-mining-tutorial"></a>Tutorial de mineração de dados básico
  Bem-vindo à [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial de mineração de dados básico. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Fornece um ambiente integrado para criação de modelos de mineração de dados e fazer previsões. Neste tutorial, você concluirá um cenário para uma campanha de mala direta na qual usará o aprendizado automatizado para analisar e prever o comportamento de compra do cliente. O tutorial demonstra como usar três dos algoritmos de mineração de dados mais importantes: clustering, árvores de decisão, e Naive Bayes. Você também aprenderá como analisar os resultados usando os visualizadores de modelo de mineração e para criar previsões e gráficos de precisão usando as ferramentas de mineração de dados que estão incluídas no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. A empresa fictícia, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], é usada para todos os exemplos.  
  
 Quando você estiver familiarizado com o uso de ferramentas de mineração de dados, recomendamos que conclua também o [Tutorial intermediário de mineração de dados &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). As lições demonstram como usar previsão, análise da cesta de compras, série temporal, modelos de associação, tabelas aninhadas, e clustering de sequência.  
  
## <a name="tutorial-scenario"></a>Cenário do tutorial  
 Neste tutorial, você é funcionário da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] que recebeu a aprender mais sobre os clientes da empresa com base nos históricos das compras e, em seguida, usar esses dados históricos para desenvolver previsões que podem ser usadas em marketing. A empresa nunca tinha realizado a mineração de dados antes, por isso você deve criar um novo banco de dados especificamente para a mineração de dados e definir vários modelos de mineração.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial ensina como criar e trabalhar com vários tipos diferentes de métodos automatizados de aprendizado. Você também aprenderá como criar uma cópia de um modelo de mineração, e aplicar um filtro aos dados de entrada para obter resultados diferentes. Depois, você poderá comparar os resultados de ambos os modelos, usando um gráfico de comparação de precisão. Por fim, você usará o detalhamento para recuperar dados adicionais da estrutura de mineração subjacente.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Mineração de dados inclui os seguintes recursos que ajudam você a facilmente desenvolver e comparar vários modelos preditivos e tomar providências sobre os resultados:  
  
-   *Conjuntos de Testes de Controle -* ao criar uma estrutura de mineração, você poderá dividir os dados na estrutura de mineração em conjuntos de treinamento e teste. Isso permite testar modelos em conjuntos de dados semelhantes e comparar a exatidão de modelos relacionados.  
  
-   *Filtros de modelo de mineração -* agora é possível anexar filtros a um modelo de mineração e aplicá-lo durante o treinamento e o teste. Isso permite criar facilmente modelos relacionados em diferentes subconjuntos dos dados.  
  
-   *Detalhamento para casos de estrutura e colunas de estrutura -* agora você pode se mover facilmente dos padrões gerais do modelo de mineração para detalhes acionáveis na fonte de dados.  
  
 Ele se divide nas lições a seguir:  
  
 [Lição 1: Preparar a análise de serviços de banco de dados &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 Nesta lição, você aprenderá a criar um novo banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a adicionar uma fonte de dados e uma exibição da fonte de dados, bem como a preparar o novo banco de dados para ser usado com a mineração de dados.  
  
 [Lição 2: Criando uma estrutura de mala direta &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 Nesta lição, você aprenderá a criar uma estrutura de modelo de mineração que poderá ser usada como parte de um cenário de mala direta.  
  
 [Lição 3: Adicionando e processando modelos](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 Nesta lição, você aprenderá a adicionar modelos a uma estrutura. Os modelos criados por você serão desenvolvidos com os seguintes algoritmos:  
  
-   Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering  
  
-   Naive Bayes da [!INCLUDE[msCoName](../includes/msconame-md.md)]  
  
 [Lição 4: Explorando os modelos de mala direta &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 Nesta lição, você aprenderá a explorar e a interpretar as descobertas de cada modelo usando os Visualizadores.  
  
 [Lição 5: Testando modelos &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 Nesta lição, você fará uma cópia de um dos modelos de mala direta, adicionará um filtro de modelo de mineração para restringir os dados de treinamento a um determinado conjunto de clientes e avaliará a viabilidade do modelo.  
  
 [Lição 6: Criando e trabalhando com previsões &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 Na última lição do Tutorial de mineração de dados básico, você usará o modelo para prever que clientes têm mais probabilidade de comprar uma bicicleta. Em seguida, você detalhará os casos subjacentes para obter informações de contato.  
  
## <a name="requirements"></a>Requisitos  
 Verifique se os seguintes itens estão instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no modo multidimensional  
  
-   O banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)].  
  
 Para aumentar a segurança, os bancos de dados de exemplo não são instalados com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para instalar o banco de dados oficiais [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], visite o [Microsoft SQL Sample Databases](http://go.microsoft.com/fwlink/?LinkId=88417) página e selecione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Ao trabalhar com um tutorial, talvez você ache mais fácil ir e voltar entre as etapas se adicionar os botões **Próximo tópico** e **Tópico anterior** à barra de ferramentas do visualizador de documentos.  
  
## <a name="see-also"></a>Consulte também  
 [Soluções de mineração de dados](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [Tarefas e tarefas do modelo de mineração](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Criando e consultando modelos de mineração de dados com DMX: tutoriais &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
