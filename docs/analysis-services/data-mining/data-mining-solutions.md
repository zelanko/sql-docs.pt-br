---
title: "Soluções de mineração de dados | Microsoft Docs"
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
- data mining [Analysis Services], about data mining
- data mining [Analysis Services], development
ms.assetid: 84f6548d-ebb0-4e10-9b29-66253fa0a04a
caps.latest.revision: "64"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 595282e28a55171ed5a528d28f37500a21f71c0d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="data-mining-solutions"></a>Soluções de mineração de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Uma solução de mineração de dados é um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solução que contém um ou mais projetos de mineração de dados.  
  
 Os tópicos desta seção fornecem informações sobre como projetar e implementar uma solução de mineração de dados integrada usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter uma visão geral do processo de design de mineração de dados e as ferramentas relacionadas, consulte [Data Mining Concepts](../../analysis-services/data-mining/data-mining-concepts.md).  
  
 Para obter mais informações sobre os tipos de projetos que são úteis para mineração de dados, consulte [Projetos relacionados a soluções de mineração de dados](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md).  
  
 [Relacional versus Soluções multidimensionais](#bkmk_RelMD)  
  
 [Implantando soluções de mineração de dados](#bkmk_Deploy)  
  
 [Passo a passo de solução](#bkmk_Walkthru)  
  
##  <a name="bkmk_RelMD"></a>Relacional versus Soluções multidimensionais  
 Uma solução de mineração de dados pode ser baseada em dados multidimensionais, ou seja, um cubo existente, ou em dados puramente relacionais, como as tabelas e exibições em um data warehouse, ou em arquivos de texto, pastas de trabalho do Excel ou outras fontes de dados externas.  
  
-   Você pode criar objetos de mineração de dados dentro de uma solução de banco de dados multidimensional existente.  
  
     Normalmente você criaria uma solução como essa se já tivesse criado um cubo e quisesse executar mineração de dados usando o cubo como uma fonte de dados. Quando você move e faz backup de modelos com base em um cubo, o cubo também deve ser movido ou copiado.  
  
-   Você pode criar uma solução de mineração de dados que contém apenas objetos de mineração de dados, inclusive as fontes de dados de apoio e as exibições da fonte de dados, e que usa somente fonte de dados relacional.  
  
     Este é o método preferido para criar modelos de mineração de dados, já que processar e consultar é geralmente mais rápido em fontes de dados relacionais. Você também pode facilmente mover e fazer backup de modelos entre servidores usando os comandos EXPORT e IMPORT.  
  
##  <a name="bkmk_Deploy"></a> Implantando soluções de mineração de dados  
 A instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o qual você implanta a solução deve estar sendo executada em um modo que dá suporte a objetos multidimensionais e objetos de mineração de dados; ou seja, você não pode implantar objetos de mineração de dados em uma instância que hospeda modelos de tabela ou dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Portanto, quando você cria uma solução de mineração de dados no Visual Studio, use o modelo **Projeto Multidimensional e de Mineração de Dados do Analysis Services**.  
  
 Quando você implanta a solução, os objetos usados para mineração de dados são criados na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada, em um banco de dados com o mesmo nome do arquivo de solução.  
  
 Para obter mais informações sobre como implantar soluções relacionais e multidimensionais, consulte [Implantação de soluções de mineração de dados](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md).  
  
##  <a name="bkmk_Walkthru"></a> Passo a passo de solução  
 Fornece uma visão geral de como criar soluções de mineração de dados usando o Assistente de Mineração de Dados.  
  
 [Criar uma estrutura de mineração relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)  
 Crie uma estrutura de mineração de dados relacionais, arquivos de texto e outras origens que podem ser combinadas em uma exibição da fonte de dados.  
  
 [Criar uma estrutura de mineração OLAP](../../analysis-services/data-mining/create-an-olap-mining-structure.md)  
 Criar a estrutura de mineração baseada em dados em um cubo OLAP. Os modelos que você cria dos dados OLAP podem ser salvos como uma dimensão de mineração de dados ou você pode salvar o conjunto de dados e seus modelos como um novo cubo.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Projetos de mineração de dados](../../analysis-services/data-mining/data-mining-projects.md)  
  
 [Processando objetos de Mineração de dados](../../analysis-services/data-mining/processing-data-mining-objects.md)  
  
 [Projetos relacionados a soluções de Mineração de dados](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)  
  
 [Implantação de soluções de mineração de dados](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md)  
  
## <a name="related-tasks-and-topics"></a>Tarefas e tópicos relacionados  
 Depois de você ter criado uma solução de mineração de dados básica, incluindo fontes de dados e uma estrutura de mineração, pode criar a solução adicionando novos modelos, testando e comparando modelos, criando previsões e experimentando com subconjuntos de dados.  
  
 Para obter mais informações, consulte os seguintes links:  
  
|Tarefas|Tópicos|  
|-----------|------------|  
|Teste os modelos que você criou, valide a qualidade de seus dados de treinamento e crie gráficos que representam a precisão de modelos de mineração de dados.|[Teste e validação &#40;Mineração de dados&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|Treine o modelo populando a estrutura e os modelos relacionados com os dados. Atualize e estenda modelos com novos dados.|[Processando objetos de Mineração de dados](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|Personalize um modelo de mineração aplicando filtros aos dados de treinamento, escolhendo um algoritmo diferente ou definindo parâmetros de algoritmo avançados.|[Personalizar os modelos de mineração e a estrutura](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|Personalize um modelo de mineração aplicando filtros aos dados usados no treinamento do modo.|[Adicionar Modelos de Mineração a uma estrutura &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|Atualize e gerencie as soluções de mineração de dados.|Link TBD|  
  
## <a name="see-also"></a>Consulte Também  
 [Tutoriais de Data Mining &#40;Analysis Services&#41;](../../analysis-services/data-mining-tutorials-analysis-services.md)  
  
  
