---
title: Tutorial DMX de previsão de série temporal | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1623f824c062c270268323fd45ebf0e9533c8788
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63044171"
---
# <a name="time-series-prediction-dmx-tutorial"></a>Tutorial DMX de previsão de série temporal
  Neste tutorial, você aprenderá a criar uma estrutura de mineração de série temporal, a criar três modelos de mineração de série temporal e a fazer previsões usando esses modelos.  
  
 Os modelos de mineração são baseados nos dados contidos no banco de dados de exemplo do  [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] , que armazena dados para a empresa fictícia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] é uma grande empresa industrial e multinacional.  
  
## <a name="tutorial-scenario"></a>Cenário do tutorial  
 A [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] decidiu usar a mineração de dados para gerar projeções de vendas. Eles já criaram alguns modelos de previsão regionais; para obter mais informações, consulte [lição 2: Criando um cenário de previsão &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md). No entanto, o Departamento de Vendas precisa ser capaz de atualizar periodicamente o modelo de mineração de dados com novos dados de vendas. Eles também desejam personalizar os modelos para oferecer projeções diferentes.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece várias ferramentas que podem ser usadas para realizar essa [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tarefa:  
  
-   A linguagem de consulta de Extensões de Mineração de Dados (DMX)  
  
-   O algoritmo MTS  
  
-   Editor de Consultas do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 O algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series cria modelos que podem ser usados para previsão de dados relacionados a tempo. DMX (Extensões de Mineração de Dados) é uma linguagem de consulta fornecida pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que pode ser usada para criar modelos de mineração e consultas de previsão.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial pressupõe que você já conheça os objetos usados pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para a criação de modelos de mineração. Se você ainda não criou uma estrutura de mineração ou um modelo de mineração usando DMX, consulte [Bike Buyer DMX Tutorial](../../2014/tutorials/bike-buyer-dmx-tutorial.md).  
  
 Ele se divide nas lições a seguir:  
  
 [Lição 1: Criando um modelo de mineração de série temporal e uma estrutura de mineração](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 Nesta lição, você aprenderá a usar a instrução `CREATE MINING MODEL` para adicionar um novo modelo de previsão e um modelo de mineração relacionado.  
  
 [Lição 2: Adicionando modelos de mineração à estrutura de mineração de série temporal](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
 Nesta lição, você aprenderá a usar a instrução ALTER MINING STRUCTURE para adicionar novos modelos de mineração a uma estrutura de série temporal. Você também aprenderá a personalizar o algoritmo usado para análise de uma série temporal.  
  
 [Lição 3: Processando a estrutura e os modelos de série temporal](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
 Nesta lição, você aprenderá a treinar os modelos usando a instrução `INSERT INTO` e populando a estrutura com dados do banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)].  
  
 [Lição 4: Criando previsões de série temporal usando DMX](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
 Nesta lição, você aprenderá a criar previsões de série temporal.  
  
 [Lição 5: Estendendo o modelo de série temporal](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
 Nesta lição, você aprenderá a usar o parâmetro `EXTEND_MODEL_CASES` para atualizar o modelo com novos dados quando fizer previsões.  
  
## <a name="requirements"></a>Requisitos  
 Antes de fazer este tutorial, verifique se os seguintes itens estão instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   O banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]  
  
 Por padrão, e para reforçar a segurança, os bancos de dados de exemplo não são instalados. Para instalar os bancos de dados de exemplo oficiais [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]do, vá [http://www.CodePlex.com/MSFTDBProdSamples](https://go.microsoft.com/fwlink/?LinkId=88417) para ou no Microsoft SQL Server exemplos e projetos da Comunidade home page na seção Microsoft SQL Server exemplos de produto. Clique em **Bancos de Dados**e, em seguida, clique na guia **Releases** e selecione o banco de dados desejado.  
  
> [!NOTE]  
>  Ao examinar os tutoriais, recomendamos que você adicione os botões **Próximo Tópico** e **Tópico Anterior** à barra de ferramentas do visualizador de documentos.  
  
## <a name="see-also"></a>Consulte Também  
 [Tutorial de mineração de dados básico](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial de mineração de dados intermediário &#40;Analysis Services de mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
