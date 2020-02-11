---
title: Exibir dados de sessão de evento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ac742a01-2a95-42c7-b65e-ad565020dc49
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2fecf8a71854d7f8df160ba3ff63912086a34e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67131798"
---
# <a name="view-event-session-data"></a>Exibir dados de sessão de evento
  Este tópico descreve o uso da interface do usuário de exibição para ver e analisar dados de evento estendidos:  
  
-   Exibir Dados de Destino  
  
-   Trabalhando com dados  
  
## <a name="view-target-data"></a>Exibir Dados de Destino  
 Você pode exibir os dados coletados no destino especificado dentro do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="view-target-data"></a>Exibir Dados de Destino  
 Para exibir dados de destino:  
  
1.  No Pesquisador de Objetos, expanda **Gerenciamento**, **Eventos Estendidos**, **Sessões**e, em seguida, uma sessão.  
  
2.  Clique com o botão direito do mouse no nome do destino e clique em **Exibir Dados de Destino** para exibir os dados de destino.  
  
     A janela de dados de destino aparece na exibição padrão e mostra os dados de destino.  
  
 Observações sobre como exibir dados de destino:  
  
-   Os dados de destino não estão disponíveis para o destino ETW.  
  
-   Para exibir os dados de ring_buffer no formato xml, na janela de dados de destino, clique no link **dados de destino de ring_buffer** . O arquivo ring_buffer.xml aparece no editor de xml.  
  
