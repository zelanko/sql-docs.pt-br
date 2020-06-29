---
title: Destino de processamento de dimensões | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d2feaf838706b6862eb480dba7d5a6438ae76247
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437843"
---
# <a name="dimension-processing-destination"></a>Destino de processamento de dimensões
  O destino de Processamento de Dimensões carrega e processa uma dimensão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações sobre dimensões, consulte [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data).  
  
 O Destino de Processamento de Dimensões inclui os seguintes recursos:  
  
-   Opções para executar o processamento incremental, completo ou atualizado.  
  
-   Configuração de erro, para especificar se o processamento de dimensões ignora erros ou é interrompido depois de um determinado número de erros.  
  
-   Mapeamento de colunas de entrada para colunas nas tabelas de dimensão.  
  
 Para obter mais informações sobre processamento de objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services).  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>Configuração do o destino Processamento de Dimensão  
 O Destino de Processamento de Dimensões usa um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém as dimensões processadas pelo destino. Para obter mais informações, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md).  
  
 Esse destino tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Destino de Processamento de Dimensões** , clique em um dos seguintes tópicos:  
  
-   [Editor de Destino de Processamento de Dimensões &#40;Página Gerenciador de Conexões&#41;](../dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [Editor de Destino de Processamento de Dimensões &#40;página Mapeamentos&#41;](../dimension-processing-destination-editor-mappings-page.md)  
  
-   [Editor de Destino de Processamento de Dimensões &#40;Página Avançado&#41;](../dimension-processing-destination-editor-advanced-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de dados](data-flow.md)   
 [Transformações do Integration Services](transformations/integration-services-transformations.md)  
  
  
