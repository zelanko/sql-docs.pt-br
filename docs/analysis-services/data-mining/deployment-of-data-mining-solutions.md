---
title: "Implantação de soluções de mineração de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], deploying
- deploying [Analysis Services], production environments
- deploying [Analysis Services - data mining]
- solutions [Analysis Services], deploying
- models [Analysis Services], data mining
ms.assetid: d83effc7-437d-42e9-8ac3-b65f79e27043
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e40b686c7aa60b023600e17170c33e2ba7b776be
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="deployment-of-data-mining-solutions"></a>Implantação de soluções de mineração de dados
  A última etapa no processo de mineração de dados é implantar os modelos para um ambiente de produção. A implantação é importante porque torna os modelos disponíveis para usuários, para que você possa executar qualquer uma das tarefas a seguir:  
  
-   Use os modelos para criar previsões e tomar decisões comerciais. Para obter informações sobre as ferramentas que você pode usar para criar consultas, consulte [Ferramentas de Consulta de Data Mining](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
-   Insira a funcionalidade de mineração de dados diretamente em um aplicativo. Você pode incluir AMO (Objetos de Gerenciamento de Análise) ou um assembly que contém um conjunto de objetos que seu aplicativo pode usar para criar, alterar, processar e excluir estruturas e modelos de mineração.  
  
-   Crie relatórios que permitem que os usuários solicitem previsões, exibam tendências ou comparem modelos.  
  
 Esta seção fornece informações detalhadas sobre as opções de implantação.  
  
 [Requisitos para a implantação de soluções de mineração de dados](#bkmk_Reqs)  
  
 [Implantando uma solução relacional](#bkmk_RelationalSltn)  
  
 [Implantando uma solução multidimensional](#bkmk_MDSltn)  
  
 [Recursos relacionados](#bkmk_Resources)  
  
## <a name="in-this-section"></a>Nesta seção  
 [Implantar uma solução de mineração de dados em versões anteriores do SQL Server](../../analysis-services/data-mining/deploy-a-data-mining-solution-to-previous-versions-of-sql-server.md)  
  
 [Exportar e importar objetos de mineração de dados](../../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
##  <a name="bkmk_Reqs"></a> Requisitos para a implantação de soluções de mineração de dados  
 A instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o qual você implanta a solução deve estar sendo executada em um modo que dá suporte a objetos multidimensionais e objetos de mineração de dados; ou seja, você não pode implantar objetos de mineração de dados em uma instância que hospeda modelos de tabela ou dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Portanto, quando você cria uma solução de mineração de dados no Visual Studio, use o modelo **Projeto Multidimensional e de Mineração de Dados do Analysis Services**.  
  
 Quando você implanta a solução, os objetos usados para mineração de dados são criados na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada, em um banco de dados com o mesmo nome do arquivo de solução.  
  
###  <a name="bkmk_RelationalSltn"></a> Implantando uma solução relacional  
 Quando você implanta uma solução de mineração de dados relacional, os objetos de mineração de dados exigidos são criados dentro de um novo banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os objetos são processados por padrão. Você pode alterar as opções de processamento usando a propriedade de configuração, **Opção de Processamento**. Para obter mais informações, consulte [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
 Por padrão, somente as alterações incrementais são implantadas de cada vez. Em outras palavras, você pode modificar um modelo de mineração e, quando reimplantar o projeto, somente o modelo de mineração será atualizado. Porém, se você tiver vários clientes que editam o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , isto poderá levar a erros. Para alterar o modo de implantação padrão para que o banco de dados inteiro seja atualizado quando você implantar a solução, altere a propriedade **Modo de Implantação**  
  
 Em uma solução de mineração de dados relacional, os únicos objetos que devem ser implantados são a definição de fonte de dados, as exibições da fonte de dados que foram usadas, as estruturas de mineração e todos os modelos de mineração dependentes.  
  
###  <a name="bkmk_MDSltn"></a> Implantando uma solução multidimensional  
 Quando você implanta uma solução de mineração de dados multidimensional, esta solução cria seus objetos de mineração de dados dentro do mesmo banco de dados do cubo de origem.  
  
 Quando você processa a estrutura de mineração ou o modelo de mineração, você também deve processar o cubo de origem. Por isto, implantar uma solução que usa modelos de mineração OLAP pode levar mais tempo que as soluções de mineração de dados relacionais.  
  
 Normalmente os objetos de mineração de dados também usam as mesmas fontes de dados e exibições da fonte de dados que são usadas para o cubo. No entanto, você pode adicionar fontes de dados e exibições da fonte de dados que são destinadas especificamente para mineração de dados. Por exemplo, normalmente um cubo não conteria dados sobre clientes em potencial ou dados externos que não são usados nos objetos multidimensionais.  
  
##  <a name="bkmk_Resources"></a> Recursos relacionados  
 [Movendo objetos de mineração de dados](../../analysis-services/data-mining/moving-data-mining-objects.md)  
  
 Se seu modelo for baseado somente em dados relacionais, exportar e importar objetos usando DMX é o modo mais fácil de mover modelos.  
  
 [Mover um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 Quando os modela usam um cubo como uma fonte de dados, consulte este tópico para obter mais informações sobre como mover modelos e os dados de cubo de suporte.  
  
 [Implantar projetos do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
 Fornece informações gerais sobre a implantação de projetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e descreve as propriedades que você pode definir como parte da configuração de projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Ferramentas de Consulta de Mineração de Dados](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [Requisitos e considerações de processamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