-   Para um destino de event_file, exiba os dados de destino de arquivo (arquivo .XEL) usando um dos métodos a seguir:  
  
    -   Use o arquivo-> abrir [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]no.
    
    -   Arraste e solte o arquivo no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. 
    
    -   Clique duas vezes no arquivo .XEL.  
    
    -   No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique com o botão direito em uma sessão de Eventos Estendidos em execução e selecione Exibir Dados de Destino. 
    
    -   [fn_xe_file_target_read_file](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql).
    
    -   Use o PowerShell Read-SQLXevent no [módulo SqlServer. XEvent](https://www.powershellgallery.com/packages/SqlServer.XEvent).
    
    -   Consumir programaticamente XEvents usando o [NuGet do XELite](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite).
    
    -   Você pode exibir mais de um. XEL arquivo selecionando **mesclar arquivos de eventos estendidos** no menu arquivo-> abrir.

### <a name="watching-live-data"></a>Assistindo dados ao vivo  
 Você pode assistir dados ao vivo à medida que estão sendo capturados.  
  
-   No Pesquisador de objetos, expanda os nós **Gerenciamento**, **eventos estendidos**e **sessões** .  

-   Clique com o botão direito do mouse no nome da sessão e clique em **Observar Dados Dinâmicos** para começar a exibir dados de rastreamento.  
  
     As colunas de exibição padrão são **Nome do Evento** e **TimeStamp**.  
  
     Para adicionar mais colunas à janela de rastreamento, clique no botão **Escolher Colunas** na barra de ferramentas Eventos Estendidos. A guia **Detalhes** mostra todos os detalhes de evento do evento selecionado.  
  
     Em geral, os eventos são exibidos em aproximadamente 30 segundos. Se você quiser alterar o período de latência, poderá alterar a **Latência máxima de expedição** na página **Avançado** da caixa de diálogo **Nova Sessão** .  
     
-    Os dados dinâmicos podem ser transmitidos pelo [módulo SqlServer. XEvent do PowerShell](https://www.powershellgallery.com/packages/SqlServer.XEvent).
     
### <a name="to-refresh-target-data"></a>Para atualizar dados de destino  
 Atualizar dados de destino não tem suporte para destinos de event_files:  
  
1.  Para atualizar os dados de destino automaticamente, clique com o botão direito do mouse nesses dados, selecione **Intervalo de Atualização**e selecione o intervalo de atualização na lista de intervalos.  
  
2.  Para pausar e continuar a atualização automática, clique com o botão direito do mouse nos dados de destino e selecione **Pausar** ou **Retomar**.  
  
3.  Para exibir os dados de destino manualmente, clique com o botão direito do mouse nos dados de destino e selecione **Atualizar**.  
  
## <a name="working-with-data"></a>Trabalhando com dados  
 Você pode usar os recursos de análise da interface de usuário de Eventos Estendidos para identificar problemas.  
  
### <a name="details-pane"></a>Painel Detalhes  
 O painel de **Detalhes** mostra todas as colunas para o evento selecionado, incluindo campos e ações. Você pode adicionar uma coluna à tabela de dados de destino clicando com o botão direito em uma linha no painel de **Detalhes** e selecionando **Mostrar Coluna na Tabela**.  
  
### <a name="create-modify-or-delete-merged-columns"></a>Criar, modificar ou excluir colunas mescladas  
 Uma coluna mesclada permite que você combine um conjunto de campos a ser exibido em uma única coluna. A coluna mesclada mostrará os dados do primeiro campo não NULL baseado na ordem que eles são adicionados à lista de campos. Isto é semelhante ao que você vê no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Profiler, onde uma coluna específica pode mostrar dados diferentes dependendo do evento (o exemplo mais comum disto é o campo TextData no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Profiler). Para um exemplo, você pode mesclar os campos instrução e batch_text dos eventos sql_statement_completed e sql_batch_completed, respectivamente, em um campo nomeado myStatement. Quando você exibe a coluna myStatement na tabela, ela mostrará os dados apropriados para o evento associado.  
  
 Você pode criar, modificar ou excluir colunas mescladas:  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento. (Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **inspecionar dados dinâmicos**.)  
  
2.  Na janela de resultados de rastreamento, clique com o botão direito no cabeçalho de coluna e clique em **Escolher Colunas**.  
  
 Para criar uma coluna mesclada, clique em **Novo** na caixa de diálogo **Escolher Colunas** .  Na caixa de diálogo **Nova Coluna Mesclada** , nomeie a coluna mesclada e selecione as colunas originais a serem incluídas na coluna mesclada.  
  
 Para editar uma coluna mesclada, selecione uma coluna mesclada na caixa de diálogo **Escolher Colunas** e clique em **Editar**. Na caixa de diálogo **Editar Coluna Mesclada** , renomeie a coluna mesclada ou modifique as colunas originais a serem incluídas na coluna mesclada.  
  
 Para excluir uma coluna mesclada, selecione uma coluna mesclada na caixa de diálogo **Escolher Colunas** e clique em **Excluir**.  
  
### <a name="filter-results"></a>Filtrar resultados  
 Você pode exibir resultados de rastreamento e aplicar filtros para reduzir os resultados do rastreamento que são exibidos na janela de rastreamento. O filtro de exibição inclui um filtro de hora e um filtro avançado. Use o filtro de hora para filtrar os resultados de rastreamento por carimbo de data/hora de evento e use o filtro avançado para construir condições de filtro usando os campos de eventos e ações. Há um relacionamento "e" entre os filtros de hora e avançado.  
  
 Para criar um filtro:  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento. (Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **inspecionar dados dinâmicos**.)  
  
2.  Na janela de resultados de rastreamento, selecione os resultados que você deseja filtrar e, na barra de ferramentas **Eventos Estendidos** , clique no botão **Filtros**.  
  
3.  Na caixa de diálogo **Filtros** , selecione **Definir filtro de hora** para definir o filtro de hora arrastando o controle deslizante ou modificando a hora na caixa de edição.  
  
4.  Na seção **filtros adicionais** , aplique os critérios de filtro e clique em **aplicar**.  
  
### <a name="sort-results"></a>Classificar Resultados  
 Para classificar os resultados em ordem crescente ou decrescente:  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento. (Você também pode clicar com o botão direito do mouse no nome da sessão, selecionar **observar dados dinâmicos**e clicar no botão **parar feed de dados** na barra de ferramentas.)  
  
2.  Na janela de resultados de rastreamento, clique com o botão direito do mouse no cabeçalho da coluna que você quer classificar e clique em **Classificação Crescente** ou **Classificação Decrescente**.  
  
 Você também pode clicar no cabeçalho da coluna para reverter a ordem de classificação.  
  
 Se você agrupou colunas, classificar a coluna só classificará os dados dentro do grupo.  
  
### <a name="group-results"></a>Agrupar resultados  
 Os resultados agrupados são equivalentes à funcionalidade da cláusula `GROUP BY` no [!INCLUDE[tsql](../includes/tsql-md.md)]. A tabela de dados de destino mostrará os dados agrupados, permitindo expandir e recolher os dados.  
  
 Você deve agrupar dados antes de poder agregá-lo. Por exemplo, você pode agrupar no valor query_hash, classificar em ordem decrescente por duração, obter a duração média para cada grupo e classificar em ordem decrescente na agregação.  Isto produzirá uma lista que mostra a lista de instruções exclusivas da duração média mais longa para a mais curta. Quando você expande o grupo de nível superior, você verá as execuções individuais daquela consulta específica classificada da mais longa para a mais curta.  
  
 Você pode agrupar os resultados por uma única coluna ou por várias colunas.  
  
 Abra um arquivo .XEL para exibir os resultados do rastreamento. (Você também pode clicar com o botão direito do mouse no nome da sessão, selecionar **observar dados dinâmicos**e clicar no botão **parar feed de dados** na barra de ferramentas.)  
  
 Para agrupar resultados por uma única coluna, clique com o botão direito do mouse no cabeçalho da coluna na janela de resultados de rastreamento e clique em **Agrupar por Esta Coluna**. Para desfazer o agrupamento, selecione uma das linhas e clique em **Remover Todo o Agrupamento**.  
  
 Para agrupar resultados por várias colunas, clique no botão **Agrupamento** na barra de ferramentas **Eventos Estendidos** . Na caixa de diálogo **Colunas disponíveis** da caixa de diálogo **Agrupamento** , selecione as colunas que você quer agrupar e mova-as na caixa **Colunas agrupadas em** . Para alterar a ordem, na caixa **Colunas agrupadas em** , clique nas setas para cima ou para baixo.  
  
### <a name="aggregate-results"></a>Agregar resultados  
 Você pode exibir os resultados de rastreamento e analisar mais profundamente os dados de seu evento agregando colunas em seus resultados. Eventos Estendidos dão suporte a cinco funções de agregação:  
  
-   sum  
  
-   Min  
  
-   max  
  
-   média  
  
-   count  
  
 Sum, Min, Max e Average podem ser usados somente com as colunas numéricas. Count é o número de valores não nulos que existem para a coluna selecionada no grupo.  
  
 A agregação é realizada em um grupo; portanto, você deve agrupar os resultados antes de você executar a agregação. Para agregar resultados:  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento. (Você também pode clicar com o botão direito do mouse no nome da sessão, selecionar **observar dados dinâmicos**e clicar no botão **parar feed de dados** na barra de ferramentas.)  
  
2.  Na barra de ferramentas **Eventos Estendidos** , clique no botão **Agregação** . A caixa de diálogo Agregação exibirá as colunas disponíveis para agregação.  
  
3.  Na coluna **Tipo de Agregação** , selecione o tipo de agregação.  
  
4.  Na caixa **Classificar agregação por** , selecione a coluna de classificação. Em seguida, selecione em ordem crescente ou decrescente.  
  
### <a name="search-for-text-in-columns"></a>Pesquisar texto nas colunas  
 Você pode pesquisar texto nas colunas:  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento. (Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **Observar Dados Dinâmicos**.)  
  
2.  Clique em **Localizar** na barra de ferramentas **Eventos Estendidos** .  
  
3.  Na caixa de diálogo **Localizar** da caixa de diálogo **Localizar nos Eventos Estendidos** , insira o texto de pesquisa. Você pode selecionar uma das suas últimas 20 cadeias de caracteres pesquisadas na lista suspensa.  
  
4.  Na caixa **Examinar** , selecione o local para pesquisar o texto especificado. Use as seguintes opções para procurar:  
  
    -   Colunas da tabela. Use esta opção para procurar todas as colunas visíveis na janela de rastreamento.  
  
    -   Detalhes. Use esta opção para pesquisar todas as colunas (promovidas e não promovidas) na janela de rastreamento que foram selecionadas antes de abrir a caixa de diálogo **Localizar em eventos estendidos** .  
  
    -   *Event_column_name*. Use esta opção para procurar uma coluna de evento específica na lista suspensa.  
  
5.  Use as opções a seguir para especificar como você quer definir a pesquisa:  
  
    -   Diferenciar maiúsculas de minúsculas. Use esta opção para exibir os resultados da pesquisa para o texto que você inseriu na caixa Localizar que corresponde conteúdo e caso.  
  
    -   Coincidir palavra inteira. Use esta opção para exibir somente os resultados da pesquisa para o texto que você inseriu que corresponde palavras completas.  
  
    -   Pesquisar para cima. Use esta opção para pesquisar do local do seu cursor para o início dos resultados.  
  
    -   Usar. Use esta opção para interpretar os caracteres especiais e as expressões regulares que você inseriu na caixa Localizar. Caracteres especiais incluem os caracteres curinga (*) e (?) para representar um ou mais caracteres. Expressões regulares são notações especiais usadas para definir padrões de texto de pesquisa.  
  
    -   Clique em **Localizar Próximo** para procurar o próximo texto que você inseriu na caixa **Localizar** .  
  
### <a name="bookmarks"></a>Indicadores  
 Para facilitar o retorno a uma linha, você poderá marcar uma ou mais linhas nos dados de destino. Clique com o botão direito do mouse para alterar o indicador. Use os botões anterior e próximo na barra de ferramentas **Eventos Estendidos** para navegar para linhas marcadas.  
  
### <a name="change-display-settings"></a>Alterar as configurações de exibição  
 Você pode salvar informações de coluna (ordem de coluna, coluna de mesclagem e largura de coluna) e informações de filtro de um resultado de rastreamento em um arquivo de configuração de exibição de Eventos Estendidos (arquivo .viewsetting). Após salvar o arquivo, você pode aplicá-lo aos seus resultados de rastreamento para alterar a exibição.  
  
 Para alterar as configurações de exibição:  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento. (Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **Observar Dados Dinâmicos**.)  
  
2.  Na barra de ferramentas **Eventos Estendidos** , selecione **Configurações de Vídeo**. Na lista suspensa, selecione uma das seguintes opções:  
  
    -   Salvar como. Salve as colunas e informações de filtro de um resultado de rastreamento em um arquivo .viewsetting.  
  
    -   Abrir. Abra um arquivo .viewsetting existente.  
  
    -   Abrir recente. Abra um arquivo .viewsetting salvo recentemente.  
  
### <a name="copy-or-export-trace-results"></a>Copiar ou exportar resultados de rastreamento  
 Você pode copiar células, linhas e detalhes para linhas selecionadas de seus resultados do rastreamento. Você também pode exportar seus resultados do rastreamento para os itens a seguir:  
  
-   Arquivo .XEL  
  
-   tabela  
  
-   Arquivo .CSV  
  
 Para copiar resultados de rastreamento, selecione uma célula, linha ou linhas, clique com o botão direito, selecione **Cópia** e em **Célula**, **Linha**ou **Detalhes**. A opção Eventos Estendidos oferece suporte à cópia de um máximo de 1.000 linhas.  
  
 Você pode exportar resultados de rastreamento para um arquivo .XEL, tabela ou arquivo .CSV selecionando **Exportar para** da opção de menu **Eventos Estendidos** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="view-a-deadlock-graph-and-query-plans"></a>Exibir um gráfico de Deadlock e planos de consulta  
 Você pode exibir o deadlock graph para **xml_deadlock_report** no painel Detalhes para ajudar a solucionar problemas de deadlocks. Você também pode exibir gráficos de plano de consulta para os seguintes eventos:  
  
-   query_post_compilation_showplan  
  
-   query_pre_execution_showplan  
  
-   query_post_execution_showplan  
  
 Para exibir o deadlock graph:  
  
-   No Pesquisador de objetos, expanda os nós **Gerenciamento**, **eventos estendidos**e **sessões** .  
  
-   Clique com o botão direito do mouse na sessão que contém o evento de deadlock configurado que você deseja exibir e selecione **Observar Dados Dinâmicos**.  
  
-   Selecione o evento de deadlock e exiba o gráfico na guia **Deadlock** no painel Detalhes.  
  
 Para exibir gráficos de plano de consulta:  
  
1.  No Pesquisador de objetos, expanda os nós **Gerenciamento**, **eventos estendidos**e **sessões** .  
  
2.  Clique com o botão direito do mouse na sessão que contém o gráfico de plano de consulta que você deseja exibir (por exemplo, query_post_compilation_showplan) e selecione **Observar Dados Dinâmicos**.  
  
3.  Selecione o evento de gráfico de plano de consulta (por exemplo, query_post_compilation_showplan) e exiba o gráfico na guia **Plano de consulta** no painel Detalhes.  
  
  
