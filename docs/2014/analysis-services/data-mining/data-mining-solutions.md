---
title: Soluções de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], about data mining
- data mining [Analysis Services], development
ms.assetid: 84f6548d-ebb0-4e10-9b29-66253fa0a04a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d5a5126048928e66fd8351bc00226cadb2de54d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084886"
---
# <a name="data-mining-solutions"></a>Soluções de mineração de dados
  Uma solução de mineração de dados é uma solução do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém um ou mais projetos de mineração de dados.  
  
 Os tópicos nesta seção fornecem informações sobre como projetar e implementar uma solução de Data Mining integrada usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]o. Para obter uma visão geral do processo de design de mineração de dados e as ferramentas relacionadas, consulte [Data Mining Concepts](data-mining-concepts.md).  
  
 Para obter mais informações sobre os tipos de projetos que são úteis para mineração de dados, consulte [Projetos relacionados a soluções de mineração de dados](data-mining-solutions.md).  
  
 [Relacional versus soluções multidimensionais](#bkmk_RelMD)  
  
 [Implantando soluções de mineração de dados](#bkmk_Deploy)  
  
 [Orientações da solução](#bkmk_Walkthru)  
  
##  <a name="bkmk_RelMD"></a>Relacional versus soluções multidimensionais  
 Uma solução de Data Mining pode ser baseada em dados multidimensionais, ou seja, um cubo existente ou dados puramente relacionais, como as tabelas e exibições em uma data warehouse, ou em arquivos de texto, pastas de trabalho do Excel ou outras fontes de dados externas.  
  
-   Você pode criar objetos de mineração de dados dentro de uma solução de banco de dados multidimensional existente.  
  
     Normalmente você criaria uma solução como essa se já tivesse criado um cubo e quisesse executar mineração de dados usando o cubo como uma fonte de dados. Quando você move e faz backup de modelos com base em um cubo, o cubo também deve ser movido ou copiado.  
  
-   Você pode criar uma solução de mineração de dados que contém apenas objetos de mineração de dados, inclusive as fontes de dados de apoio e as exibições da fonte de dados, e que usa somente fonte de dados relacional.  
  
     Este é o método preferido para criar modelos de mineração de dados, já que processar e consultar é geralmente mais rápido em fontes de dados relacionais. Você também pode facilmente mover e fazer backup de modelos entre servidores usando os comandos EXPORT e IMPORT.  
  
##  <a name="bkmk_Deploy"></a>Implantando soluções de mineração de dados  
 A instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o qual você implanta a solução deve estar sendo executada em um modo que dá suporte a objetos multidimensionais e objetos de mineração de dados; ou seja, você não pode implantar objetos de mineração de dados em uma instância que hospeda modelos de tabela ou dados PowerPivot.  
  
 Portanto, quando você cria uma solução de mineração de dados no Visual Studio, use o modelo **Projeto Multidimensional e de Mineração de Dados do Analysis Services**.  
  
 Quando você implanta a solução, os objetos usados para mineração de dados são criados na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada, em um banco de dados com o mesmo nome do arquivo de solução.  
  
 Para obter mais informações sobre como implantar soluções relacionais e multidimensionais, consulte [Implantação de soluções de mineração de dados](deployment-of-data-mining-solutions.md).  
  
##  <a name="bkmk_Walkthru"></a>Instruções da solução  
 Fornece uma visão geral de como criar soluções de mineração de dados usando o Assistente de Mineração de Dados.  
  
 [Criar uma estrutura de mineração relacional](create-a-relational-mining-structure.md)  
 Crie uma estrutura de mineração de dados relacionais, arquivos de texto e outras origens que podem ser combinadas em uma exibição da fonte de dados.  
  
 [Criar uma estrutura de mineração OLAP](create-an-olap-mining-structure.md)  
 Criar a estrutura de mineração baseada em dados em um cubo OLAP. Os modelos que você cria dos dados OLAP podem ser salvos como uma dimensão de mineração de dados ou você pode salvar o conjunto de dados e seus modelos como um novo cubo.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Projetos de mineração de dados](data-mining-projects.md)  
  
 [Processando objetos de mineração de dados](processing-data-mining-objects.md)  
  
 [Projetos relacionados a soluções de mineração de dados](data-mining-solutions.md)  
  
 [Implantação de soluções de mineração de dados](deployment-of-data-mining-solutions.md)  
  
## <a name="related-tasks-and-topics"></a>Tarefas e tópicos relacionados  
 Depois de você ter criado uma solução de mineração de dados básica, incluindo fontes de dados e uma estrutura de mineração, pode criar a solução adicionando novos modelos, testando e comparando modelos, criando previsões e experimentando com subconjuntos de dados.  
  
 Para obter mais informações, consulte os links a seguir:  
  
|Tarefas|Tópicos|  
|-----------|------------|  
|Teste os modelos que você criou, valide a qualidade de seus dados de treinamento e crie gráficos que representam a precisão de modelos de mineração de dados.|[Teste e validação &#40;mineração de dados&#41;](testing-and-validation-data-mining.md)|  
|Treine o modelo populando a estrutura e os modelos relacionados com os dados. Atualize e estenda modelos com novos dados.|[Processando objetos de mineração de dados](processing-data-mining-objects.md)|  
|Personalize um modelo de mineração aplicando filtros aos dados de treinamento, escolhendo um algoritmo diferente ou definindo parâmetros de algoritmo avançados.|[Personalizar os modelos de mineração e a estrutura](customize-mining-models-and-structure.md)|  
|Personalize um modelo de mineração aplicando filtros aos dados usados no treinamento do modo.|[Adicionar modelos de mineração a uma estrutura &#40;mineração de dados Analysis Services&#41;](add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|Atualize e gerencie as soluções de mineração de dados.|Link TBD|  
  
## <a name="see-also"></a>Consulte Também  
 [Tutoriais de mineração de dados &#40;Analysis Services&#41;](../data-mining-tutorials-analysis-services.md)  
  
  
