---
title: Barra de ferramentas (guia navegador, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a1c6272d-e514-456b-9995-b73fec0112a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fe356d15c0602f33ec9c59ee463a69783686899b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066147"
---
# <a name="toolbar-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Barra de Ferramentas (guia Navegador, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use os recursos na **Barra de Ferramentas** no Designer de Cubo para executar operações comuns ao criar ou procurar um cubo ou seu objeto, ou ao criar uma consulta MDX. As operações comuns ao tempo de design e exibição de consulta incluem a definição de o contexto do usuário, o processamento dos objetos e a definição do idioma padrão.  
  
 A tabela a seguir lista os botões da **Barra de Ferramentas** e suas funções.  
  
|Botão|Descrição|  
|------------|-----------------|  
|**Editar como Texto**|Não habilitado para esse tipo de fonte de dados.|  
|**Importar**|Importa uma consulta existente de um arquivo de definição de relatório (.rdl) no sistema de arquivos.|  
|![Alterar para a exibição de consulta MDX](media/rsqdicon-commandtypemdx.gif "Alterar para a exibição de consulta MDX")|Alternar para Tipo de Comando MDX.|  
|![Atualizar dados de resultados](media/rsqdicon-refresh.gif "Atualizar dados de resultados")|Atualiza metadados na fonte de dados.|  
|![Add calculated member](media/rsqdicon-addcalculatedmember.gif "Add calculated member")|Exibe a caixa de diálogo **Construtor de Membro Calculado** .|  
|![Alternar para mostrar células vazias](media/rsqdicon-showemptycells.gif "Alternar para mostrar células vazias")|Alterna entre mostrar ou ocultar células vazias no painel Dados. (Equivale a usar a cláusula NON EMPTY em MDX).|  
|![Executar a consulta automaticamente](media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente")|Executa automaticamente a consulta e mostra o resultado sempre que é feita uma alteração. Os resultados são mostrados no painel Dados.|  
|![Botão Mostrar Agregações](media/rsqdicon-showaggregations.gif "Botão Mostrar Agregações")|Mostra agregações no painel Dados.|  
|![Excluir](media/rsqdicon-delete.gif "Excluir")|Exclui da consulta a coluna selecionada no painel Dados.|  
|![Ícone da caixa de diálogo Parâmetros de Consulta](media/iconqueryparameter.gif "Ícone da caixa de diálogo Parâmetros de Consulta")|Exiba a caixa de diálogo **Parâmetros de Consulta** . Quando você especifica os valores para um parâmetro de consulta, um parâmetro com o mesmo nome é automaticamente criado.|  
|![Botão Preparar Consulta](media/rsqdicon-preparequery.gif "Botão Preparar Consulta")|Prepara a consulta.|  
|![Executar a consulta](media/rsqdicon-run.gif "Executar a consulta")|Executa a consulta e exibe os resultados no painel Dados.|  
|![Cancelar a consulta](media/rsqdicon-cancel.gif "Cancelar a consulta")|Cancela a consulta.|  
|![Alternar para o modo de Design](media/rsqdicon-designmode.gif "Alternar para o modo de Design")|Alterna entre o modo Design e o modo Consulta.|  
  
 Em geral, os botões da barra de ferramentas são idênticos no **Modo de Design** e **Modo de Consulta**. Porém, os botões seguintes não estão habilitados para o modo de Consulta:  
  
-   **Editar como Texto**  
  
-   **Adicionar Membro Calculado** (![Add calculated member](media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Mostrar Células Vazias** (![Alternar para mostrar células vazias](media/rsqdicon-showemptycells.gif "Alternar para mostrar células vazias"))  
  
-   **Executar automaticamente** (![Executar a consulta automaticamente](media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente"))  
  
-   **Mostrar Agregações** (![botão Mostrar Agregações](media/rsqdicon-showaggregations.gif "botão Mostrar Agregações"))  
  
## <a name="options"></a>Opções  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Processar**|Clique para exibir a caixa de diálogo **Processar** e processar o cubo. Para obter mais informações sobre a caixa de diálogo **Processar**, consulte [Caixa de diálogo Processar &#40;Analysis Services – Dados Multidimensionais&#41;](process-dialog-box-analysis-services-multidimensional-data.md).|  
|**Alterar usuário**|Clique para exibir a caixa de diálogo **Contexto de Segurança** e alterar o usuário e a função usados na guia **Navegador**. Para obter mais informações sobre a caixa de diálogo **Contexto de Segurança**, consulte [Caixa de diálogo Contexto de Segurança &#40;Analysis Services – Dados Multidimensionais&#41;](security-context-dialog-box-analysis-services-multidimensional-data.md).|  
|**Reconnect**|Clique para reconectar a guia **Cálculos** com a instância e o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que contém o cubo, se a sessão da guia **Navegador** for desconectada devido a perda ou tempo limite da conexão.|  
|**Atualizar**|Clique para atualizar os painéis de **Metadados** e de **Relatórios** .|  
|**Classificar em Ordem Crescente**|Clique para classificar as irmãs da linha selecionada no painel de **Relatório** em ordem crescente no idioma especificado em **Idioma**.<br /><br /> **Observação** esta opção será habilitada apenas se uma célula no painel **Relatórios** for selecionada.|  
|**Classificar em Ordem Decrescente**|Clique para classificar as irmãs da linha selecionada no painel de **Relatório** em ordem decrescente no idioma especificado em **Idioma**.<br /><br /> Observação: Essa opção é habilitada somente se uma célula na **relatórios** painel é selecionado.|  
|**Filtro automático**|Clique para filtrar os resultados automaticamente no painel **Resultado** .|  
|**Mostrar apenas de cima para baixo**|Selecione um valor ou percentual para mostrar apenas o número superior ou inferior ou o percentual de células no painel **Relatório** com base na medida selecionada.<br /><br /> Para obter mais informações sobre essa opção, consulte [TopCount &#40;MDX&#41;](/sql/mdx/topcount-mdx), [TopPercent &#40;MDX&#41;](/sql/mdx/toppercent-mdx), [BottomCount &#40;MDX&#41;](/sql/mdx/bottomcount-mdx) e [BottomPercent &#40;MDX&#41;](/sql/mdx/bottompercent-mdx).|  
|**Subtotal**|Clique para exibir subtotais.|  
|**Totais de todos os itens**|Clique para exibir os totais de Todos os membros no painel **Relatório** .|  
|**Mostrar células vazias**|Clique para exibir células vazias no painel **Relatório** .|  
|**Limpar resultados**|Clique para limpar os resultados no painel **Relatório** .|  
|**Comandos e opções**|Clique para exibir a caixa de diálogo **Comandos e Opções** e editar propriedades avançadas do controle da Tabela Dinâmica do Microsoft Office 11.0 no painel **Relatório** . Para obter mais informações sobre a caixa de diálogo **Comandos e Opções** , consulte a documentação do Microsoft Office.|  
|**Perspectiva**|Selecione a perspectiva da qual exibir dados e metadados nos painéis de **Metadados** e de **Relatório** .<br /><br /> Para exibir o cubo sem usar uma perspectiva, selecione o nome do cubo.|  
|**Idioma**|Selecione o idioma com o qual exibir dados e metadados nos painéis de **Metadados** e de **Relatório** .<br /><br /> Para exibir o cubo que usa o idioma padrão, selecione **Padrão**.|  
  
  
