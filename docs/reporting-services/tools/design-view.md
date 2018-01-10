---
title: "Modo de exibição de Design | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rtp.rptdesigner.layoutview.f1
helpviewer_keywords: Layout View dialog box
ms.assetid: 6fa378aa-442f-4d2f-beab-02a0fb5cd3ce
caps.latest.revision: "38"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 43b324699b0e462f452b106846fe86d5e5e0919a
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="design-view"></a>Modo Design
No Designer de Relatórios do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , use o modo de exibição de Design para organizar itens no relatório. O modo Design também é chamado de superfície de design ou modo de layout.  
  ![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png)
## <a name="report-design-surface"></a>Superfície de design do relatório  
A superfície de design consiste em três seções: 
+ corpo do relatório
+ cabeçalho da página
+ rodapé 

Use a Caixa de Ferramentas para selecionar itens a serem colocados nessas três seções. Use o painel de dados do relatório para exibir imagens, parâmetros, fontes de dados e conjuntos de dados, incluindo consultas a conjuntos de dados e listas de campo. Depois de adicionar itens de relatório à superfície de design, arraste campos do conjunto de dados do painel **Dados do Relatório** para regiões de dados, como uma tabela, matriz ou lista. Cada item na superfície de design do relatório contém propriedades que podem ser gerenciadas usando-se uma caixa de diálogo ou o painel Propriedades.  
  
## <a name="toolbox"></a>Caixa de Ferramentas  
 A Caixa de Ferramentas lista regiões de dados e outros itens que estão disponíveis para seu relatório. Para adicionar itens de relatório da Caixa de Ferramentas, clique duas vezes no item ou arraste-o para a superfície de design. Você poderá alterar a forma e o tamanho usando os identificadores de objetos.  
  
## <a name="report-data-pane"></a>painel Dados do Relatório  
 Para exibir o painel de dados do relatório, no menu **Exibir** , clique em **Dados do Relatório**. Use esse painel para definir parâmetros, imagens, fontes de dados e conjuntos de dados, bem como para referenciar campos internos, como ReportName. Para adicionar um novo item, clique no menu **Novo** e selecione um item. Para adicionar campos calculados a um conjunto de dados existente, clique em **Conjunto de Dados**e, na caixa de diálogo **Propriedades do Conjunto de Dados** , selecione **Campos**. Selecione um item e clique em **Editar** para abrir a caixa de diálogo **Propriedades** . Você também poderá clicar com o botão direito do mouse em itens do painel de dados do relatório para adicionar itens ou atualizar suas propriedades.  
  
 Arraste itens do painel de dados do relatório para regiões de dados e caixas de texto na superfície de design para adicionar dados e imagens a um relatório.  
  
 Para obter mais informações, consulte [Report Data Pane](../../reporting-services/report-data/report-data-pane.md).  
  
## <a name="grouping-pane"></a>Painel Agrupamento  
 Os grupos são usados para organizar seus dados de relatório em uma hierarquia visual e para calcular totais. Use o painel Agrupamento para exibir os grupos definidos para uma tabela, matriz ou região de dados de lista. Por padrão, o painel Agrupamento exibe todos os grupos para a região de dados selecionada como uma lista plana. O painel Agrupamento é desabilitado para regiões de dados Gráfico e Medidor.  
  
 Para consultar os grupos em relação um ao outro, alterne o painel Agrupamento para o modo Avançado. Esse modo exibe a hierarquia de membros do grupo, uma exibição visual de células da região de dados que correspondem a cada grupo.  
  
 Para obter mais informações, consulte [Grouping Pane](../../reporting-services/tools/grouping-pane.md).  
  
## <a name="page-header-and-page-footer"></a>Cabeçalho da Página e Rodapé da Página  
 Um cabeçalho e um rodapé se estendem na parte superior e inferior de cada página, respectivamente. Os cabeçalhos e rodapés podem conter texto estático, imagens, linhas, retângulos, bordas, cor e imagens de plano de fundo. Para adicionar itens de relatório ao cabeçalho ou rodapé, clique com o botão direito do mouse na superfície de design e selecione Cabeçalho ou Rodapé. As seções de cabeçalho e rodapé aparecem na superfície de design.  
  
## <a name="properties-pane"></a>Painel Propriedades  
 Use o painel Propriedades para exibir as propriedades do item de relatório selecionado na superfície de design ou do grupo selecionado no painel Agrupamento. Se preferir, clique com o botão direito do mouse em um item de relatório ou grupo selecionado e clique em **Propriedades** para abrir a caixa de diálogo **Propriedades** do item de relatório ou do grupo.  
  
## <a name="see-also"></a>Consulte Também  
 [Cabeçalhos e rodapés de página &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Dicas de design de relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-design-tips-report-builder-and-ssrs.md)  
  
  
