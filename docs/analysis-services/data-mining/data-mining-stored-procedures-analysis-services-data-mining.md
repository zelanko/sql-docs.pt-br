---
title: "Procedimentos armazenados da minera&#231;&#227;o de dados (Analysis Services - Minera&#231;&#227;o de Dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "procedimentos armazenados [Analysis Services], mineração de dados"
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# Procedimentos armazenados da minera&#231;&#227;o de dados (Analysis Services - Minera&#231;&#227;o de Dados)
  Começando no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte a procedimentos armazenados que podem ser escritos em qualquer linguagem gerenciada. As linguagens gerenciadas com suporte incluem [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET, C# e C++ gerenciado. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você pode chamar os procedimentos armazenados diretamente usando a instrução **CALL** ou como parte de uma consulta DMX (extensões DMX).  
  
 Para obter mais informações sobre como chamar os procedimentos armazenados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Chamando procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md).  
  
 Para obter informações gerais sobre a capacidade de programação do [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)], consulte [Programação de mineração de dados](../../analysis-services/data-mining-programming.md).  
  
 Para obter informações adicionais sobre como programar objetos de mineração de dados, consulte o artigo, "[SQL Server Data Mining Programmability](http://go.microsoft.com/fwlink/?LinkId=93735)" (Programabilidade de Mineração de Dados do SQL Server) na biblioteca de MSDN.  
  
> [!NOTE]  
>  Quando você consulta modelos de mineração, especialmente quando testa novas soluções de mineração de dados, pode ser conveniente chamar os procedimentos armazenados do sistema usados internamente pelo mecanismo de mineração de dados. É possível exibir os nomes desses procedimentos armazenados do sistema usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para criar um rastreamento no servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e criar, procurar e consultar os modelos de mineração de dados. No entanto, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] não garante a compatibilidade dos procedimentos armazenados do sistema entre versões e você nunca deve usar chamadas para os procedimentos armazenados do sistema em um sistema em produção. Em vez disso, para compatibilidade, crie suas próprias consultas usando DMX ou XML/A.  
  
## Nesta seção  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## Referência  
 [Script de tarefas administrativas no Analysis Services](../../analysis-services/instances/script-administrative-tasks-in-analysis-services.md)  
  
## Consulte também  
 [Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [Guia Validação Cruzada &#40;Exibição do gráfico de precisão de mineração&#41;](../Topic/Cross-Validation%20Tab%20\(Mining%20Accuracy%20Chart%20View\).md)   
 [Chamando um procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  