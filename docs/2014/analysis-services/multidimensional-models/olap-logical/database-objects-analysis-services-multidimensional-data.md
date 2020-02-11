---
title: Objetos Database (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], about objects
- SQL Server Analysis Services, objects
- Analysis Services objects, about Analysis Services objects
- SSAS, objects
- Analysis Services objects
- objects [Analysis Services]
ms.assetid: f76d869b-fc1d-4807-9f28-da09c7be382d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 39116b4bf8c4c361dfa82ca0d8a38dc6977de217
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62725651"
---
# <a name="database-objects-analysis-services---multidimensional-data"></a>Objetos de banco de dados (Analysis Services – Dados Multidimensionais)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Uma [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância contém objetos de banco de dados e assemblies para uso com OLAP (processamento analítico online) e Data Mining.  
  
-   Os bancos de dados contêm objetos OLAP e dados de mineração, como fontes de dados, exibições de fonte de dados, cubos, medidas, grupos de medidas, dimensões, atributos, hierarquias, estruturas de mineração de dados, modelos de mineração de dados e funções.  
  
-   Os assemblies contêm funções definidas pelo usuário que ampliam a funcionalidade de funções intrínsecas, fornecidas com as linguagens MDX e extensões de mineração de dados (DMX).  
  
 O objeto <xref:Microsoft.AnalysisServices.Database> é o contêiner de todos os objetos de dados necessários para um projeto de business intelligence (como cubos OLAP, dimensões e estruturas de mineração de dados) e seus objetos de suporte (como <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Account> e <xref:Microsoft.AnalysisServices.Role>).  
  
 Um objeto <xref:Microsoft.AnalysisServices.Database> fornece acesso a objetos e atributos incluindo o seguinte:  
  
-   Todos os cubos que você pode acessar, como uma coleção.  
  
-   Todas as dimensões que você pode acessar, como uma coleção.  
  
-   Todas as estruturas de mineração que você pode acessar, como uma coleção.  
  
-   Todas as fontes de dados e exibições de fonte de dados, como duas coleções.  
  
-   Todas as funções e permissões de banco de dados, como duas coleções.  
  
-   O valor da ordenação para o banco de dados.  
  
-   O tamanho estimado do banco de dados.  
  
-   O valor do idioma do banco de dados.  
  
-   A configuração visível do banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos seguintes descrevem objetos compartilhados por recursos OLAP e mineração de dados no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Fontes de dados em modelos multidimensionais](../data-sources-in-multidimensional-models.md)|Descreve uma fonte de dados no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Exibições de fontes de dados em modelos multidimensionais](../data-source-views-in-multidimensional-models.md)|Descreve um modelo de dados lógico baseado em uma ou mais fontes de dados, no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Cubos em modelos multidimensionais](../cubes-in-multidimensional-models.md)|Descreve cubos e objetos de cubo, incluindo medidas, grupos de medidas, relações de uso de dimensão, cálculos indicadores de desempenho principais, ações, traduções, partições e perspectivas.|  
|[Dimensões &#40;Analysis Services de dados multidimensionais&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|Descreve dimensões e objetos de dimensão, inclusive atributos, relações de atributo, hierarquias, níveis e membros.|  
|[Estruturas de mineração &#40;Analysis Services de mineração de dados&#41;](../../data-mining/mining-structures-analysis-services-data-mining.md)|Descreve estruturas e objetos de mineração de dados, inclusive modelos de mineração de dados.|  
|[Funções de segurança &#40;Analysis Services de dados multidimensionais&#41;](security-roles-analysis-services-multidimensional-data.md)|Descreve uma função, o mecanismo de segurança usado para controlar o acesso a objetos no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Gerenciamento de assemblies de modelo multidimensional](../multidimensional-model-assemblies-management.md)|Descreve um assembly, uma coleção de funções definidas pelo usuário e usada para ampliar as linguagens MDX e DMX, no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Fontes de dados com suporte &#40;SSAS multidimensional&#41;](../supported-data-sources-ssas-multidimensional.md)   
 [Soluções de modelo multidimensional &#40;SSAS&#41;](../multidimensional-model-solutions-ssas.md)   
 [Soluções de mineração de dados](../../data-mining/data-mining-solutions.md)  
  
  
