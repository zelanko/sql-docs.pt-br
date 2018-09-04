---
title: Adicionar classificação interativa a uma tabela ou matriz (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
f1_keywords:
- "10121"
- sql13.rtp.rptdesigner.textboxproperties.intrctvsort.f1
ms.assetid: 05819637-729b-4cf6-82de-91a99f184ec6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a92f326fd1933fdc6df2adb1add9db11e92b6a19
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43269028"
---
# <a name="add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs"></a>Adicionar classificação interativa a uma tabela ou matriz (Construtor de Relatórios e SSRS)
  Adicione botões de classificação interativa para permitir que os usuários alterem a ordem de classificação de linhas e colunas em tabelas e matrizes. Esse recurso só é suportado em formatos de renderização que dão suporte à interação do usuário, como o HTML.  
  
 Ao criar um botão de classificação interativa, você deve especificar o que classificar, pelo que classificar e o escopo ao qual aplicar a classificação. Por exemplo, você pode classificar linhas de detalhes pelo sobrenome do cliente, valores do grupo de subcategorias dentro de um grupo de categorias por vendas ou valores de grupos de categorias e subcategorias combinados por totais.  
  
 Quando você exibe o relatório, colunas que suportam a classificação interativa têm ícones de seta que são alteradas para indicar a ordem de classificação. Na primeira vez que você clica em um botão de classificação interativa, os itens são classificados em ordem crescente. Cliques subsequentes alternam a ordem de classificação entre crescente e decrescente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="BackToTop"></a> Neste artigo  
 [Classificando linhas de detalhes para um tabela sem grupos](#SortingDetailRows)  
  
 [Classificando um grupo de linhas pai de nível superior para um tabela ou matriz](#SortingTopLevelParent)  
  
 [Classificando grupos filho ou linhas de detalhes de um grupo](#SortingChildGroups)  
  
 [Classificando linhas com base em uma expressão de grupo complexa](#SortingMultipleRowGroups)  
  
 [Sincronizando a ordem de classificação para várias regiões de dados](#SynchronizingSortOrder)  
  
##  <a name="SortingDetailRows"></a> Classificando linhas de detalhes para um tabela sem grupos  
 Adicione um botão de classificação interativa a um cabeçalho de coluna para permitir que um usuário clique no cabeçalho da coluna e classifique as linhas de detalhes em uma tabela pelo valor exibido naquela coluna.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-the-table-by-value"></a>Para adicionar um botão de classificação interativa a um cabeçalho de coluna para classificar a tabela pelo valor  
  
1.  No modo de exibição de Design do relatório, em uma tabela sem grupos, clique com o botão direito do mouse na caixa de texto no cabeçalho da coluna ao qual você deseja adicionar um botão de classificação interativa e clique em **Propriedades da Caixa de Texto**.  
  
2.  Clique em **Classificação Interativa**.  
  
3.  Selecione **Habilitar classificação interativa nesta caixa de texto**.  
  
4.  Em **Escolher o que classificar**, clique em **Linhas de detalhes**.  
  
5.  Em **Classificar por**, especifique uma expressão de classificação. Na lista suspensa, selecione o campo que corresponde à coluna para a qual você deseja definir uma ação de classificação (por exemplo, para um título de coluna denominado "Título", escolha `[Title]`). É necessário especificar uma expressão de classificação.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Repita as etapas 1 a 6 para cada coluna para a qual você deseja adicionar um botão de classificação interativa.  
  
 Para verificar a ação de classificação, clique em **Executar** para visualizar o relatório e clique nos botões de classificação interativa.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="SortingTopLevelParent"></a> Classificando um grupo de linhas pai de nível superior para um tabela ou matriz  
 Adicione um botão de classificação interativa a um cabeçalho de coluna para permitir que um usuário clique no cabeçalho da coluna e classifique as linhas do grupo pai em uma tabela ou matriz pelo valor exibido naquela coluna. A ordem dos grupos filho permanece inalterada.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-groups"></a>Para adicionar um botão de classificação interativa a um cabeçalho de coluna para classificar grupos  
  
1.  Em uma tabela ou matriz, no modo de exibição de Design do relatório, clique com o botão direito do mouse na caixa de texto no cabeçalho da coluna do grupo ao qual você deseja adicionar um botão de classificação interativa e clique em **Propriedades da Caixa de Texto**.  
  
2.  Clique em **Classificação Interativa**.  
  
3.  Selecione **Habilitar classificação interativa nesta caixa de texto**.  
  
4.  Em **Escolher o que classificar**, clique em **Grupos**.  
  
5.  Na lista suspensa, selecione o nome do grupo que você está classificando. Para grupos baseados em expressões de grupo simples, o valor de **Classificar por** é populado com a expressão de grupo.  
  
    > [!NOTE]  
    >  Para expressões de grupo complexas, defina manualmente a expressão **Classificar por** com o mesmo valor da expressão de grupo.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para verificar a ação de classificação, clique em **Executar** para visualizar o relatório e clique nos botões de classificação interativa.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="SortingChildGroups"></a> Classificando grupos filho ou linhas de detalhes de um grupo  
 Adicione um botão de classificação interativa a uma linha de cabeçalho de grupo para permitir que os usuários classifiquem os valores de um grupo filho de um grupo pai ou classifiquem as linhas de detalhes do grupo filho interno.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-text-box-in-a-group-row-header-to-sort-child-groups-or-detail-rows"></a>Para adicionar um botão de classificação interativa a uma caixa de texto em um cabeçalho de linha de grupo para classificar grupos filho ou linhas de detalhes  
  
1.  No modo de exibição de Design do relatório, clique com o botão direito do mouse na caixa de texto na linha do cabeçalho do grupo ao qual você deseja adicionar um botão de classificação interativa e clique em **Propriedades da Caixa de Texto**.  
  
2.  Clique em **Classificação Interativa**.  
  
3.  Selecione **Habilitar classificação interativa nesta caixa de texto**.  
  
4.  Em **Escolher o que classificar**, clique em uma das seguintes opções:  
  
    -   **Detalhes** Clique em **Detalhes** para classificar as linhas de detalhes. Na lista suspensa, selecione o campo pelo qual classificar. Para esta opção, você deve especificar o valor pelo qual classificar.  
  
    -   **Grupos** Clique em **Grupos** para classificar os valores do grupo filho. Para essa opção, a expressão **Classificar por** é preenchida automaticamente da expressão de grupo.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para verificar a ação de classificação, clique em **Executar** para visualizar o relatório e clique nos botões de classificação interativa.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="SortingMultipleRowGroups"></a> Classificando linhas com base em uma expressão de grupo complexa  
 Adicione um botão de classificação interativa a um cabeçalho de coluna para permitir que um usuário clique no cabeçalho da coluna e classifique os grupos pai e filho combinados. Para obter esse efeito, é necessário alterar a expressão de grupo para que seja uma composição dos dois grupos. Por exemplo, suponha que uma matriz exibe totais de inventário de uma loja de itens agrupados por cor e tamanho. Para classificar as linhas com base na combinação de cor e tamanho, em vez de ter um grupo separado para cor e outro para tamanho, é possível definir um grupo com base na combinação de cor e tamanho. Para obter mais informações sobre como definir expressões de grupo, consulte [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
 No procedimento seguinte, condições especificam áreas da região de dados Tablix. Para obter mais informações, consulte [Áreas da região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 Normalmente, ao classificar linhas com base em vários grupos, você deseja ver os totais das linhas classificadas, independentemente dos grupos de colunas. Neste procedimento, nenhum grupo de colunas é usado. Você começa adicionando uma matriz e removendo o grupo de colunas padrão. Como alternativa, você pode começar adicionando uma tabela e removendo o grupo de detalhes.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-multiple-groups"></a>Para adicionar um botão de classificação interativa a um cabeçalho de coluna para classificar vários grupos  
  
1.  Na exibição de design do relatório, adicione uma matriz.  
  
2.  Arraste um campo numérico até a célula de dados para vincular o conjunto de dados à matriz.  
  
     Em seguida, crie um grupo com uma expressão de grupo que especifique vários campos e um cabeçalho de grupo a ser usado para exibir valores do grupo.  
  
3.  Verifique se a matriz está selecionada na superfície de design. O painel Agrupamento exibe o grupo de linhas e colunas padrão.  
  
4.  No painel Grupos de Linhas, clique com o botão direito do mouse no grupo de linhas padrão e clique em **Editar Grupo**. A caixa de diálogo **Propriedades do Grupo** é aberta.  
  
5.  Em **Nome**, substitua o nome padrão por um nome que especifique os vários grupos pelos quais você deseja agrupar.  
  
6.  Em **Expressões de grupo**, em **Agrupar em**, clique no botão Expressão (**fx**) para abrir a caixa de diálogo **Expressão** .  
  
7.  Digite a expressão que especifica todos os campos pelos quais você deseja agrupar. Por exemplo, a expressão de grupo a seguir combina um campo denominado Cor e um campo denominado Tamanho: `=Fields!Color.Value & Fields!Size.Value`.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Você definiu o grupo agora. Em seguida, arraste os campos a serem exibidos para a área do corpo do tablix da matriz. Adicione os campos escolhidos para agrupamento na etapa 7 à área do corpo do tablix, cada um em sua própria coluna.  
  
     Para este cenário, a primeira coluna na área de grupos de linhas do tablix não é necessária. Para excluir a coluna, clique com o botão direito do mouse no cabeçalho da coluna e clique em **Excluir Colunas**. Uma caixa de diálogo pergunta se os grupos associados devem ser excluídos. Clique em **Não**. A área do grupo de linhas é excluída e só a área do corpo do Tablix permanece.  
  
     Em seguida, você removerá o grupo de colunas padrão.  
  
9. No painel Grupos de Colunas, clique com o botão direito do mouse no grupo de colunas padrão e clique em **Excluir Grupo**. Uma caixa de diálogo pergunta se o grupo e as linhas e colunas relacionadas ou somente o grupo deve ser excluído. Clique em **Excluir somente grupo**. O grupo de colunas e a área do grupo de colunas são excluídos. Somente a área do corpo do Tablix permanece.  
  
     Em seguida, você adicionará um botão de classificação interativa à caixa de texto que se transpõe a matriz.  
  
10. Clique na caixa de texto na primeira linha e em **Propriedades da Caixa de Texto**.  
  
11. Clique em **Classificação Interativa**.  
  
12. Selecione **Habilitar classificação interativa nesta caixa de texto**.  
  
13. Em **Escolher o que classificar**, clique em **Grupos**.  
  
14. Na lista suspensa, selecione o nome do grupo criado na etapa 5. A expressão de grupo é copiada automaticamente na caixa de texto **Classificar por** .  
  
15. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Você adicionou o botão de classificação à caixa de texto.  
  
16. (Opcional) Você pode suprimir valores duplicados nas colunas que exibem valores de grupo. Na superfície de design de relatório, clique na caixa de texto que exibe o valor do qual você deseja ocultar valores repetidos. No painel Propriedades, role até **HideDuplicates**e, na lista suspensa, selecione o nome do conjunto de dados que está vinculado a esta matriz.  
  
 Para verificar a ação de classificação, clique em **Executar** para visualizar o relatório e clique no botão de classificação interativa. A matriz é classificada pelos valores combinados da expressão de grupo, embora cada valor individual seja exibido em sua própria coluna.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="SynchronizingSortOrder"></a> Sincronizando a ordem de classificação para várias regiões de dados  
 Adicione um botão de classificação interativa que permita que um usuário clique em um botão de classificação e classifique várias regiões de dados. Ao criar um botão de classificação interativa, é possível especificar se a classificação deve ser sincronizada para várias regiões de dados com base no mesmo conjunto de dados do relatório. Por exemplo, um relatório poder incluir uma matriz e um gráfico que exibem os dados graficamente. Quando um usuário altera a ordem de classificação das linhas na matriz, o gráfico exibe a mesma ordem de classificação automaticamente.  
  
 Para sincronizar a ordem de classificação, você deve usar expressões de classificação idênticas para as regiões de dados ou grupos a serem classificados e definir o escopo da classificação para que seja um ancestral mútuo das duas regiões de dados. O ancestral mútuo pode ser o conjunto de dados ao qual as duas regiões de dados estão vinculadas ou uma região contentora de dados dentro da qual as duas regiões de dados aparecem. Por exemplo, assuma que um relatório tem uma matriz e um gráfico que exibem dados do mesmo conjunto de dados e que estão contidos em uma lista. Para sincronizar a ação de classificação, você deve especificar a classificação interativa em uma coluna na matriz e definir o escopo para a lista. Quando o usuário classifica a matriz, o gráfico também é classificado.  
  
#### <a name="to-synchronize-sort-order-with-a-chart-for-an-interactive-sort-button-on-a-matrix-data-region"></a>Para sincronizar a ordem de classificação com um gráfico para um botão de classificação interativa em uma região de dados da matriz  
  
1.  Na exibição de design do relatório, adicione uma matriz ao relatório.  
  
2.  Adicione um campo de conjunto de dados numérico à célula de dados da matriz, por exemplo, um campo que represente quantidade ou vendas.  
  
3.  Defina um grupo de linhas. Por padrão, a ordem de classificação do grupo é definida como a mesma expressão que a expressão do grupo.  
  
4.  Adicione um gráfico ao relatório, por exemplo, um gráfico de pizza.  
  
5.  Arraste o campo escolhido na etapa 2 para a área **Valor** do painel **Dados do Gráfico** .  
  
6.  Arraste o campo escolhido para agrupamento para a área **Grupos de Categorias** .  
  
     A expressão do grupo de linhas da matriz e o grupo de categorias do gráfico devem ser idênticos.  
  
7.  Clique com o botão direito do mouse no grupo de categorias e clique em **Propriedades do Grupo de Categorias**.  
  
8.  Clique em **Classificar**.  
  
9. Clique em **Adicionar**. Uma nova linha de classificação é adicionada à grade de opções de classificação.  
  
10. Em Classificar por, na lista suspensa, escolha o mesmo campo escolhido na etapa 6 para agrupamento.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
12. Na matriz, clique com o botão direito do mouse no cabeçalho da coluna ao qual você deseja adicionar um botão de classificação interativa e clique em **Propriedades da Caixa de Texto**.  
  
13. Clique em **Classificação Interativa**.  
  
14. Selecione **Habilitar classificação interativa nesta caixa de texto**.  
  
15. Em **Escolher o que classificar**, clique em **Grupos**.  
  
16. Na lista suspensa, sob **Grupos**, selecione o nome do grupo que você está classificando. A expressão desse grupo é definida automaticamente para definir o valor de **Classificar por** .  
  
17. Selecione **Aplicar esta classificação também a outros grupos e regiões de dados em**. Na caixa de texto, digite o nome do conjunto de dados, por exemplo, "SalesData".  
  
18. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para verificar a ação de classificação, clique em **Executar** para visualizar o relatório e clique no botão de classificação interativa. A matriz é classificada pelos valores combinados da expressão de grupo, embora cada valor individual seja exibido em sua própria coluna.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
## <a name="see-also"></a>Consulte Também  
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Classificação interativa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)   
 [Classificar dados em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Explorando a flexibilidade de uma região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)  
  
  
