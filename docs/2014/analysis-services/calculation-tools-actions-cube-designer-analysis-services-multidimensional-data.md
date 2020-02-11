---
title: Ferramentas de cálculo (guia ações, designer de cubo) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionsview.calculationtoolspane.f1
ms.assetid: a3370370-43cd-4cc2-bb9f-c0d988b96f05
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 087f5f5e3383fd66244541fea35160946936bc1c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088342"
---
# <a name="calculation-tools-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Ferramentas de Cálculo (guia Ações, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Ferramentas de Cálculo** da guia **Ações** no Designer de Cubo para explorar metadados, funções e modelos disponíveis para uso em ações, ações de extração de detalhes e ações de relatório.  
  
## <a name="options"></a>Opções  
 **Metadados**  
 Exibe os metadados do cubo selecionado.  
  
 Arraste um elemento selecionado para o painel **Action Form Editor (Editor de Formulário de Ação)**, **Drillthrough Action Form Editor (Editor de Formulário de Ação de Extração de Detalhes)** ou **Report Action Form Editor (Editor de Formulário de Ação de Relatório)** para incluir a sintaxe MDX (Multidimensional Expressions) daquele elemento no local selecionado no painel.  
  
 **Funções**  
 Exibe as funções disponíveis para expressões e condições.  
  
 Arraste um elemento selecionado para o painel **Editor de Formulário de Ação**, **Editor de Formulário de Ação de Extração de Detalhes**ou **Editor de Formulário de Ação de Relatório** para incluir a sintaxe MDX daquele elemento no local selecionado no painel.  
  
> [!NOTE]  
>  No modo de projeto, a caixa de diálogo **Ferramentas de Cálculo** lê as informações desta opção em um arquivo XML denominado MDXFunctions.xml fornecido com o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Em modo online, informações para esta opção são recuperadas do conjunto de linhas de esquema de MDSCHEMA_FUNCTIONS da instância.  
  
 **Modelo**  
 Exibe os modelos predefinidos disponíveis para ações.  
  
 Arraste um elemento selecionado para o painel **Editor de Formulário de Ação**, **Editor de Formulário de Ação de Extração de Detalhes**ou **Editor de Formulário de Ação de Relatório** para incluir a sintaxe MDX daquele elemento no local selecionado no painel.  
  
## <a name="context-menu"></a>Menu de contexto  
 As seguintes opções estão disponíveis no menu de contexto exibido ao clicar com o botão direito do mouse em um elemento exibido no painel **Ferramentas de Cálculo** :  
  
|Opção|Definição|  
|------------|----------------|  
|**Copy**|Selecione para copiar o elemento selecionado em **Metadados** ou **Funções** na Área de Transferência.<br /><br /> Observe que essa opção não será exibida se **modelos** estiver selecionado. Observe também que essa opção estará desabilitada se o membro selecionado não puder ser copiado, como a pasta **sets** de uma dimensão exibida em **metadados** ou a pasta do grupo de funções para uma função exibida em **funções**.|  
|**Filtrar Membros**|Clique para exibir a caixa de diálogo **Filtrar Membros** e filtrar os membros exibidos para o elemento selecionado em **Metadados**. Para obter mais informações sobre a caixa de diálogo **Filtrar Membros**, consulte [Caixa de diálogo Filtrar Membros &#40;Analysis Services – Dados Multidimensionais&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Observe que essa opção será exibida somente se os **metadados** estiverem selecionados. Observe também que essa opção será habilitada somente se um nível para um atributo for selecionado em **metadados**.|  
|**Adicionar Modelo**|Selecione para adicionar uma nova ação, ação de extração de detalhes ou ação de relatório com base no modelo selecionado ao cubo e exibir, respectivamente, o **Editor de Formulário de Ação**, **Editor de Formulário de Ação de Extração de Detalhes**ou **Editor de Formulário de Ação de Relatório**.<br /><br /> Observação: essa opção será exibida somente se os **metadados** estiverem selecionados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos de script MDX &#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Ações &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia ações, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Guia ações do organizador de ação &#40;, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação &#40;guia ações, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de detalhamento &#40;guia ações, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de relatório &#40;guia ações, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
