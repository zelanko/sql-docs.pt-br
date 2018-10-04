---
title: Destino de processamento de dimensões | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3cd8b33e330a2edd9d6c93cb9ab00c68783ae5bc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135416"
---
# <a name="dimension-processing-destination"></a>Destino de processamento de dimensões
  O Destino de Processamento de Dimensões carrega e processa uma dimensão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obter mais informações sobre dimensões, consulte [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 O Destino de Processamento de Dimensões inclui os seguintes recursos:  
  
-   Opções para executar o processamento incremental, completo ou atualizado.  
  
-   Configuração de erro, para especificar se o processamento de dimensões ignora erros ou é interrompido depois de um determinado número de erros.  
  
-   Mapeamento de colunas de entrada para colunas nas tabelas de dimensão.  
  
 Para obter mais informações sobre processamento de objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>Configuração do o destino Processamento de Dimensão  
 O Destino de Processamento de Dimensões usa um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém as dimensões processadas pelo destino. Para obter mais informações, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md).  
  
 Esse destino tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Destino de Processamento de Dimensões** , clique em um dos seguintes tópicos:  
  
-   [Editor de destino de processamento de dimensões &#40;página do Gerenciador de Conexão&#41;](../dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de processamento de dimensões &#40;página mapeamentos&#41;](../dimension-processing-destination-editor-mappings-page.md)  
  
-   [Editor de destino de processamento de dimensões &#40;página Avançado&#41;](../dimension-processing-destination-editor-advanced-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](data-flow.md)   
 [Transformações do Integration Services](transformations/integration-services-transformations.md)  
  
  
