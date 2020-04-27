---
title: Tutorial de mineração de dados intermediários (Analysis Services-Mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 404b31d5-27f4-4875-bd60-7b2b8613eb1b
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4c244701d8a58765061ef3bde1f918c8be5a941d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63017175"
---
# <a name="intermediate-data-mining-tutorial-analysis-services---data-mining"></a>Tutorial de mineração de dados intermediário (Analysis Services – Mineração de dados)
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece um ambiente integrado para criar e trabalhar com modelos de data mining. Você pode se associar com facilidade a fontes de dados, criar e testar vários modelos com os mesmos dados e implantar modelos a serem usados na análise de previsão.  
  
 No tutorial básico de mineração de dados, você aprendeu a usar o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar uma solução de data mining e construiu três modelos para dar suporte a uma campanha de mala direta para análise de comportamento de compra de clientes e para atingir compradores potenciais.  
  
 Esse tutorial intermediário desenvolve essa experiência e apresenta diversos cenários novos, inclusive requisitos de negócios comuns como a previsão e a análise de cesta de compras. Você aprenderá a criar um modelo de série temporal, um modelo de associação e um modelo de clustering de sequência. Finalmente, você aprenderá a usar a rede neural para explorar correlações em dados e a usar a regressão logística para previsões.  
  
 As lições são independentes e podem ser concluídas separadamente.  
  
 Para concluir os tutoriais a seguir, você deve estar familiarizado com as ferramentas de mineração de dados e os visualizadores de modelo de mineração apresentados no Tutorial de mineração de dados básico.  
  
 Todos os cenários usam a fonte de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], mas você criará exibições da fonte de dados diferentes para cenários diferentes. Você poderá fazer as lições em qualquer ordem, desde que crie a fonte de dados primeiro.  
  
## <a name="lesson-scenarios"></a>Cenários das lições  
 Depois do seu sucesso com a campanha de mala direta, será preciso aplicar o seu conhecimento de mineração de dados no desenvolvimento de vários novos modelos a serem usados no planejamento comercial. As seguintes tarefas estão incluídas:  
  
-   **Previsão:** Você criará um modelo de *série temporal* para prever as vendas de produtos em regiões diferentes em todo o mundo. Você desenvolverá modelos individuais para cada região e aprenderá a usar a *previsão cruzada*.  
  
-   **Análise da cesta de compras:** Você criará um *modelo de associação*para analisar agrupamentos de produtos que são comprados durante visitas ao [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] site de comércio eletrônico. Com base nesse modelo de cesta de compras, você pode recomendar produtos aos clientes.  
  
-   **Análise de sequência:** Você cria um *modelo de clustering de sequência*, para analisar a ordem em que os clientes compram produtos. Com base nesse modelo, é possível planejar alterações no design do site ou novas ofertas de produtos.  
  
-   **Análise de fator:** Você usa um modelo de *rede neural* para explorar as possíveis causas da baixa qualidade de serviço nos dados do Call Center. Com base nas informações do modelo preliminar, você criará um *modelo de regressão logística* para prever estratégias para melhorar a experiência do cliente.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial ensina como criar e trabalhar com vários tipos de algoritmos de mineração de dados. Ele se divide nas lições a seguir:  
  
 [Lição 1: criando a solução intermediária de mineração de dados &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
 Nesta lição, você criará um novo projeto com base no banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] para dar suporte a várias exibições da fonte de dados e muitos outros modelos de mineração.  
  
 [Lição 2: Criando um cenário de previsão &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
 Nesta lição, você criará um modelo de mineração que pode ser usado como parte de um cenário de previsão. Você também vai explorar modelos de mineração criados com o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series.  
  
 Você desenvolverá modelos para regiões individuais e criará um modelo geral a ser usado para previsão cruzada.  
  
 [Lição 3: Criando um cenário de cesta de compras &#40;Tutorial intermediário de mineração de dados&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
 Nesta lição, você adicionará uma nova exibição da fonte de dados e aprenderá a trabalhar com tabelas aninhadas e com chaves. Com base nesses dados, criará um modelo de mineração que poderá ser usado como parte de um cenário de cesta de compras. Você também vai explorar modelos de mineração criados com o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association.  
  
 [Lição 4: Criando um cenário de clustering de sequência &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
 Nesta lição, você criará um modelo de mineração que poderá ser usado como parte de um cenário de clustering de sequências. Você também aprenderá a explorar modelos de mineração criados com o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering.  
  
 [Lição 5: Criando modelos de rede neural e de regressão logística &#40;Tutorial intermediário de Data Mining&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
 Nesta lição, você criará vários modelos de mineração relacionados, usando os algoritmos Rede Neural da Microsoft e Regressão Logística da Microsoft. Você também aprenderá a trabalhar com exibições da fontes de dados e explorar dados subjacentes aos modelos.  
  
## <a name="requirements"></a>Requisitos  
 Verifique se os seguintes itens estão instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o banco de dados do [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
 Por padrão, e para reforçar a segurança, os bancos de dados de exemplo não são instalados. Para instalar os bancos de dados oficiais do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], visite a página bancos de dados de [exemplo do Microsoft SQL](https://go.microsoft.com/fwlink/?LinkId=88417) e selecione a versão apropriada do banco de dados de exemplo.  
  
## <a name="see-also"></a>Consulte Também  
 [Tutorial de mineração de dados básico](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial DMX do comprador de bicicletas](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [Tutorial de DMX do Market Basket](../../2014/tutorials/market-basket-dmx-tutorial.md)  
  
  
