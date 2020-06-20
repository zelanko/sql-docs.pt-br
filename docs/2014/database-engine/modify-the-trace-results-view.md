---
title: Modificar o modo de exibição de resultados de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 860a80dc-bac0-4ef0-bf7f-7a9b430d7aa3
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0c5aa031804d2c5f4ad3a3679a6fe1cac96c63b1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930647"
---
# <a name="modify-the-trace-results-view"></a>Modificar a exibição dos resultados de rastreamento
  Este tópico descreve como modificar a exibição dos resultados do rastreamento de uma sessão de Eventos Estendidos no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] executando as tarefas a seguir.  
  
1.  [Adicionar ou remover colunas](#AddRemoveColumns)  
  
2.  [Criar, editar ou excluir colunas mescladas](#ChangeColumns)  
  
3.  [Classificar os resultados](#SortResults)  
  
4.  [Agrupar os resultados](#GroupResults)  
  
5.  [Agregar os resultados](#AggregateResults)  
  
6.  [Filtrar os resultados](#Filter)  
  
7.  [Pesquisar texto nas colunas](#Search)  
  
8.  [Alterar as configurações de exibição](#ChangeDisplay)  
  
##  <a name="add-or-remove-columns"></a><a name="AddRemoveColumns"></a>Adicionar ou remover colunas  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **observar dados dinâmicos**.  
  
2.  Na janela de resultados de rastreamento, clique com o botão direito no cabeçalho de coluna e selecione **Escolher Colunas**.  
  
3.  Na caixa de diálogo **Escolher Colunas** , na seção **Colunas disponíveis** , selecione os nomes de colunas que você quer adicionar e clique na seta para a direita.  
  
    > [!NOTE]  
    >  Por padrão, as colunas são organizadas por nome. Para exibir as colunas por evento, clique em **Organizar por evento**.  
  
     Para remover colunas, na seção **Colunas selecionadas** , selecione as colunas que você quer remover e clique na seta para a esquerda.  
  
4.  Na seção **Colunas selecionadas** , para alterar a exibição da ordem das colunas, clique em **Mover para cima** ou **Mover para baixo** respectivamente. Você não pode mover várias linhas.  
  
5.  Clique em **OK**.  
  
##  <a name="create-edit-or-delete-merged-columns"></a><a name="ChangeColumns"></a>Criar, editar ou excluir colunas mescladas  
  
#### <a name="to-create-merged-columns"></a>Para criar colunas mescladas  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **observar dados dinâmicos**.  
  
2.  Na janela de resultados de rastreamento, clique com o botão direito no cabeçalho de coluna e clique em **Escolher Colunas**.  
  
3.  Na caixa de diálogo **Escolher Colunas** , clique em **Novo**.  
  
4.  Na caixa de diálogo **Nova Coluna Mesclada** , na caixa **Nome da coluna mesclada** , insira um nome para as colunas mescladas.  
  
5.  Na caixa **Colunas originais a serem mescladas** , selecione duas ou mais colunas para serem mescladas da lista suspensa.  
  
    > [!NOTE]  
    >  Eventos Estendidos só dão suporte a mesclagem de até cinco colunas.  
  
6.  Clique em **OK**.  
  
#### <a name="to-edit-merged-columns"></a>Para editar colunas mescladas  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **observar dados dinâmicos**.  
  
2.  Na janela de resultados de rastreamento, clique com o botão direito no cabeçalho de coluna e clique em **Escolher Colunas**.  
  
3.  Na caixa de diálogo **Escolher Colunas** , clique em **Editar**.  
  
4.  Para alterar o nome da coluna mesclada, na caixa de diálogo **Nova Coluna Mesclada** , na caixa **Nome da coluna mesclada** , insira um nome.  
  
     Para alterar as colunas que você quer mesclar, na caixa **Colunas originais a serem mescladas** , selecione as colunas que você quer mesclar na lista suspensa e clique em **OK**.  
  
#### <a name="to-delete-merged-columns"></a>Para excluir as colunas mescladas  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **observar dados dinâmicos**.  
  
2.  Na janela de resultados de rastreamento, clique com o botão direito no cabeçalho de coluna e clique em **Escolher Colunas**.  
  
3.  Na caixa de diálogo **Escolher Colunas** , marque o nome da coluna mesclada que você quer excluir e clique em **Excluir**.  
  
##  <a name="sort-the-results"></a><a name="SortResults"></a>Classificar os resultados  
  
#### <a name="to-sort-the-results-in-ascending-or-descending-order"></a>Para classificar os resultados em ordem crescente ou decrescente  
  
-   Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão, selecionar **observar dados dinâmicos**e clicar no botão **parar feed de dados** na barra de ferramentas.  
  
-   Na janela dos resultados de rastreamento, clique com o botão direito em um cabeçalho de coluna que você deseja classificar. Clique em **Classificação Crescente** ou em **Classificação Decrescente** para classificar a coluna em ordem crescente ou decrescente respectivamente.  
  
     Se você agrupou colunas, classificar a coluna só classificará os dados dentro do grupo.  
  
##  <a name="group-results"></a><a name="GroupResults"></a>Resultados do grupo  
  
#### <a name="to-group-the-results-by-a-single-column"></a>Para agrupar os resultados por uma única coluna  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito no nome da sessão, **Observar Dados Dinâmicos**e em seguida clicar no botão **Parar Feed de Dados** na barra de ferramentas Eventos Estendidos.  
  
2.  Na janela dos resultados de rastreamento, clique com o botão direito do mouse no cabeçalho da coluna que você quer agrupar e clique em **Agrupar por Esta Coluna**.  
  
#### <a name="to-group-the-results-by-multiple-columns"></a>Para agrupar os resultados por várias colunas  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão, selecionar **observar dados dinâmicos**e clicar no botão **parar feed de dados** na barra de ferramentas.  
  
2.  Clique no botão **Agrupamento** na barra de ferramentas Eventos Estendidos.  
  
3.  Na caixa de diálogo **Agrupamento** , na caixa **Colunas disponíveis** , selecione as colunas que você deseja agrupar e clique na seta para a direita.  
  
     Para alterar a ordem de agrupamento, na seção **Colunas agrupadas em** , clique nas setas para cima ou para baixo.  
  
     Para remover colunas do agrupamento, na caixa **Colunas agrupadas em** , selecione as colunas que você quer remover e clique na seta para a esquerda.  
  
4.  Clique em **OK**.  
  
##  <a name="aggregate-results"></a><a name="AggregateResults"></a>Agregar resultados  
 Eventos Estendidos dão suporte a cinco funções de agregação:  
  
-   SUM  
  
-   Mín  
  
-   Max  
  
-   Média  
  
-   Contagem  
  
 Sum, Min, Max e Average podem ser usados somente com as colunas numéricas disponíveis. Count é o número de valores não nulos que existem para a coluna selecionada no grupo.  
  
#### <a name="to-aggregate-results"></a>Para agregar resultados  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão, selecionar **observar dados dinâmicos**e clicar no botão **parar feed de dados** na barra de ferramentas.  
  
    > [!NOTE]  
    >  A agregação é executada em um grupo; portanto, você deve agrupar os resultados antes de você executar a agregação.  
  
2.  Na barra de ferramentas Eventos Estendidos, clique no botão **Agregação** .  
  
     A caixa de diálogo **Agregação** aparece exibindo as colunas disponíveis para agregação.  
  
3.  Em **Tipo de Agregação**, selecione como você deseja agregar a coluna correspondente da lista suspensa.  
  
4.  Na caixa **Classificar agregação por** , selecione a coluna pela qual deseja classificar na lista suspensa.  
  
5.  Selecione a opção **Em ordem crescente** para classificar o resultado da agregação em ordem crescente.  
  
6.  Selecione a opção **Em ordem decrescente** para classificar o resultado da agregação em ordem decrescente.  
  
7.  Clique em **OK**.  
  
##  <a name="filter-results"></a><a name="Filter"></a>Filtrar resultados  
 Você pode aplicar filtros para refinar os resultados do rastreamento que são exibidos na janela de rastreamento. O filtro de exibição inclui um filtro de hora e um filtro avançado. Use o filtro de hora para filtrar os resultados de rastreamento por carimbo de data/hora de evento e use o filtro avançado para construir condições de filtro usando os campos de eventos e ações. Há uma relação AND lógica entre os filtros Hora e Avançado.  
  
#### <a name="to-create-a-filter"></a>Para criar um filtro  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **observar dados dinâmicos**.  
  
2.  Na janela de resultados de rastreamento, selecione os resultados que você deseja filtrar e, na barra de ferramentas Eventos Estendidos, clique no botão **Filtros** .  
  
3.  Na caixa de diálogo **Filtros** , selecione **Definir filtro de hora** para definir o filtro de hora arrastando o controle deslizante tranca para definir a linha de tempo. Observe que, quando você move as barras de controle deslizante, a caixa de hora exibe o valor de tempo de acordo. Você também pode inserir a hora nas caixas de hora ou selecioná-la na lista suspensa. Observe que, quando você inserir a hora, o controle deslizante do tempo restante moverá de acordo.  
  
4.  Na seção **filtros adicionais** , aplique os critérios de filtro e clique em **aplicar**. Quando acabar de criar o filtro, clique em **OK**.  
  
 Uma situação especial ocorre quando um campo de evento tem o mesmo nome de uma ação. Um exemplo disso seria session_id. Há vários eventos que incluem um campo session_id e você também pode adicionar a ação session_id. Ambas as informações são coletadas, mas a grade de exibição do profiler Eventos Estendidos usa a lógica a seguir.  
  
-   Somente uma cópia da coluna (session_id nesse caso) é mostrada na exibição de grade.  
  
-   Se houver campos e ação nos dados, o valor do campo será mostrado.  
  
-   Se apenas o campo ou a ação existir nos dados, o campo ou a ação será exibido.  
  
-   Se não houver nem o campo nem a ação, NULL será exibido.  
  
##  <a name="search-for-text-in-columns"></a><a name="Search"></a>Pesquisar texto em colunas  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **observar dados dinâmicos**.  
  
2.  Na barra de ferramentas Eventos Estendidos, clique no botão **Localizar** .  
  
3.  Na caixa de diálogo **Localizar nos Eventos Estendidos** , na caixa **Localizar** , insira o texto que você quer procurar.  
  
     Você pode selecionar uma das suas últimas 20 cadeias de caracteres pesquisadas na lista suspensa.  
  
4.  Na caixa **Examinar** , selecione o local no qual procurar o texto especificado na lista suspensa. Use as seguintes opções para procurar:  
  
    -   **Colunas da tabela**. Use esta opção para procurar todas as colunas visíveis na janela de rastreamento.  
  
    -   **Detalhes**. Use esta opção para pesquisar todas as colunas (promovidas e não promovidas) na janela de rastreamento que foram selecionadas antes de abrir a caixa de diálogo **Localizar em eventos estendidos** .  
  
    -   **\<Event column name>**. Use esta opção para procurar uma coluna de evento específica na lista suspensa.  
  
5.  Use as opções a seguir para especificar como você quer definir a pesquisa:  
  
    1.  **Diferenciar maiúsculas de minúsculas**. Use esta opção para exibir os resultados da pesquisa para o texto que você inseriu na caixa **Localizar** que corresponde tanto ao conteúdo quanto ao caso.  
  
    2.  **Coincidir palavra inteira**. Use esta opção para exibir somente os resultados da pesquisa para o texto que você inseriu que corresponde palavras completas.  
  
    3.  **Pesquisar para cima**. Use esta opção para pesquisar do local do seu cursor para o início dos resultados.  
  
    4.  **Use**o. Use esta opção para interpretar os caracteres especiais e as expressões regulares que você inseriu na caixa **Localizar** . Caracteres especiais incluem os caracteres curinga (*) e (?) para representar um ou mais caracteres. Expressões regulares são notações especiais usadas para definir padrões de texto de pesquisa.  
  
6.  Clique em **Localizar Próximo** para procurar o próximo texto que você inseriu na caixa **Localizar** .  
  
##  <a name="change-the-display-settings"></a><a name="ChangeDisplay"></a>Alterar as configurações de exibição  
 Você pode salvar informações de coluna (ordem de coluna, coluna de mesclagem e largura de coluna) e informações de filtro de um resultado de rastreamento em um arquivo de configuração de exibição de Eventos Estendidos (arquivo .viewsetting). Após salvar o arquivo, você pode aplicá-lo aos seus resultados de rastreamento para alterar a exibição.  
  
#### <a name="to-change-the-display-settings"></a>Para alterar as configurações de exibição  
  
1.  Abra um arquivo .XEL para exibir os resultados do rastreamento.  
  
    > [!NOTE]  
    >  Você também pode clicar com o botão direito do mouse no nome da sessão e selecionar **observar dados dinâmicos**.  
  
2.  Na janela de resultados de rastreamento, na barra de ferramentas ou no menu Eventos Estendidos, selecione **Configurações de Vídeo**.  
  
3.  Na lista suspensa, selecione uma das seguintes opções:  
  
    -   **Salvar como**. Salve as colunas e informações de filtro de um resultado de rastreamento em um arquivo .viewsetting.  
  
    -   **Abra**o. Abra um arquivo .viewsetting existente.  
  
    -   **Abra recente**. Abra um arquivo .viewsetting salvo recentemente.  
  
  
