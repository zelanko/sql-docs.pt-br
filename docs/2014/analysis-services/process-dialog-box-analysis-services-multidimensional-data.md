---
title: Processar caixa de diálogo (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.processdialog.f1
ms.assetid: c065248c-9001-4f0c-928f-9c59eccb618b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32411ff5b715e15fd52b832d8047d8382a603924
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070752"
---
# <a name="process-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Processar (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Processar** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para processar objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . É possível exibir a caixa de diálogo **Processar** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] das seguintes maneiras:  
  
-   Clicando com o botão direito do mouse em um projeto, cubo, dimensão ou estrutura de mineração do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no **Gerenciador de Soluções** e selecionando **Processar**.  
  
-   Selecionando **Processar** na barra de ferramentas em cada página do **Designer de Cubo**, em cada página do **Designer de Dimensão**ou nas páginas **Estrutura de Mineração** e **Modelos de Mineração** do **Designer de Modelo de Mineração de Dados**.  
  
-   Clicando com o botão direito do mouse na página **Modelos de Mineração** do **Designer de Modelo de Data Mining** e selecionando **Estrutura de Mineração do Processo e Todos os Modelos** ou **Modelo de Processo**.  
  
 É possível exibir a caixa de diálogo **Processar** no **SQL Server Management Studio** das seguintes maneiras:  
  
-   Clicando com o botão direito do mouse em um banco de dados, cubo, grupo de medidas, partição, dimensões, estrutura de mineração ou modelo de mineração do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no **Explorador de Objetos** e selecionando **Processar**.  
  
## <a name="options"></a>Opções  
 **Lista de objetos**  
 Selecione os objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a serem processados e as opções e configurações de processamento a serem aplicadas. A grade contém as seguintes colunas:  
  
 **Object Name**  
 Exibe o nome do objeto a ser processado. O ícone à esquerda do nome indica o tipo do objeto.  
  
 **Tipo**  
 Exibe o tipo do objeto a ser processado.  
  
 **Opções de Processo**  
 Selecione o tipo de processamento a ser executado no objeto selecionado. Para obter mais informações sobre as opções de processamento disponíveis, consulte [processamento de objeto de modelo Multidimensional](multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 **Configurações**  
 Exibe o hiperlink **Configurar** quando você escolhe **Processar Incremental** em **Opções de Processo** para cubos, grupos de medidas ou partições. Clique em **Configurar** para iniciar a caixa de diálogo **Atualização Incremental** . Para obter mais informações sobre a caixa de diálogo **Atualização Incremental**, consulte [Caixa de diálogo Atualização Incremental &#40;Analysis Services – Dados Multidimensionais&#41;](incremental-update-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Remover**  
 Clique para remover os itens selecionados da **Lista de objetos**.  
  
 **Análise de Impacto**  
 Clique para abrir a caixa de diálogo **Análise de Impacto** e exibir os objetos que serão afetados pela tarefa de processamento. Para obter mais informações sobre a caixa de diálogo **Análise de Impacto**, consulte [Caixa de diálogo Análise de Impacto &#40;Analysis Services – Dados Multidimensionais&#41;](impact-analysis-dialog-box-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Esta opção é desabilitada quando a opção **Objetos afetados pelo processo** está selecionada na caixa de diálogo **Alterar Configurações** .  
  
 **Alterar Configurações**  
 Clique para abrir a caixa de diálogo **Alterar Configurações** e alterar as configurações que controlam o processamento dos objetos selecionados, incluindo configurações de processamento em lote, configurações de write-back e configurações de erro de chave de dimensão. Para obter mais informações sobre a caixa de diálogo **Alterar Configurações**, consulte [Caixa de diálogo Alterar Configurações &#40;Analysis Services – Dados Multidimensionais&#41;](change-settings-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Executar**  
 Clique para processar os objetos.  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Processar caixa de diálogo de progresso &#40;Analysis Services - dados multidimensionais&#41;](process-progress-dialog-box-analysis-services-multidimensional-data.md)  
  
  
