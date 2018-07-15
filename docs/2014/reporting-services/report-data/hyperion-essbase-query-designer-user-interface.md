---
title: Interface do usuário do Designer de Consultas do Hyperion Essbase | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10013"
- sql12.rtp.rptdesigner.dataview.hyperionessbasequerydesigner.f1
helpviewer_keywords:
- Hyperion Essbase Query Designer
- data sources [Reporting Services], Hyperion Essbase
- multidimensional data [Reporting Services]
- query designers [Reporting Services]
- Hyperion Essbase [Reporting Services], query designer
ms.assetid: bc91b422-c6ab-4062-a300-8290fae6191b
caps.latest.revision: 21
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7c93db9a11c9e3aa33a3e5119aee548f58cc7edb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330986"
---
# <a name="hyperion-essbase-query-designer-user-interface"></a>Interface de usuário do Designer de Consulta do Hyperion Essbase
  
            [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oferece um designer de consultas gráficas para criar consultas MDX (Multidimensional Expression) para uma fonte de dados do [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] . O designer de consultas gráficas MDX tem dois modos: Design e Consulta. Cada modo contém um painel Metadados, do qual é possível arrastar membros de um cubo definido na fonte de dados para criar uma consulta MDX que recupere dados quando o relatório for processado.  
  
> [!IMPORTANT]  
>  Os usuários acessam fontes de dados quando criam e executam consultas. Você deve conceder permissões mínimas nas fontes de dados, como permissões somente leitura.  
  
 Para obter mais informações sobre como trabalhar com uma fonte de dados multidimensionais do [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)], consulte [Tipo de conexão do Hyperion Essbase &#40;SSRS&#41;](hyperion-essbase-connection-type-ssrs.md).  
  
 Esta seção descreve os botões da barra de ferramentas e os painéis do designer de consulta para cada modo do designer de consultas gráficas.  
  
## <a name="graphical-query-designer-in-design-mode"></a>Designer de Consultas Gráficas no modo Design  
 Quando você edita uma consulta MDX para um conjunto de dados que usa um [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] fonte de dados, o designer de consultas gráficas é aberto no modo de Design.  
  
 A figura a seguir mostra os painéis do modo Design.  
  
 ![Designer de Consultas para a fonte de dados do Hyperion Essbase](../media/rsqd-dshyperionessbase-mdx-designmode.gif "Designer de Consultas para a fonte de dados do Hyperion Essbase")  
  
 A tabela a seguir lista os painéis neste modo.  
  
|Painel|Função|  
|----------|--------------|  
|Botão Selecionar Cubo|Exibe o cubo selecionado no momento.|  
|Painel Metadados|Exibe uma lista hierárquica de cubos.|  
|Painel Membros Calculados|Exibe os membros calculados definidos no momento disponíveis para serem usados na consulta.|  
|Painel Filtro|Exibe os filtros a serem aplicados na consulta.|  
|Painel Dados|Exibe os resultados da execução da consulta.|  
  
 Você pode arrastar dimensões e medidas do painel Metadados e membros calculados do painel Membro Calculado para o painel Dados. Se o botão de alternância **Executar Automaticamente** na barra de ferramentas estiver ativo, o designer de consulta executará a consulta toda vez que você soltar um objeto no painel Dados. Se **Executar Automaticamente** estiver desativado, o designer de consulta não executará a consulta quando forem feitas alterações no painel Dados. Você pode executar manualmente a consulta usando o botão **Executar** na barra de ferramentas.  
  
 No painel Filtro, você pode selecionar os valores de dimensão para limitar os dados recuperados da fonte de dados. Os valores definidos no filtro no modo Design são exibidos na cláusula Where do MDX no modo Consulta.  
  
### <a name="toolbar-for-the-graphical-query-designer-in-design-mode-toolbar"></a>Barra de ferramentas do Designer de Consultas Gráficas na barra de ferramentas do modo Design  
 A barra de ferramentas do designer de consulta fornece botões para ajudá-lo a criar consultas MDX por meio da interface gráfica. A tabela a seguir mostra os botões e descreve suas funções.  
  
|Botão|Description|  
|------------|-----------------|  
|**Editar como Texto**|Alterna entre o designer de consulta baseado em texto e o designer de consultas gráficas. Não disponível para esse tipo de fonte de dados.|  
|**Importar**|Importa uma consulta existente de um arquivo de definição de relatório (.rdl) no sistema de arquivos. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Atualizar campos de conjunto de dados](../media/rsqdicon-refreshfields.gif "Atualizar campos de conjunto de dados")|Atualiza metadados na fonte de dados.|  
|![Adicionar membro calculado](../../analysis-services/media/rsqdicon-addcalculatedmember.gif "Adicionar membro calculado")|Exibe a caixa de diálogo **Construtor de Membro Calculado** . Use essa opção para criar ou editar expressões de um membro calculado, incluindo a definição da propriedade **Ordem de Resolução** .|  
|![Alternar para mostrar células vazias](../../analysis-services/media/rsqdicon-showemptycells.gif "Alternar para mostrar células vazias")|Alterna entre mostrar ou não células vazias no painel Dados. (Equivale a usar a cláusula NON EMPTY em MDX).|  
|![Executar a consulta automaticamente](../../analysis-services/media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente")|Executa automaticamente a consulta e mostra o resultado toda vez que é feita uma alteração, por exemplo, excluindo uma coluna no painel Dados. Os resultados são mostrados no painel Dados.|  
|![Exclua](../../analysis-services/media/rsqdicon-delete.gif "excluir")|Exclui o item selecionado da consulta. Use esse botão para excluir as linhas selecionadas no painel Filtro.|  
|![Executar a consulta](../../analysis-services/media/rsqdicon-run.gif "Executar a consulta")|Executa a consulta e exibe os resultados no painel Dados.|  
|![Cancelar a consulta](../../analysis-services/media/rsqdicon-cancel.gif "Cancelar a consulta")|Cancela a consulta.|  
|![Alternar para o modo de Design](../../analysis-services/media/rsqdicon-designmode.gif "Alternar para o modo de Design")|Alterna entre o modo Design e o modo Consulta.|  
  
## <a name="graphical-query-designer-in-query-mode"></a>Designer de consultas gráficas no modo Consulta  
 Para alterar o designer de consultas gráficas para o modo Consulta, clique no botão de alternância **Modo Design** na barra de ferramentas. A figura a seguir indica as partes do designer de consulta no modo Consulta.  
  
 ![Designer de Consultas no modo de consulta do Hyperion](../media/rsqd-hyperionessbase-mdx-querymode.gif "Designer de Consultas no modo de consulta do Hyperion")  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Botão Selecionar Cubo|Exibe o cubo selecionado no momento.|  
|Painel Metadados/Funções|Exibe uma janela com guias que mostra uma lista de metadados ou funções disponíveis que pode ser usada para criar o texto de consulta.|  
|Painel Consulta|Exibe o texto da consulta atual.|  
|Painel Resultado|Exibe os resultados da consulta.|  
  
 No painel Metadados, você pode arrastar as medidas e dimensões da guia **Metadados** para o painel Consulta MDX. Você pode arrastar as funções da guia **Funções** para o painel Consulta MDX. Quando você executar a consulta, o painel Resultado exibirá os resultados da consulta MDX atual.  
  
### <a name="toolbar-for-the-graphical-query-designer-in-query-mode"></a>Barra de ferramentas do Designer de Consultas Gráficas no modo Consulta  
 A barra de ferramentas do designer de consulta fornece botões para ajudá-lo a criar consultas MDX por meio da interface gráfica. Os botões da barra de ferramentas são idênticos nos modos Design e Consulta, mas os botões a seguir não estão ativados no modo Consulta:  
  
-   **Editar como Texto**  
  
-   **Adicionar membro calculado** (![Adicionar membro calculado](../../analysis-services/media/rsqdicon-addcalculatedmember.gif "Adicionar membro calculado"))  
  
-   **Mostrar Células Vazias** (![Alternar para mostrar células vazias](../../analysis-services/media/rsqdicon-showemptycells.gif "Alternar para mostrar células vazias"))  
  
-   **Executar automaticamente** (![Executar a consulta automaticamente](../../analysis-services/media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente"))  
  
## <a name="see-also"></a>Consulte também  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Arquivo de configuração RSReportDesigner](../report-server/rsreportdesigner-configuration-file.md)  
  
  
