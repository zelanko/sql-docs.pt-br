---
title: 'Tutorial: Adicionar um gráfico de barras ao relatório (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ef72373f91b9104c8ff83f6d1d9b012b283df3d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>Tutorial: Adicionar um gráfico de barras ao relatório (Construtor de Relatórios)
Neste tutorial, você usa um assistente no [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] para criar um gráfico de barras em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . Em seguida, adicione um filtro e aprimore o gráfico. 

Um gráfico de barras exibe os dados de categoria horizontalmente. Ele pode ajudar a:  
  
-   Melhorar a legibilidade de nomes de categorias longos.  
-   Melhorar a capacidade de compreensão de tempos plotados como valores.   
-   Comparar o valor relativo de várias séries.  
  
A ilustração a seguir mostra o gráfico de barras que você criará, com as vendas de 2014 e 2015 dos cinco principais vendedores, das maiores até as menores vendas de 2015.  
  
![report-builder-bar-chart](../reporting-services/media/report-builder-bar-chart.png) 
  
 
> [!NOTE]  
> Neste tutorial, as etapas do assistente são consolidadas em um procedimento. Para obter instruções passo a passo sobre como procurar um servidor de relatório, criar um conjunto de dados e escolher uma fonte de dados, consulte o primeiro tutorial desta série: [Tutorial: Criando um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo estimado para concluir este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Criar um relatório de gráfico no Assistente de Gráfico  
Em que você cria um conjunto de dados inserido, escolhe uma fonte de dados compartilhada e cria um gráfico de barras usando o Assistente de Gráfico.  
  
> [!NOTE]  
> Neste tutorial, como contém os valores de dados, a consulta não precisa de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) por meio do portal da Web do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , do servidor de relatórios no modo integrado do SharePoint ou em seu computador.  
  
     A caixa de diálogo **Guia de Introdução** é exibida.  
  
     ![Introdução ao Construtor de Relatórios](../reporting-services/media/rb-getstarted.png "Introdução ao Construtor de Relatórios")  
  
     Se a caixa de diálogo **Introdução** não estiver visível, clique em **Arquivo** >**Novo**. A maior parte do conteúdo na caixa de diálogo **Novo Relatório ou Conjunto de Dados** é igual àquele encontrado na caixa de diálogo **Introdução** . 
      
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Gráfico**.  
  
4.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados**e em **Avançar**.  
  
5.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou procure o servidor de relatório, selecione uma fonte de dados e clique em **Avançar**. Talvez seja necessário inserir um nome de usuário e uma senha.  
  
    > [!NOTE]  
    > A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
