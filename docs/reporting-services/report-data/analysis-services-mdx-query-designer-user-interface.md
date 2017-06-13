---
title: "Interface de usuário do Designer de consulta MDX do Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.asquerydesigner.f1
helpviewer_keywords:
- MDX [Reporting Services], creating datasets
- query designers [Reporting Services]
ms.assetid: d9c7c0b3-fce4-4a65-b679-408273e6a925
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7f8838c9793cfc4a8e38bea3f0f27e702dd27e4d
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="analysis-services-mdx-query-designer-user-interface"></a>Interface do usuário do Designer de Consulta MDX do Analysis Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece designers de consultas gráficas para criar consultas MDX (Multidimensional Expression) e consultas DMX (extensões DMX) para uma fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Este tópico descreve o designer de consulta MDX. Para obter mais informações sobre o designer de consultas DMX, consulte [Tipo de conexão Analysis Services para DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md).  
  
 O designer de consultas gráficas MDX tem dois modos: Design e Consulta. Cada modo contém um painel Metadados, do qual é possível arrastar membros dos cubos selecionados para criar uma consulta MDX que recupere dados quando o relatório for processado.  
  
> [!IMPORTANT]  
>  Os usuários acessam fontes de dados quando criam e executam consultas. Você deve conceder permissões mínimas nas fontes de dados, como permissões somente leitura.  
  
> [!NOTE]  
>  Não há suporte para a importação de uma consulta .mdx a partir de um arquivo.  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>Designer de consultas gráficas MDX no modo Design  
 Quando você edita uma consulta MDX para um conjunto de dados de relatórios, o designer de consultas gráficas MDX é aberto no modo Design.  
  
 A figura a seguir mostra os painéis do modo Design.  
  
 ![Designer de consulta do Analysis Services MDX, o modo de exibição de design](../../reporting-services/report-data/media/rsqd-dsawas-mdx-designmode.gif "designer de consulta MDX do Analysis Services, modo de design")  
  
 A tabela a seguir lista os painéis neste modo:  
  
|Painel|Função|  
|----------|--------------|  
|Botão Selecionar Cubo (**...**)|Exibe o cubo selecionado no momento.|  
|Painel Metadados|Exibe uma lista hierárquica de medidas, KPIs (Indicadores Chave de Desempenho) e dimensões definidas no cubo selecionado.|  
|Painel Membros Calculados|Exibe os membros calculados definidos no momento disponíveis para serem usados na consulta.|  
|Painel Filtro|Use para escolher dimensões e hierarquias relacionadas para filtrar dados na origem e limitar os dados retornados ao relatório.|  
|Painel Dados|Exibe os cabeçalhos de coluna do conjunto de resultados à medida que você arrasta os itens do painel Metadados e do painel Membros Calculados. Atualiza automaticamente o conjunto de resultados se o botão **Executar Automaticamente** for selecionado. .|  
  
 Você pode arrastar dimensões, medidas e KPIs do painel Metadados e membros calculados do painel Membro Calculado para o painel Dados. No painel Filtro, é possível selecionar dimensões e hierarquias relacionadas e definir expressões de filtro para limitar os dados disponíveis para consulta. Se o **AutoExecutar** (![executar a consulta automaticamente](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "executar a consulta automaticamente")) botão de alternância na barra de ferramentas estiver selecionada, o designer de consulta executa a consulta toda vez que você solta um objeto de metadados no painel de dados. Você pode executar manualmente a consulta usando o **executar** (![executar a consulta](../../reporting-services/report-data/media/rsqdicon-run.gif "executar a consulta")) na barra de ferramentas.  
  
 Quando você cria uma consulta MDX nesse modo, as seguintes propriedades adicionais são incluídas automaticamente na consulta:  
  
 **Propriedades do Membro** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **Propriedades da Célula** VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
  
 Para especificar suas próprias propriedades adicionais, você deve editar manualmente a consulta MDX no modo Consulta.  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Barra de ferramentas do Designer de Consultas Gráficas MDX no modo Design  
 A barra de ferramentas do designer de consulta fornece botões para ajudá-lo a criar consultas MDX por meio da interface gráfica. A tabela a seguir lista os botões e as suas funções.  
  
