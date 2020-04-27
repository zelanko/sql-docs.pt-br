---
title: Designer de consulta MDX Analysis Services (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.asmdxquerydes.f1
ms.assetid: a2fb0b79-802a-4dac-bd9a-32dfe2e8c4d4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23bdc92e18a7f2cae351faddd69370c9e08a7371
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062513"
---
# <a name="analysis-services-mdx-query-designer-ssas"></a>Designer de consulta MDX do Analysis Services (SSAS)
  O designer de consulta MDX (multidimensional Expression) do Analysis Services fornece interfaces gráficas do usuário para ajudá-lo a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] criar consultas MDX para uma fonte de dados. O designer de consultas gráficas MDX tem dois modos: Design e Consulta. Cada modo contém um painel Metadados, do qual é possível arrastar membros dos cubos selecionados para criar uma consulta MDX que recupere os dados que você deseja usar.  
  
> [!IMPORTANT]  
>  Os usuários acessam fontes de dados quando criam e executam consultas. Você deve conceder permissões mínimas nas fontes de dados, como permissões somente leitura.  
>   
>  As credenciais do usuário atual, e não as credenciais especificadas na página Informações sobre Representação, são usadas na conexão à fonte de dados quando uma consulta é executada.  
  
 As seções a seguir descrevem os botões da barra de ferramentas e os painéis do designer de consulta para cada modo do designer de consultas gráficas.  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>Designer de consultas gráficas MDX no modo Design  
 Quando você edita uma consulta MDX, o designer de consultas gráficas MDX é aberto no modo Design.  
  
 A figura a seguir mostra os painéis do modo Design.  
  
 ![Designer de consultas MDX do Analysis Services, exibição de design](media/rsqd-dsawas-mdx-designmode.gif "Designer de consultas MDX do Analysis Services, exibição de design")  
  
 A tabela a seguir lista os painéis neste modo:  
  