7.  Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2015, CAST(150000. AS money) AS SalesYear2014  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(190000. AS money) AS SalesYear2014  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2015, CAST(195000. AS money) AS SalesYear2014  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(160000. AS money) AS SalesYear2014  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(220000. AS money) AS SalesYear2014  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(215000. AS money) AS SalesYear2014  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2015, CAST(207000. AS money) AS SalesYear2014  
    ```  
  
8.  (Opcional) Clique no botão Executar (**!**) para ver os dados em que o gráfico se baseará.  
  
9. Clique em **Avançar**.  
  
## <a name="ChartType"></a>2. Criar um gráfico de barras  
 
1.  Na página **Escolher um tipo de gráfico** , o gráfico de colunas é o tipo de gráfico padrão.  
  
2.  Clique em **Barra**e em **Avançar**.  
  
    Na página **Organizar campos de gráfico** , há quatro campos no painel **Campos disponíveis** : FirstName, LastName, SalesYear2015 e SalesYear2014.  
  
3.  Arraste LastName para o painel Categorias.  
  
4.  Arraste SalesYear2015 até o painel Valores. SalesYear2015 representa o valor das vendas de cada vendedor no ano de 2015. O painel Valores exibe `[Sum(SalesYear2015)]` porque o gráfico exibe a agregação de cada produto.  
  
5.  Arraste SalesYear2014 até o painel Valores sob SalesYear2015. SalesYear2014 representa o valor das vendas de cada vendedor no ano de 2014.  
  
6.  Clique em **Avançar**.  
  
7.  Clique em **Concluir**.  
  
    O gráfico é adicionado à superfície de design. Observe que o novo gráfico de barras mostra apenas dados representacionais. A legenda indica Sobrenome A, Sobrenome B, etc., em vez de nomes de pessoas, apenas para dar uma ideia da aparência do relatório. 
  
9. Clique no gráfico para exibir suas alças. Arraste o canto inferior direito do gráfico para aumentar o tamanho do gráfico. Observe que a superfície de design fica maior à medida que você arrasta. 
  
10. Clique em **Executar** para visualizar o relatório.  
  
O gráfico de barras exibe as vendas de cada vendedor nos anos de 2014 e 2015. O comprimento da barra corresponde ao total de vendas.  
  
## <a name="AllValues"></a>3. Exibir todos os nomes no eixo vertical  
Por padrão, apenas alguns valores no eixo vertical são exibidos. É possível alterar o gráfico para exibir todas as categorias.  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com o botão direito do mouse no eixo vertical e clique em **Propriedades do Eixo Vertical**.  
  
3.  Em **Alcance e intervalo do eixo**, na caixa **Intervalo** , digite **1**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Clique em **Executar** para visualizar o relatório.  
  
> [!NOTE]  
> Se você não conseguir ler os nomes dos vendedores no eixo vertical, poderá aumentar o tamanho do gráfico ou alterar as opções de formatação dos rótulos do eixo.  
  
### <a name="CategoryExpression"></a>Exibir sobrenome e nome no eixo vertical  
Você pode alterar a expressão de categoria para incluir o sobrenome seguido do nome de cada vendedor.  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes no gráfico para exibir o painel **Dados do Gráfico** .  
  
3.  Na área **Grupos de Categorias** , clique com o botão direito do mouse em [LastName] e clique em **Propriedades do Grupo de Categorias**.  
  
4.  Em Rótulo, clique no botão de expressão (Fx).  
  
5.  Digite a seguinte expressão: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
    Essa expressão concatena o sobrenome, uma vírgula e o nome.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Clique em **Executar** para visualizar o relatório.  
  
Se os nomes não aparecerem ao executar o relatório, você poderá atualizar os dados manualmente. Enquanto estiver no modo de visualização, na guia **Executar** , no grupo **Navegação** , clique em **Atualizar**.  
  
> [!NOTE]  
> Se você não conseguir ler os nomes dos vendedores no eixo vertical, poderá aumentar o tamanho do gráfico ou alterar as opções de formatação dos rótulos do eixo.  
  
## <a name="Sort"></a>4. Alterar a ordem de classificação no eixo vertical  
Quando você classifica dados em um gráfico, está alterando a ordem de valores no eixo de categoria.  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes no gráfico para exibir o painel **Dados do Gráfico** .  
  
3.  Na área **Grupos de Categorias** , clique com o botão direito do mouse em [LastName] e clique em **Propriedades do Grupo de Categorias**.  
  
4.  Clique em **Classificar**. A página **Alterar opções de classificação** exibe uma lista de expressões de classificação. Por padrão, essa lista contém uma expressão de classificação que é igual à expressão do grupo de categorias original.  
  
5.  Em **Classificar por**, clique em **[SalesYear2015]**.  
  
6.  Na lista **Ordem** , selecione **A a Z** para que os nomes sejam exibidos das maiores para as menores vendas de 2015.
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Clique em **Executar** para visualizar o relatório.  
  
Os nomes no eixo horizontal são classificados das maiores para as menores vendas de 2015, com **Zeng** na parte superior.  
  
## <a name="Legend"></a>5. Mover a legenda  
Para melhorar a capacidade de leitura dos valores do gráfico, mova a legenda do gráfico. Por exemplo, em um gráfico de barras no qual as barras são mostradas na horizontal, você pode alterar a posição da legenda para que ela fique acima ou abaixo da área do gráfico. Isso dá mais espaço na horizontal às barras.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>Para exibir a legenda abaixo da área de gráfico de um gráfico de barras  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique com o botão direito do mouse na legenda no gráfico.  
  
3.  Selecione **Propriedades da Legenda**.  
  
4.  Em **Posição da legenda**, selecione uma posição diferente. Por exemplo, defina a posição para a opção da metade inferior.  
  
    Quando a legenda estiver posicionada na parte superior ou inferior de um gráfico, o layout da legenda será alterado de vertical para horizontal. Você pode selecionar um layout diferente na lista suspensa **Layout** .  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="ChartTitle"></a>6. Intitular o gráfico  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Selecione as palavras **Título do Gráfico** na parte superior do gráfico e digite: **Vendas de 2014 e 2015**.  
  
3.  No painel Propriedades, com o título selecionado, defina **Cor** como **Preto** e **Tamanho da Fonte** como **12 pt**. 
  
4.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="Horizontal"></a>7. Formatar e rotular o eixo horizontal  
Por padrão, o eixo horizontal exibe valores em um formato geral que é dimensionado para ajustar o tamanho do gráfico automaticamente. Você pode alterá-lo para o formato de moeda.  
   
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique no eixo horizontal ao longo da parte inferior do gráfico para selecioná-lo.  
  
3.  Na guia **Início** > grupo **Número** > **Moeda**. Os rótulos do eixo horizontal são alterados para moeda.  
  
3.  (Opcional) Remova os dígitos decimais. Próximo ao botão **Moeda** , clique no botão **Diminuir Decimal** duas vezes.  
  
4.  Clique com o botão direito do mouse no eixo horizontal e clique em **Propriedades do Eixo Horizontal**.  
  
5.  Na guia **Número** , selecione **Mostrar valores em Milhares**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

8.  Clique com o botão direito do mouse no eixo horizontal e selecione **Mostrar Título do Eixo**.
  
7.  Na caixa **Título do Eixo** , digite **Vendas em milhares** e pressione Enter.  

    >**Observação:** enquanto estiver digitando, a caixa Título do Eixo parece estar no eixo vertical. Mas quando você pressiona Enter, ele vai para o eixo horizontal.
  
9. Clique em **Executar** para visualizar o relatório.  
  
O relatório exibe o valor das vendas no eixo horizontal como moeda em milhares, sem dígitos decimais.  
  
## <a name="Filter"></a>8. Adicionar um filtro para exibir os cinco valores principais  
Você pode adicionar um filtro ao gráfico para especificar os dados do conjunto de dados a serem incluídos ou excluídos no gráfico.   
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique duas vezes no gráfico para exibir o painel **Dados do Gráfico** .  
  
3.  Na área **Grupos de Categorias** , clique com o botão direito do mouse no campo [LastName] e clique em **Propriedades do Grupo de Categorias**.  
  
4.  Clique em **Filtros**. A página **Alterar filtros** pode exibir uma lista de expressões de filtro. Por padrão, essa lista está vazia.  
  
5.  Clique em **Adicionar**. Um novo filtro em branco é exibido.  
  
6.  Em **Expressão**, digite **[Sum(SalesYear2015)]**. Esse procedimento cria a expressão subjacente `=Sum(Fields!SalesYear2015.Value)`, que poderá ser vista se você clicar no botão **fx** .  
  
7.  Verifique se o tipo de dados é **Text**.  
  
8.  Em **Operador**, selecione **N Superior** na lista suspensa.  
  
9. Em **Valor**, digite a seguinte expressão: **=5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Clique em **Executar** para visualizar o relatório.  
  
Se os resultados não forem filtrados ao executar o relatório, você poderá atualizar os dados manualmente. Na guia **Executar** do grupo **Navegação** , clique em **Atualizar**.  
  
O gráfico mostra os cinco primeiros nomes de vendedores dos dados de vendas de 2015.  
  
## <a name="Title"></a>9. Adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Gráfico de Barras de Vendas**, pressione ENTER e digite **Cinco Primeiros Vendedores de 2015**, como neste exemplo:  
  
    **Gráfico de Barras de Vendas**  
  
    **Cinco Primeiros Vendedores de 2015**  
  
3.  Selecione **Gráfico de Barras de Vendas**e clique no botão **Negrito** .  
  
4.  Selecione **Cinco Primeiros Vendedores de 2015**e, na seção **Fonte** da guia **Início** , defina o tamanho da fonte como **10**.  
  
5.  (Opcional) Talvez seja necessário aumentar a altura da caixa de texto Título e mover para baixo a parte superior do gráfico de barras, para acomodar as duas linhas de texto.  
  
    Esse título aparecerá na parte superior do relatório. Quando não houver nenhum cabeçalho de página definido, os itens na parte superior do corpo do relatório serão equivalentes a um cabeçalho de relatório.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="Save"></a>10. Salvar o relatório  
  
1.  Alterne para a exibição de design de relatório.  
  
2.  Clique em **Arquivo** > **Salvar Como**.  
  
3.  Em **Nome**, digite **Gráfico de Barras de Vendas**.  

    Você pode salvá-lo no computador ou no servidor de relatório.
  
4.  Clique em **Salvar**.   
  
## <a name="next-steps"></a>Next Steps  
Você concluiu com êxito o tutorial Adicionando um gráfico de barras seu relatório. Para saber mais sobre gráficos, consulte [Gráficos](../reporting-services/report-design/charts-report-builder-and-ssrs.md) e [Gráficos de Barras](../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
[Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md)  
[Construtor de Relatórios no SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

