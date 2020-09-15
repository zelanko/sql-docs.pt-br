---
description: Navegar no Designer de Consulta e Exibição (Visual Database Tools)
title: Navegar no designer de exibição e de consultas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, navigating
- shortcuts [SQL Server]
- Query Designer [SQL Server], navigating
- keyboard shortcuts [Visual Database Tools]
ms.assetid: 1c65acef-6dfa-463a-bf37-5a5335fe3865
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: ff0153da9b3905fb57d0e1359ff71aaaeef663df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423070"
---
# <a name="navigate-in-the-query-and-view-designer-visual-database-tools"></a>Navegar no Designer de Consulta e Exibição (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Você pode trabalhar no Designer de Consulta e Exibição usando o teclado ou o mouse. Consulte as seguintes tabelas para obter métodos específicos.  
  
## <a name="any-pane"></a>Qualquer painel  
  
|**Para**|**Pressione**|**Clique em**|  
|----------|-------------|-------------|  
|Mover entre os painéis do Designer de Consulta e Exibição|F6, SHIFT+F6|Em qualquer lugar no painel de destino|  
  
> [!TIP]  
> Você pode usar as teclas de atalho CTRL+TAB para alterar foco para outros painéis além dos painéis do Designer de Consulta e Exibição.  
  
## <a name="diagram-pane"></a>Painel Diagrama  
  
|**Para**|**Pressione**|**Clique em**|  
|----------|-------------|-------------|  
|Mover entre tabelas, outros objetos estruturados em tabelas (e para linhas de junção, se disponíveis)|TAB ou SHIFT+TAB|Na tabela, no objeto estruturado por tabela ou na linha de junção a ser movida|  
|Mover entre as colunas de uma tabela ou objeto estruturado por tabela|Teclas de direção|Na coluna para a qual ir|  
|Escolher a coluna de dados selecionada para saída|BARRA DE ESPAÇOS ou tecla +|Na caixa de seleção próxima ao nome da coluna|  
|Remover a coluna de dados selecionada da saída da consulta|BARRA DE ESPAÇOS ou tecla -|Na caixa de seleção próxima ao nome da coluna|  
|Remover a tabela selecionada, o objeto estruturado por tabela ou a linha de junção da consulta|Delete (excluir)|Clique com o botão direito do mouse e escolha **Remover**|  
  
> [!NOTE]  
> Se forem selecionados vários itens, pressionar esta tecla afetará todos os itens selecionados. Selecione vários itens mantendo a tecla CTRL pressionada enquanto clica neles.  
  
Para obter mais informações, consulte [Painel Diagrama &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md).  
  
## <a name="criteria-pane"></a>Painel de Critérios  
  
|Para|Pressione|Clique em|  
|------|---------|---------|  
|Mover entre células|Teclas de direção, TAB ou SHIFT+TAB|Na célula de destino|  
|Mover para a última linha em uma coluna selecionada|CTRL+SETA PARA BAIXO||  
|Mover para a primeira linha em uma coluna selecionada|CTRL+SETA PARA CIMA||  
|Mover para a célula superior esquerda na parte visível da grade|CTRL+HOME||  
|Mover para a célula inferior direita|CTRL+END||  
|Mover em uma lista suspensa|SETA PARA CIMA ou SETA PARA BAIXO|No botão da célula|  
|Selecionar uma coluna inteira de grade|CTRL+BARA DE ESPAÇOS|O cabeçalho da coluna|  
|Alternar entre o modo de edição e o modo de seleção de célula|F2||  
|Copiar o texto selecionado em uma célula para a Área de Transferência (no modo de edição)|CTRL+C||  
|Cortar o texto selecionado em uma célula e colocá-lo na Área de Transferência (no modo de edição)|CTRL+X||  
|Colar o texto da Área de Transferência (no modo de edição)|CTRL+V||  
|Alternar entre os modos de inserção e sobreposição ao editar uma célula|INS||  
|Alternar a caixa de seleção na coluna Saída|BARRA DE ESPAÇOS|Na caixa de seleção|  
|Desmarcar o conteúdo selecionado de uma célula|Delete (excluir)||  
|Limpar todos os valores de uma coluna selecionada de grade|Delete (excluir)||  
|Inserir uma linha entre as linhas existentes|INS depois de selecionar uma linha de grade||  
|Adicionar uma coluna Ou...|INS depois de selecionar qualquer coluna Ou...||  
  
> [!NOTE]  
> Se forem selecionados vários itens, pressionar esta tecla afetará todos os itens selecionados.  
  
Para obter mais informações, consulte [Painel Critérios &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md).  
  
## <a name="sql-pane"></a>painel SQL  
Você pode usar as teclas de edição padrão do Windows ao trabalhar no painel SQL, como CTRL+Seta para se mover entre palavras, e os comandos **Recortar**, **Copiar**e **Colar** no menu **Editar** .  
  
> [!NOTE]  
> Você só pode inserir texto; não há um modo de sobreposição.  
  
Para obter mais informações, consulte [Painel SQL &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
## <a name="results-pane"></a>Painel de Resultados  
  
|**Para**|**Pressione**|**Clique em**|  
|----------|-------------|-------------|  
|Mover entre células|Teclas de direção, TAB ou SHIFT+TAB|Na célula de destino|  
|Mover para a primeira ou para a última célula na fila atual|HOME ou END||  
|Mover para a primeira linha na coluna atual|CTRL+SETA PARA CIMA||  
|Mover para a célula superior esquerda|CTRL+HOME||  
|Mover para a célula inferior na primeira coluna|CTRL+SETA PARA BAIXO||  
|Selecionar o primeiro caractere em uma célula|SHIFT+HOME||  
|Selecionar o último caractere em uma célula|SHIFT+END||  
|Alternar entre o modo de edição e o modo de seleção de célula|F2||  
|Alternar entre os modos de inserção e sobreposição ao editar uma célula|INS||  
|Excluir uma linha da tabela|Delete (excluir)||  
|Desfazer alterações na célula atual|ESC em célula alterada||  
|Desfazer alterações na linha atual|ESC em qualquer célula não alterada||  
|Inserir null em uma célula|CTRL+0||  
|Copiar colunas ou linhas selecionadas para a Área de Transferência|CTRL+C||  
|Copiar o texto selecionado em uma célula para a Área de Transferência (no modo de edição)|CTRL+C||  
|Cortar o texto selecionado em uma célula para a Área de Transferência (no modo de edição)|CTRL+X||  
|Colar o texto da Área de Transferência (no modo de edição)|CTRL+V||  
  
> [!NOTE]  
> Se forem selecionados vários itens, pressionar esta tecla afetará todos os itens selecionados.  
  
Para obter mais informações, consulte [Painel de Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