|Painel|Função|  
|----------|--------------|  
|Botão Selecionar Cubo (**...**)|Exibe o cubo selecionado no momento.|  
|Painel Metadados|Exibe uma lista hierárquica de medidas, KPIs (Indicadores Chave de Desempenho) e dimensões definidas no cubo selecionado.|  
|Painel Membros Calculados|Exibe os membros calculados definidos no momento disponíveis para serem usados na consulta.|  
|Painel Filtro|Use para escolher dimensões e hierarquias relacionadas para filtrar dados na origem e limitar os dados retornados.|  
|Painel Dados|Exibe os cabeçalhos de coluna do conjunto de resultados à medida que você arrasta os itens do painel Metadados e do painel Membros Calculados. Atualiza automaticamente o conjunto de resultados se o botão **Executar Automaticamente** for selecionado.|  
  
 Você pode arrastar dimensões, medidas e KPIs do painel Metadados e membros calculados do painel Membro Calculado para o painel Dados. No painel Filtro, é possível selecionar dimensões e hierarquias relacionadas e definir expressões de filtro para limitar os dados disponíveis para consulta. Se o botão de alternância **Executar Automaticamente** (![Executar a consulta automaticamente](media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente")) na barra de ferramentas estiver selecionado, o designer de consultas executará a consulta sempre que você soltar um objeto de metadados no painel Dados. Execute a consulta manualmente usando o botão **Executar** (![Executar a consulta](media/rsqdicon-run.gif "Executar a consulta")) na barra de ferramentas.  
  
 Quando você cria uma consulta MDX nesse modo, as seguintes propriedades adicionais são incluídas automaticamente na consulta:  
  
 **Propriedades do Membro** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **Propriedades da Célula** VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
  
 Para especificar suas próprias propriedades adicionais, você deve editar manualmente a consulta MDX no modo Consulta.  
  
 Não há suporte para a importação de uma consulta .mdx a partir de um arquivo.  
  
> [!NOTE]  
>  Para obter mais informações sobre MDX e informações gerais sobre o designer de consulta MDX, consulte "Editor de consulta MDX (Analysis Services – Dados multidimensionais)" nos [Manuais Online do SQL Server](https://go.microsoft.com/fwlink/?linkid=98335).  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Barra de ferramentas do Designer de Consultas Gráficas MDX no modo Design  
 A barra de ferramentas do designer de consulta fornece botões para ajudá-lo a criar consultas MDX por meio da interface gráfica. A tabela a seguir lista os botões e as suas funções.  
  
|Botão|Descrição|  
|------------|-----------------|  
|**Editar como Texto**|Não habilitado para esse tipo de fonte de dados.|  
|**Importar**|Importa uma consulta existente de um arquivo de definição de relatório (.rdl) no sistema de arquivos.|  
|![Alterar para a exibição de consulta MDX](media/rsqdicon-commandtypemdx.gif "Alterar para a exibição de consulta MDX")|Alternar para Tipo de Comando MDX.|  
|![Atualizar dados de resultado](media/rsqdicon-refresh.gif "Atualizar dados de resultado")|Atualiza metadados na fonte de dados.|  
|![Adicionar membro calculado](media/rsqdicon-addcalculatedmember.gif "Adicionar Membro Calculado")|Exibe a caixa de diálogo **Construtor de Membro Calculado** .|  
|![Alternar para mostrar células vazias](media/rsqdicon-showemptycells.gif "Alternar para mostrar células vazias")|Alterna entre mostrar ou ocultar células vazias no painel Dados. (Equivale a usar a cláusula NON EMPTY em MDX).|  
|![Executar a consulta automaticamente](media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente")|Executa automaticamente a consulta e mostra o resultado sempre que é feita uma alteração. Os resultados são mostrados no painel Dados.|  
|![Botão Mostrar Agregações](media/rsqdicon-showaggregations.gif "Botão Mostrar Agregações")|Mostra agregações no painel Dados.|  
|![Delete (excluir)](media/rsqdicon-delete.gif "Excluir")|Exclui da consulta a coluna selecionada no painel Dados.|  
|![Ícone da caixa de diálogo Parâmetros de Consulta](media/iconqueryparameter.gif "Ícone da caixa de diálogo Parâmetros de Consulta")|Exiba a caixa de diálogo **Parâmetros de Consulta** . Quando você especifica os valores para um parâmetro de consulta, um parâmetro com o mesmo nome é automaticamente criado.|  
|![Botão Preparar Consulta](media/rsqdicon-preparequery.gif "Botão Preparar Consulta")|Prepara a consulta.|  
|![Executar a consulta](media/rsqdicon-run.gif "Executar a consulta")|Executa a consulta e exibe os resultados no painel Dados.|  
|![Cancelar a consulta](media/rsqdicon-cancel.gif "Cancelar a consulta")|Cancela a consulta.|  
|![Alternar para o modo Design](media/rsqdicon-designmode.gif "Alterna para o modo de design")|Alterna entre o modo Design e o modo Consulta.|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>Designer de Consultas Gráficas MDX no modo Consulta  
 Para alterar o designer de consultas gráficas para o modo **Consulta** , clique no botão de alternância **Modo Design** na barra de ferramentas.  
  
 A figura a seguir mostra os painéis do modo Consulta.  
  
 ![Designer de consultas MDX do Analysis Services, exibição de consulta](media/rsqd-dsawas-mdx-querymode.gif "Designer de consultas MDX do Analysis Services, exibição de consulta")  
  
 A tabela a seguir lista os painéis neste modo:  
  
|Painel|Função|  
|----------|--------------|  
|Botão Selecionar Cubo (**...**)|Exibe o cubo selecionado no momento.|  
|Painel Metadados/Funções/Modelos|Exibe uma lista hierárquica de medidas, KPIs e dimensões definidas no cubo selecionado.|  
|Painel Consulta|Exibe o texto da consulta.|  
|Painel Resultado|Exibe os resultados da execução da consulta.|  
  
 O painel Metadados exibe as guias para **Metadados**, **Funções**e **Modelos**. Na guia **Metadados** , você pode arrastar as dimensões, hierarquias, KPIs e medidas no painel Consulta MDX. Na guia **Funções** , você pode arrastar as funções no painel Consulta MDX. Na guia **Modelos** , você pode adicionar modelos MDX ao painel Consulta MDX. Quando você executar a consulta, o painel Resultado exibirá os resultados da consulta MDX.  
  
 Você pode ampliar a consulta MDX padrão gerada no modo Design para incluir propriedades do membro adicionais e propriedades da célula. Ao executar a consulta, esses valores não são exibidos no conjunto de resultados. No entanto, eles são passados de volta com a coleção de campos do conjunto de dados e você pode usar esses valores.  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Barra de ferramentas do Designer de Consultas Gráficas no modo Consulta  
 A barra de ferramentas do designer de consulta fornece botões para ajudá-lo a criar consultas MDX por meio da interface gráfica.  
  
 Os botões da barra de ferramentas são idênticos nos modos Design e Consulta, mas os botões a seguir não estão ativados no modo Consulta:  
  
-   **Editar como Texto**  
  
-   **Adicionar membro calculado** (![Adicionar membro calculado](media/rsqdicon-addcalculatedmember.gif "Adicionar Membro Calculado"))  
  
-   **Mostrar Células Vazias** (![Alternar para mostrar células vazias](media/rsqdicon-showemptycells.gif "Alternar para mostrar células vazias"))  
  
-   **Executar automaticamente** (![Executar a consulta automaticamente](media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente"))  
  
-   **Mostrar Agregações** (![Botão Mostrar Agregações](media/rsqdicon-showaggregations.gif "Botão Mostrar Agregações"))  
  
  
