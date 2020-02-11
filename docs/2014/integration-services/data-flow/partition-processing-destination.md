---
title: Destino de processamento de partições | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partitionprocessingdest.f1
helpviewer_keywords:
- partitions [Analysis Services], processing
- Partition Processing destination [Integration Services]
- destinations [Integration Services], Partition Processing
ms.assetid: 36c592ff-3f78-4a58-b496-31c1c8eee131
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 53ef09d19b62c0e6ce7742c41581d3cdefdfc374
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68890556"
---
# <a name="partition-processing-destination"></a>Destino de processamento de partições
  O destino de processamento de partições carrega e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processa uma partição. Para obter mais informações sobre partições, consulte [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data).  
  
 O destino de Processamento de Partições inclui os seguintes recursos :  
  
-   Opções para executar o processamento incremental, completo ou atualizado.  
  
-   Configuração de erro, para especificar se o processamento ignora erros ou é interrompido depois de um número especificado de erros.  
  
-   Mapeamento das colunas de entrada em colunas de partição.  
  
 Para obter mais informações sobre processamento de objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services).  
  
> [!NOTE]  
>  As tarefas descritas aqui não se aplicam a modelos de tabela do Analysis Services.  Você não pode mapear colunas de entrada para as colunas de partição em modelos de tabela. Você pode usar a tarefa Executar DDL do Analysis Services [Analysis Services Execute DDL Task](../control-flow/analysis-services-execute-ddl-task.md) para processar a partição.  
  
## <a name="configuration-of-the-partition-processing-destination"></a>Configuração do destino do processamento da partição  
 O destino de Processamento de Partições usa um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para se conectar ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém os cubos e as partições que o destino processa. Para obter mais informações, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md).  
  
 Esse destino tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Destino** de Processamento de Partições, clique em um dos seguintes tópicos:  
  
-   [Editor de destino de processamento de partições &#40;página Gerenciador de conexões&#41;](../partition-processing-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de processamento de partições &#40;página Mapeamentos&#41;](../partition-processing-destination-editor-mappings-page.md)  
  
-   [Editor de destino de processamento de partições &#40;página avançado&#41;](../partition-processing-destination-editor-advanced-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas do destino Processamento de Partições](partition-processing-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
  