|Botão|Description|  
|------------|-----------------|  
|**Editar como Texto**|Não habilitado para esse tipo de fonte de dados.|  
|**Importar**|Importa uma consulta existente de um arquivo de definição de relatório (.rdl) no sistema de arquivos. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Alterar para a exibição de consulta MDX](../../reporting-services/report-data/media/rsqdicon-commandtypemdx.gif "alterar para a exibição de consulta MDX")|Alternar para Tipo de Comando MDX.|  
|![Alterar a exibição de linguagem de consulta DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "alterar para a exibição de linguagem de consulta DMX")|Alternar para Tipo de Comando DMX.|  
|![Atualizar dados de resultado](../../reporting-services/report-data/media/rsqdicon-refresh.gif "atualizar dados de resultado")|Atualiza metadados na fonte de dados.|  
|![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member")|Exibe a caixa de diálogo **Construtor de Membro Calculado** .|  
|![Alternar para mostrar células vazias](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "alternância para mostrar células vazias")|Alterna entre mostrar ou ocultar células vazias no painel Dados. (Equivale a usar a cláusula NON EMPTY em MDX).|  
|![Executar a consulta automaticamente](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "executar a consulta automaticamente")|Executa automaticamente a consulta e mostra o resultado sempre que é feita uma alteração. Os resultados são mostrados no painel Dados.|  
|![Botão Mostrar agregações](../../reporting-services/report-data/media/rsqdicon-showaggregations.gif "botão Mostrar agregações")|Mostra agregações no painel Dados.|  
|![Excluir](../../reporting-services/report-data/media/rsqdicon-delete.gif "Excluir")|Exclui da consulta a coluna selecionada no painel Dados.|  
|![Ícone da caixa de diálogo parâmetros de consulta](../../reporting-services/report-data/media/iconqueryparameter.gif "ícone da caixa de diálogo parâmetros de consulta")|Exiba a caixa de diálogo **Parâmetros de Consulta** . Quando você especifica os valores para um parâmetro de consulta, um parâmetro de relatório com o mesmo nome é automaticamente criado. O valor do parâmetro da consulta é definido como uma expressão que faz referência ao parâmetro do relatório.|  
|![Botão de consulta de preparação](../../reporting-services/report-data/media/rsqdicon-preparequery.gif "botão preparar consulta")|Prepara a consulta.|  
|![Execute a consulta](../../reporting-services/report-data/media/rsqdicon-run.gif "executar a consulta")|Executa a consulta e exibe os resultados no painel Dados.|  
|![Cancelar a consulta](../../reporting-services/report-data/media/rsqdicon-cancel.gif "cancelar a consulta")|Cancela a consulta.|  
|![Alternar para o modo de Design](../../reporting-services/media/rsqdicon-designmode.gif "alternar para modo de Design")|Alterna entre o modo Design e o modo Consulta.|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>Designer de Consultas Gráficas MDX no modo Consulta  
 Para alterar o designer de consultas gráficas para o modo **Consulta** , clique no botão de alternância **Modo Design** na barra de ferramentas.  
  
 A figura a seguir mostra os painéis do modo Consulta.  
  
 ![Analysis Services MDX query designer, exibição de consulta](../../reporting-services/report-data/media/rsqd-dsawas-mdx-querymode.gif "exibição consulta designer de consulta MDX do Analysis Services")  
  
 A tabela a seguir lista os painéis neste modo:  
  
|Painel|Função|  
|----------|--------------|  
|Botão Selecionar Cubo (**...**)|Exibe o cubo selecionado no momento.|  
|Painel Metadados/Funções/Modelos|Exibe uma lista hierárquica de medidas, KPIs e dimensões definidas no cubo selecionado.|  
|Painel Consulta|Exibe o texto da consulta.|  
|Painel Resultado|Exibe os resultados da execução da consulta.|  
  
 O painel Metadados exibe as guias para **Metadados**, **Funções**e **Modelos**. Na guia **Metadados** , você pode arrastar as dimensões, hierarquias, KPIs e medidas no painel Consulta MDX. Na guia **Funções** , você pode arrastar as funções no painel Consulta MDX. Na guia **Modelos** , você pode adicionar modelos MDX ao painel Consulta MDX. Quando você executar a consulta, o painel Resultado exibirá os resultados da consulta MDX.  
  
 Você pode ampliar a consulta MDX padrão gerada no modo Design para incluir propriedades do membro adicionais e propriedades da célula. Ao executar a consulta, esses valores não são exibidos no conjunto de resultados. No entanto, eles são passados de volta para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e você pode usar esses valores em um relatório. Para obter mais informações, consulte [Propriedades de campos estendidos para um banco de dados do Analysis Services &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Barra de ferramentas do Designer de Consultas Gráficas no modo Consulta  
 A barra de ferramentas do designer de consulta fornece botões para ajudá-lo a criar consultas MDX por meio da interface gráfica.  
  
 Os botões da barra de ferramentas são idênticos nos modos Design e Consulta, mas os botões a seguir não estão ativados no modo Consulta:  
  
-   **Editar como Texto**  
  
-   **Adicionar Membro Calculado** (![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Mostrar células vazias** (![alternância para mostrar células vazias](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "alternância para mostrar células vazias"))  
  
-   **Executar automaticamente** (![executar a consulta automaticamente](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "executar a consulta automaticamente"))  
  
-   **Mostrar agregações** (![botão Mostrar agregações](../../reporting-services/report-data/media/rsqdicon-showaggregations.gif "botão Mostrar agregações"))  
  
## <a name="see-also"></a>Consulte também  
 [Definir parâmetros no Designer de Consulta MDX do Analysis Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)   
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Tipo de conexão Analysis Services para DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [Arquivo de configuração RSReportDesigner](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Tipo de conexão Analysis Services para MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
  
