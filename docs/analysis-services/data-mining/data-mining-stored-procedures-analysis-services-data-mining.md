---
title: "Procedimentos armazenados da mineração de dados (Analysis Services – mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 67e09ad757b0433a4db09187492cdbe58dbe94ff
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-stored-procedures-analysis-services---data-mining"></a>Procedimentos armazenados da mineração de dados (Analysis Services - Mineração de Dados)
  Começando no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte a procedimentos armazenados que podem ser escritos em qualquer linguagem gerenciada. As linguagens gerenciadas com suporte incluem [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET, C# e C++ gerenciado. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você pode chamar os procedimentos armazenados diretamente usando a instrução **CALL** ou como parte de uma consulta DMX (extensões DMX).  
  
 Para obter mais informações sobre como chamar os procedimentos armazenados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , consulte [Chamando procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md).  
  
 Para obter informações gerais sobre programação, consulte [programação de mineração de dados](../../analysis-services/data-mining-programming.md).  
  
 Para obter informações adicionais sobre como programar objetos de mineração de dados, consulte o artigo, "[SQL Server Data Mining Programmability](http://go.microsoft.com/fwlink/?LinkId=93735)" (Programabilidade de Mineração de Dados do SQL Server) na biblioteca de MSDN.  
  
> [!NOTE]  
>  Quando você consulta modelos de mineração, especialmente quando testa novas soluções de mineração de dados, pode ser conveniente chamar os procedimentos armazenados do sistema usados internamente pelo mecanismo de mineração de dados. É possível exibir os nomes desses procedimentos armazenados do sistema usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para criar um rastreamento no servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e criar, procurar e consultar os modelos de mineração de dados. No entanto, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] não garante a compatibilidade dos procedimentos armazenados do sistema entre versões e você nunca deve usar chamadas para os procedimentos armazenados do sistema em um sistema em produção. Em vez disso, para compatibilidade, crie suas próprias consultas usando DMX ou XML/A.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## <a name="see-also"></a>Consulte também  
 [Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [Guia validação cruzada &#40; Exibição de gráfico de precisão mineração &#41;](http://msdn.microsoft.com/library/bd215a68-1ad7-4046-9c44-ec8e2be13a64)   
 [Chamar um procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  

