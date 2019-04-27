---
title: Locais de processamento e armazenamento (Assistente para partições) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifyprocessingandstorage.f1
ms.assetid: dda2dc57-923d-4db9-93a7-38e95770f3df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a1462a2cc1338e973df3d0fd84641aa24d0bc41
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748578"
---
# <a name="processing-and-storage-locations-partition-wizard"></a>Locais de Processamento e Armazenamento (Assistente para Partições)
  Use a página **Locais de Processamento e Armazenamento** para especificar a instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo que contém a partição, bem como a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que armazena os dados da partição. É possível definir uma partição como uma partição remota especificando uma instância remota do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou um local de armazenamento diferente do local de armazenamento padrão. Para obter mais informações sobre partições remotas, consulte [Partições remotas](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).  
  
## <a name="processing-location-options"></a>Processando Opções de local  
 **Instância do servidor atual**  
 Torna a instância atual do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] responsável por processar a partição.  
  
 **Fonte de dados remota do Analysis Services**  
 Torna a instância remota do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] responsável por processar esta partição.  
  
 Na lista suspensa, selecione a fonte de dados que representa a instância remota do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que será responsável por processar a partição.  
  
> [!NOTE]  
>  Ocorrerá um erro se você selecionar uma fonte de dados na qual a propriedade `Initial Catalog` da cadeia de conexão não está definida como um banco de dados correto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou se o banco de dados especificado na propriedade `Initial Catalog` da cadeia de conexão não oferecer suporte a partições remotas (ou seja, a propriedade `MasterDatasourceID` do banco de dados especificado não está definida como um valor válido).  
  
 **Nova**  
 Cria uma nova fonte de dados que representa a instância remota do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] responsável por processar a partição.  
  
## <a name="storage-location-options"></a>Opções do local de armazenamento  
 **Local padrão do servidor**  
 Torna a pasta de dados da instância atual do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o local de armazenamento dos dados de agregação e de indexação da partição.  
  
 **Pasta especificada**  
 Especifica o local de armazenamento dos dados de agregação e indexação da partição.  
  
 **...**  
 Exibe a caixa de diálogo **Procurar Pasta Remota** na qual é possível selecionar uma pasta para a opção **Pasta especificada**.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de partição &#40;Analysis Services - dados multidimensionais&#41;](partition-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Procurar pasta remota caixa de diálogo &#40;Analysis Services - dados multidimensionais&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)  
  
  
