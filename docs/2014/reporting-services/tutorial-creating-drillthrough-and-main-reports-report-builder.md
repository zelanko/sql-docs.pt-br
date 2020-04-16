---
title: 'Tutorial: Criando relatórios principais e de detalhamento (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7168c8d3-cef5-4c4a-a0bf-fff1ac5b8b71
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c9fe67c3fe0656924ea8e53c4c937a99b588b46b
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388493"
---
# <a name="tutorial-creating-drillthrough-and-main-reports-report-builder"></a>Tutorial: criando relatórios principais e de detalhamento (Construtor de Relatórios)
  Este tutorial ensina como criar dois tipos de relatório: um relatório detalhado e um relatório principal. Os dados de vendas de exemplo usados nestes relatórios são recuperados de um cubo do Analysis Services. A ilustração a seguir mostra os relatórios que você criará.  
  
 ![rs_DrillthroughCubeTutorial](../../2014/tutorials/media/rs-drillthroughcubetutorial.gif "rs_DrillthroughCubeTutorial")  
  
 A ilustração a seguir mostra como o valor do campo, Jogos e Brinquedos, no relatório principal é exibido no título do relatório de perfuração. Os dados no detalhamento pertencem à categoria de produto Games and Toys.  
  
 ![rs_DrillthroughCubeTutorialParmExpr](../../2014/tutorials/media/rs-drillthroughcubetutorialparmexpr.gif "rs_DrillthroughCubeTutorialParmExpr")  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 **No relatório detalhado você aprenderá como:**  
  
1.  [Criar um relatório de matriz de detalhamento e um conjunto de dados no Assistente de Tabela ou Matriz](#DMatrixAndDataset)  
  
    1.  [Especificar uma conexão de dados](#DConnection)  
  
    2.  [Criar uma consulta MDX](#DMDXQuery)  
  
    3.  [Organizar dados em estilo de grupos](#DLayout)  
  
    4.  [Adicionar subtotais e totais](#DTotals)  
  
    5.  [Escolha um estilo](#DStyle)  
  
2.  [Formatar dados como moeda](#DFormat)  
  
3.  [Adicionar colunas para mostrar valores de vendas em sparklines](#DSparkline)  
  
4.  [Adicionar título de relatório com nome da categoria do produto](#DReportTitle)  
  
5.  [Atualizar propriedades de parâmetros](#DParameter)  
  
6.  [Salvar o relatório em uma biblioteca do SharePoint](#DSave)  
  
 **No relatório principal, você aprenderá como:**  
  
1.  [Criar o relatório de matriz principal e o conjunto de dados no Assistente de Tabela ou Matriz](#MMatrixAndDataset)  
  
    1.  [Especificar uma conexão de dados](#MConnection)  
  
    2.  [Criar uma consulta MDX](#MMDXQuery)  
  
    3.  [Organizar dados em grupos](#MLayout)  
  
    4.  [Adicionar subtotais e totais](#MTotals)  
  
    5.  [Escolha um estilo](#MStyle)  
  
2.  [Remover a linha de total geral](#MGrandTotal)  
  
3.  [Configurar ação de caixa de texto para detalhamento](#MDrillthrough)  
  
4.  [Substituir valores numéricos por indicadores](#MIndicators)  
  
5.  [Atualizar propriedades de parâmetros](#MParameter)  
  
6.  [Adicionar um título de relatório](#MTitle)  
  
7.  [Salvar o relatório em uma biblioteca do SharePoint](#MSave)  
  
8.  [Executar os relatórios principal e de detalhamento](#MRunReports)  
  
 Tempo estimado para concluir este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Este tutorial exige acesso ao cubo Vendas da Contoso. Esse requisito se aplica aos relatórios detalhados e principal. Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-drillthrough-report-from-the-table-or-matrix-wizard"></a><a name="DMatrixAndDataset"></a>1. Crie um relatório de perfuração do Assistente de Tabela ou Matriz  
 Na caixa de diálogo Introdução , crie um relatório de matriz por meio do **Assistente de Tabela ou Matriz**. Há dois modos disponíveis no assistente: design de relatório e design de conjunto de dados compartilhado. Neste tutorial, você usará o modo design de relatório.  
  
#### <a name="to-create-a-new-report"></a>Para criar um novo relatório  
  
1.  Clique **em Iniciar,** aponte [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] para **Programas,** aponte para **''''''''''''Iniciar'.** **Report Builder**  
  
     A caixa de diálogo **Guia de Introdução** é aberta. Se ele não aparecer, a partir do botão **'''Construtor de relatórios',** clique em **Nova**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, verifique se a opção **Assistente de Tabela ou Matriz** está selecionada.  
  
##  <a name="1a-specify-a-data-connection"></a><a name="DConnection"></a>1a. Especificar uma conexão de dados  
 Uma conexão de dados contém as informações necessárias para estabelecer conexões com uma fonte de dados externa, como um cubo do Analysis Services ou um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para especificar uma conexão de dados, você pode usar uma fonte de dados compartilhada do servidor de relatório ou criar uma fonte de dados inserida que será usada somente neste relatório. Neste tutorial, você usará uma fonte de dados inserida. Para saber mais sobre como usar uma fonte de dados compartilhada, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
#### <a name="to-create-an-embedded-data-source"></a>Para criar uma fonte de dados inserida  
  
1.  Na página **Escolher um conjunto de dados** , selecione **Criar um conjunto de dados**e clique em **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
2.  Clique em **Novo**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
3.  Em **Nome**, digite **Detalhes de Vendas Online e do Revendedor** como o nome da fonte de dados.  
  
4.  Em **Selecione um tipo de conexão**, selecione **Microsoft SQL Server Analysis Services**e clique em **Compilar**.  
  
5.  Em **Fonte de dados**, verifique se a fonte de dados é **Microsoft SQL Server Analysis Services (AdomdClient)**.  
  
6.  Em **Nome do servidor**, digite o nome de um servidor em que uma instância do Analysis Services está instalada.  
  
7.  Em **Selecionar ou inserir um nome de banco de dados**, selecione o cubo Contoso.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Verifique se **Cadeia de conexão** contém a seguinte sintaxe:  
  
    ```  
    Data Source=<servername>; Initial Catalog = Contoso  
    ```  
  
     O `<servername>` é o nome de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o Analysis Services instalado.  
  
10. Clique em **Tipo de credenciais**.  
  
    > [!NOTE]  
    >  Dependendo de como as permissões estão configuradas na fonte de dados, poderá ser necessário alterar as opções de autenticação padrão. Para obter mais informações, consulte [Segurança &#40;Construtor de Relatórios&#41;](report-builder/security-report-builder.md).  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     A página **Escolher uma conexão com uma fonte de dados** é exibida.  
  
12. Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**.  
  
     A **mensagem Conexão criada** aparece com sucesso.  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
14. Clique em **Próximo**.  
  
##  <a name="1b-create-an-mdx-query"></a><a name="DMDXQuery"></a>1b. Criar uma consulta MDX  
 Em um relatório, é possível usar um conjunto de dados compartilhado que tenha uma consulta predefinida. Se preferir, crie um conjunto de dados inserido para ser usado somente em seu relatório. Neste tutorial, você criará um conjunto de dados inserido.  
  
#### <a name="to-create-query-filters"></a>Para criar filtros de consulta  
  
1.  Na **página Projetar uma consulta,** no painel Metadados, clique no botão **(...)**.  
  
2.  Na caixa de diálogo **Seleção de Cubo** , clique em Vendas e em **OK**.  
  
    > [!TIP]  
    >  Se não desejar criar a consulta MDX manualmente, clique no ícone ![Alternar para modo de Design](../analysis-services/media/rsqdicon-designmode.gif "Alterna para o modo de design"), ative/desative o designer de consultas para o modo de Consulta, cole o MDX concluído no designer de consultas e vá para a etapa 6 em [Para criar o conjunto de dados](#DSkip).  
  
    ```  
    SELECT NON EMPTY { [Measures].[Sales Amount], [Measures].[Sales Return Amount] } ON COLUMNS, NON EMPTY { ([Channel].[Channel Name].[Channel Name].ALLMEMBERS * [Product].[Product Category Name].[Product Category Name].ALLMEMBERS * [Product].[Product Subcategory Name].[Product Subcategory Name].ALLMEMBERS ) } DIMENSION PROPERTIES MEMBER_CAPTION, MEMBER_UNIQUE_NAME ON ROWS FROM ( SELECT ( { [Date].[Calendar Year].&[2009] } ) ON COLUMNS FROM ( SELECT ( { [Sales Territory].[Sales Territory Group].&[North America] } ) ON COLUMNS FROM ( SELECT ( STRTOSET(@ProductProductCategoryName, CONSTRAINED) ) ON COLUMNS FROM ( SELECT ( { [Channel].[Channel Name].&[2], [Channel].[Channel Name].&[4] } ) ON COLUMNS FROM [Sales])))) WHERE ( [Sales Territory].[Sales Territory Group].&[North America], [Date].[Calendar Year].&[2009] ) CELL PROPERTIES VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
    ```  
  
3.  No painel Grupo de Medidas, expanda Canal e arraste Nome do Canal até a coluna **Hierarquia** no painel de filtro.  
  
     O nome da dimensão, Canal, é adicionado automaticamente à coluna **Dimensão** . Não altere as colunas **Dimensão** ou **Operador** .  
  
4.  Para abrir a lista **Expressão de Filtro** , clique na seta para baixo na coluna **Expressão de Filtro** .  
  
5.  Na lista de expressões de filtro, expanda **Todo o Canal**, clique em **Online**, em **Revendedor**e em **OK**.  
  
     A consulta agora inclui um filtro para incluir apenas estes canais: Online e Revendedor.  
  
6.  Expanda a dimensão Região de Vendas e arraste Grupo da Região de Vendas até a coluna **Hierarquia** (abaixo de **Nome do Canal**).  
  
7.  Abra a lista **Expressão de Filtro** , expanda **Toda a Região de Vendas**, clique em **América do Norte**e em **OK**.  
  
     A consulta agora tem um filtro para incluir apenas vendas na América do Norte.  
  
8.  No painel Grupo de Medidas, expanda Data e arraste Ano Civil até a coluna **Hierarquia** no painel de filtro.  
  
     O nome da dimensão, Data, é adicionado automaticamente à coluna **Dimensão** . Não altere as colunas **Dimensão** ou **Operador** .  
  
9. Para abrir a lista **Expressão de Filtro** , clique na seta para baixo na coluna **Expressão de Filtro** .  
  
10. Na lista de expressões de filtro, expanda **Toda a Data**, clique em **Ano 2009**e clique em **OK**.  
  
     A consulta agora inclui um filtro para incluir apenas o ano calendário 2009.  
  
#### <a name="to-create-the-parameter"></a>Para criar o parâmetro  
  
1.  Expanda a dimensão Produto e arraste o membro Nome da Categoria do Produto até a coluna **Hierarquia** abaixo de **Ano Civil**.  
  
2.  Abra a lista **Expressão de Filtro** , clique em **Todos os Produtos**e em **OK**.  
  
3.  Clique na caixa de seleção **Parâmetro** . A consulta agora inclui o parâmetro ProductProductCategoryName.  
  
    > [!NOTE]  
    >  O parâmetro contém os nomes das categorias de produto. Quando você clica no nome de uma categoria de produto no relatório principal, o nome é passado para o relatório detalhado por meio desse parâmetro.  
  
###  <a name="to-create-the-dataset"></a><a name="DSkip"></a>Para criar o conjunto de dados  
  
1.  Na dimensão Canal, arraste Nome do Canal até o painel de dados.  
  
2.  Na dimensão Produto, arraste Nome da Categoria do Produto até o painel de dados e coloque-o à direita de Nome do Canal.  
  
3.  Na dimensão Produto, arraste Nome da Subcategoria do Produto até o painel de dados e coloque-o à direita de Nome da Categoria do Produto.  
  
4.  No painel Metadados, expanda **Medida**e Vendas.  
  
5.  Arraste a medida Valor das Vendas até o painel de dados e coloque-a à direita de Nome da Subcategoria do Produto.  
  
6.  Na barra de ferramentas do designer de consulta, clique **em Executar (!)**.  
  
7.  Clique em **Próximo**.  
  
##  <a name="1c-organize-data-into-groups"></a><a name="DLayout"></a>1c. Organizar dados em grupos  
 Quando você seleciona os campos nos quais agrupar os dados, cria uma matriz com linhas e colunas que exibe dados detalhados e dados agregados.  
  
#### <a name="to-organize-data-into-groups"></a>Para organizar dados em grupos  
  
1.  Para mudar para o modo design, clique em **Design**.  
  
2.  Na página **Organizar campos** , arraste Product_Subcategory_Name até **Grupos de linhas**.  
  
    > [!NOTE]  
    >  Os espaços nos nomes são substituídos por sublinhados (_). Por exemplo, Nome da Categoria do Produto é Product_Category_Name.  
  
3.  Arraste Channel_Name até **Grupos de colunas**.  
  
4.  Arraste Sales_Amount até **Valores**.  
  
     Sales_Amount é agregado automaticamente pela função Sum, a agregação padrão para campos numéricos. O valor é `[Sum(Sales_Amount)]`.  
  
     Para exibir as outras funções de agregação disponíveis, abra a lista suspensa (não altere a função de agregação).  
  
5.  Arraste Sales_Return_Amount até **Valores**e coloque-o abaixo de `[Sum(Sales_Amount)]`.  
  
     As etapas 4 e 5 especificam os dados a serem exibidos na matriz.  
  
6.  Clique em **Próximo**.  
  
##  <a name="1d-add-subtotals-and-totals"></a><a name="DTotals"></a>1d. Adicionar subtotais e totais  
 Depois de criar grupos, é possível adicionar e formatar linhas onde os valores de agregação dos campos serão exibidos. Também é possível escolher mostrar todos os dados ou permitir que um usuário expanda e recolha dados agrupados de forma interativa.  
  
#### <a name="to-add-subtotals-and-totals"></a>Para adicionar subtotais e totais  
  
1.  Na **página Escolher o layout,** em **Opções,** verifique se **os subtotais e totais de exibição estão selecionados.**  
  
     O painel Visualizar do assistente exibe uma matriz com quatro linhas.  
  
2.  Clique em **Próximo**.  
  
##  <a name="1e-choose-a-style"></a><a name="DStyle"></a>1e. Escolha um estilo  
 Um estilo especifica um estilo de fonte, um conjunto de cores e um estilo de borda.  
  
#### <a name="to-specify-a-style"></a>Para especificar um estilo  
  
1.  Na página **Escolha um Estilo,** no painel Estilos, selecione Ardósia.  
  
2.  Clique em **Concluir**.  
  
     A tabela é adicionada à superfície de design.  
  
3.  Para visualizar o relatório, clique em **Executar (!)**.  
  
##  <a name="2-format-data-as-currency"></a><a name="DFormat"></a>2. Formato de dados como moeda  
 Aplique a formatação de moeda aos campos de valor de vendas no relatório detalhado.  
  
#### <a name="to-format-data-as-currency"></a>Para formatar dados como moeda  
  
1.  Para mudar para o modo design, clique em **Design**.  
  
2.  Para selecionar e formatar várias células de uma vez, pressione a tecla Ctrl e selecione as células que contêm os dados de vendas numéricos.  
  
3.  Na guia **Início** , no grupo **Número** , clique em **Moeda**.  
  
##  <a name="3-add-columns-to-show-sales-values-in-sparklines"></a><a name="DSparkline"></a>3. Adicionar colunas para mostrar valores de vendas em sparklines  
 Em vez de mostrar vendas e devoluções de vendas como valores de moeda, o relatório mostra os valores em um minigráfico.  
  
#### <a name="to-add-sparklines-to-columns"></a>Para adicionar minigráficos a colunas  
  
1.  Para mudar para o modo design, clique em **Design**.  
  
2.  No grupo Total da matriz, clique com o botão direito do mouse na coluna **Valor das Vendas** , clique em **Inserir Coluna**e em **Direita**.  
  
     Uma coluna vazia é adicionada à direita de **Valor das Vendas**.  
  
3.  Na faixa de opções, clique em **Retângulo**e clique na célula vazia à direita da célula `[Sum(Sales_Amount)]` no grupo de linhas [Product_Subcategory].  
  
4.  Na faixa de opções, clique no ícone **Minigráfico** e clique na célula em que o retângulo foi adicionado.  
  
5.  Na caixa de diálogo **Selecionar Tipo de Minigráfico** , verifique se o tipo **Coluna** está selecionado.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Clique com o botão direito do mouse no minigráfico.  
  
8.  No painel Dados do Gráfico, clique no ícone **Adicionar campo** e em Sales_Amount.  
  
9. Clique com o botão direito do mouse na coluna `Sales_Return_Amount` e adicione uma coluna à direita dessa coluna.  
  
10. Repita as etapas 2 a 6.  
  
11. Clique com o botão direito do mouse no minigráfico.  
  
12. No painel Dados do Gráfico, clique no ícone **Adicionar campo** e em Sales_Return_Amount.  
  
13. Para visualizar o relatório, clique em **Executar**.  
  
##  <a name="4-add-report-title-with-product-category-name"></a><a name="DReportTitle"></a>4. Adicionar título de relatório com nome da categoria do produto  
 Um título é exibido na parte superior do relatório. É possível colocar o título em um cabeçalho do relatório ou, se o relatório não usar um cabeçalho, em uma caixa de texto na parte superior do corpo do relatório. Neste tutorial, você usará a caixa de texto colocada automaticamente na parte superior do corpo do relatório.  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Para mudar para o modo design, clique em **Design**.  
  
2.  Na superfície de design, clique em **Clique para adicionar título**.  
  
3.  Digite **Vendas e Devoluções por Categoria:**.  
  
4.  Clique com o botão direito do mouse em **Criar Espaço Reservado**.  
  
5.  Clique no botão **(fx)** à direita da lista **Valor** .  
  
6.  Na caixa de diálogo **Expressão** , no painel Categoria, clique em **Conjunto de Dados**e, na lista **Valores** , clique duas vezes em `First(Product_Category_Name)`.  
  
     A caixa **Expressão** contém a seguinte expressão:  
  
    ```  
    =First(Fields!Product_Category_Name.Value, "DataSet1")  
    ```  
  
7.  Para visualizar o relatório, clique em **Executar**.  
  
 O título do relatório inclui o nome da primeira categoria de produto. Posteriormente, depois que você executar esse relatório como um relatório detalhado, o nome da categoria do produto será alterado dinamicamente para refletir o nome da categoria do produto que foi clicada no relatório principal.  
  
##  <a name="5-update-parameter-properties"></a><a name="DParameter"></a>5. Atualizar propriedades do parâmetro  
 Por padrão, os parâmetros estão visíveis, o que não é apropriado para este relatório. Você atualizará as propriedades dos parâmetros do relatório detalhado.  
  
#### <a name="to-hide-a-parameter"></a>Para ocultar um parâmetro  
  
1.  No painel Dados do Relatório, expanda **Parâmetros**.  
  
2.  Clique com \@o botão direito do mouse ProductProductCategoryName e clique em **Propriedades de parâmetro .**  
  
    > [!NOTE]  
    >  O caractere \@ próximo ao nome indica que este é um parâmetro.  
  
3.  Na guia **Geral** , clique em **Oculto**.  
  
4.  Na caixa **Aviso** , digite **Categoria do Produto**.  
  
    > [!NOTE]  
    >  Como o parâmetro está oculto, esse aviso nunca é usado.  
  
5.  Opcionalmente, clique em **Valores Disponíveis** e em **Valores Padrão** e examine as opções. Não altere nenhuma opção nessas guias.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="6-save-the-report-to-a-sharepoint-library"></a><a name="DSave"></a>6. Salve o relatório em uma biblioteca sharepoint  
 É possível salvar o relatório em um biblioteca do SharePoint, em um servidor de relatório ou no computador. Se você salvar o relatório no computador, vários recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como partes do relatório e sub-relatórios, não estarão disponíveis. Neste tutorial, você salvará o relatório em uma biblioteca do SharePoint.  
  
#### <a name="to-save-the-report"></a>Para salvar o relatório  
  
1.  No botão Construtor de Relatórios, clique em **Salvar**. A caixa de diálogo **Salvar como Relatório** é aberta.  
  
    > [!NOTE]  
    >  Se você estiver salvando um relatório de novo, ele será salvo novamente automaticamente em seu local anterior. Para alterar o local, use a opção **Salvar Como** .  
  
2.  Para mostrar uma lista de servidores de relatório e sites do SharePoint usados recentemente, clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do site do SharePoint onde você tem permissão para salvar relatórios.  
  
     A URL da biblioteca do SharePoint tem a seguinte sintaxe:  
  
    ```  
    Http://<ServerName>/<Sites>/  
    ```  
  
4.  Clique em **Save** (Salvar).  
  
     **Sites e Servidores Recentes** lista as bibliotecas no site do SharePoint.  
  
5.  Navegue para a biblioteca onde você salvará o relatório.  
  
6.  Na caixa **Nome** , substitua o nome padrão por **ResellerVSOnlineDrillthrough**.  
  
    > [!NOTE]  
    >  Você salvará o relatório principal no mesmo local. Se desejar salvar os relatórios principal e de detalhamento em sites ou bibliotecas diferentes, você deverá atualizar o caminho da ação **Ir para o relatório** no relatório principal.  
  
7.  Clique em **Save** (Salvar).  
  
##  <a name="1-create-a-new-report-from-the-table-or-matrix-wizard"></a><a name="MMatrixAndDataset"></a>1. Crie um novo relatório do Assistente de Tabela ou Matriz  
 Na caixa de diálogo **Introdução** , crie um relatório de matriz por meio do **Assistente de Tabela ou Matriz**.  
  
#### <a name="to-create-a-new-report"></a>Para criar um novo relatório  
  
1.  Clique **em Iniciar,** aponte [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] para **Programas,** aponte para **''''''''''''Iniciar'.** **Report Builder**  
  
2.  Na caixa de diálogo **Introdução** , verifique se a opção **Novo Relatório** está selecionada e clique em **Assistente de Tabela ou Matriz**.  
  
##  <a name="1a-specify-a-data-connection"></a><a name="MConnection"></a>1a. Especificar uma conexão de dados  
 Você adicionará uma fonte de dados inserida ao relatório principal.  
  
#### <a name="to-create-an-embedded-data-source"></a>Para criar uma fonte de dados inserida  
  
1.  Na página **Escolher um conjunto de dados** , selecione **Criar um conjunto de dados**e clique em **Avançar**.  
  
2.  Clique em **Novo**.  
  
3.  Em **Nome**, digite **Principal de Vendas Online e do Revendedor** como o nome da fonte de dados.  
  
4.  Em **Selecione um tipo de conexão**, selecione **Microsoft SQL Server Analysis Services**e clique em **Compilar**.  
  
5.  Em **Fonte de dados**, verifique se a fonte de dados é **Microsoft SQL Server Analysis Services (AdomdClient)**.  
  
6.  Em **nome do servidor,** digite o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nome de um servidor onde uma instância de está instalada.  
  
7.  Em **Selecionar ou inserir um nome de banco de dados**, selecione o cubo Contoso.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Verifique se a **Cadeia de conexão** contém a seguinte sintaxe:  
  
    ```  
    Data Source=<servername>; Initial Catalog = Contoso  
    ```  
  
10. Clique em **Tipo de credenciais**.  
  
     Dependendo de como as permissões estão configuradas na fonte de dados, poderá ser necessário alterar a autenticação padrão.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**.  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
14. Clique em **Próximo**.  
  
##  <a name="1b-create-an-mdx-query"></a><a name="MMDXQuery"></a>1b. Criar uma consulta MDX  
 Em seguida, crie um conjunto de dados inserido. Para fazer isso, você usará o designer de consulta para criar filtros, parâmetros e membros calculados como também o próprio conjunto de dados.  
  
#### <a name="to-create-query-filters"></a>Para criar filtros de consulta  
  
1.  Na **página Design a consulta,** no painel Metadados, na seção cubo, clique na elipse **(...)**.  
  
2.  Na caixa de diálogo **Seleção de Cubo** , clique em Vendas e em **OK**.  
  
    > [!TIP]  
    >  Se não desejar criar a consulta MDX manualmente, clique no ícone ![Alternar para modo de Design](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-designmode.gif "Alterna para o modo de design"), ative/desative o designer de consultas para o modo de Consulta, cole o MDX concluído no designer de consultas e vá para a etapa 5 em [Para criar o conjunto de dados](#MSkip).  
  
    ```  
    WITH MEMBER [Measures].[Net QTY] AS [Measures].[Sales Quantity] -[Measures].[Sales Return Quantity] MEMBER [Measures].[Net Sales] AS [Measures].[Sales Amount] - [Measures].[Sales Return Amount] SELECT NON EMPTY { [Measures].[Net QTY], [Measures].[Net Sales] } ON COLUMNS, NON EMPTY { ([Channel].[Channel Name].[Channel Name].ALLMEMBERS * [Product].[Product Category Name].[Product Category Name].ALLMEMBERS ) } DIMENSION PROPERTIES MEMBER_CAPTION, MEMBER_UNIQUE_NAME ON ROWS FROM ( SELECT ( { [Date].[Calendar Year].&[2009] } ) ON COLUMNS FROM ( SELECT ( STRTOSET(@ProductProductCategoryName, CONSTRAINED) ) ON COLUMNS FROM ( SELECT ( { [Sales Territory].[Sales Territory Group].&[North America] } ) ON COLUMNS FROM ( SELECT ( { [Channel].[Channel Name].&[2], [Channel].[Channel Name].&[4] } ) ON COLUMNS FROM [Sales])))) WHERE ( [Sales Territory].[Sales Territory Group].&[North America], [Date].[Calendar Year].&[2009] ) CELL PROPERTIES VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGSQuery text: Code.  
    ```  
  
3.  No painel Grupo de Medidas, expanda Canal e arraste Nome do Canal até a coluna **Hierarquia** no painel de filtro.  
  
     O nome da dimensão, Canal, é adicionado automaticamente à coluna **Dimensão** . Não altere as colunas **Dimensão** ou **Operador** .  
  
4.  Para abrir a lista **Expressão de Filtro** , clique na seta para baixo na coluna **Expressão de Filtro** .  
  
5.  Na lista de expressões de filtro, expanda **Todo o Canal**, clique em **Online** , em **Revendedor**e em **OK**.  
  
     A consulta agora inclui um filtro para incluir apenas estes canais: Online e Revendedor.  
  
6.  Expanda a dimensão Território de Vendas e arraste o Grupo Território de Vendas para a coluna **Hierarquia,** abaixo **nome do canal**.  
  
7.  Abra a lista **Expressão de Filtro** , expanda **Toda a Região de Vendas**, clique em **América do Norte**e em **OK**.  
  
     A consulta agora tem um filtro para incluir apenas vendas na América do Norte.  
  
8.  No painel Grupo de Medidas, expanda Data e arraste Ano Civil até a coluna **Hierarquia** no painel de filtro.  
  
     O nome da dimensão, Data, é adicionado automaticamente à coluna **Dimensão** . Não altere as colunas **Dimensão** ou **Operador** .  
  
9. Para abrir a lista **Expressão de Filtro** , clique na seta para baixo na coluna **Expressão de Filtro** .  
  
10. Na lista de expressões de filtro, expanda **Toda a Data**, clique em **Ano 2009**e clique em **OK**.  
  
     A consulta agora inclui um filtro para incluir apenas o ano calendário 2009.  
  
#### <a name="to-create-the-parameter"></a>Para criar o parâmetro  
  
1.  Expanda a dimensão Produto e arraste o membro Nome da Categoria do Produto até a coluna **Hierarquia** , abaixo de **Grupo da Região de Vendas**.  
  
2.  Abra a lista **Expressão de Filtro** , clique em **Todos os Produtos**e em **OK**.  
  
3.  Clique na caixa de seleção **Parâmetro** . A consulta agora inclui o parâmetro ProductProductCategoryName.  
  
#### <a name="to-create-calculated-members"></a>Para criar membros calculados  
  
1.  Posicione o cursor no painel Membros Calculados, clique com o botão direito do mouse e clique em **Novo Membro Calculado**.  
  
2.  No painel Metadados, expanda **as Medidas** e, em seguida, expanda as vendas.  
  
3.  Arraste a medida Quantidade de Vendas até a caixa **Expressão** , digite o caractere de subtração (-), arraste a medida Quantidade de Devoluções de Vendas até a caixa **Expressão** e coloque-a após o caractere de subtração.  
  
     O código a seguir mostra a expressão:  
  
    ```  
    [Measures].[Sales Quantity] - [Measures].[Sales Return Quantity]  
    ```  
  
4.  Na caixa Nome, digite **Qtd Líquida**e clique em **OK**.  
  
     O painel Membros Calculados lista o membro calculado **Qtd Líquida** .  
  
5.  Clique com o botão direito do mouse em **Membros Calculados**e clique em **Novo Membro Calculado**.  
  
6.  No painel Metadados, expanda **Medidas**e Vendas.  
  
7.  Arraste a medida Valor das Vendas até a caixa **Expressão** , digite o caractere de subtração (-), arraste a medida Valor de Devolução das Vendas até a caixa **Expressão** e coloque-a após o caractere de subtração.  
  
     O código a seguir mostra a expressão:  
  
    ```  
    [Measures].[Sales Amount] - [Measures].[Sales Return Amount]  
    ```  
  
8.  Na caixa **Nome** , digite  **Vendas Líquidas**e clique em **OK**. O painel Membros Calculados lista o membro calculado **Vendas Líquidas** .  
  
###  <a name="to-create-the-dataset"></a><a name="MSkip"></a>Para criar o conjunto de dados  
  
1.  Na dimensão Canal, arraste Nome do Canal até o painel de dados.  
  
2.  Na dimensão Produto, arraste Nome da Categoria do Produto até o painel de dados e coloque-o à direita de Nome do Canal.  
  
3.  Em **Membros Calculados**, arraste `Net QTY` até o painel de dados e coloque-o à direita de Nome da Categoria do Produto.  
  
4.  Em Membros Calculados, arraste Vendas Líquidas até o painel de dados e coloque-o à direita de `Net QTY`.  
  
5.  Na barra de ferramentas do designer de consulta, clique **em Executar (!)**.  
  
     Revise o conjunto de resultados da consulta.  
  
6.  Clique em **Próximo**.  
  
##  <a name="1c-organize-data-into-groups"></a><a name="MLayout"></a>1c. Organizar dados em grupos  
 Quando seleciona os campos nos quais agrupar os dados, você cria uma matriz com linhas e colunas que exibe dados detalhados e dados agregados.  
  
#### <a name="to-organize-data-into-groups"></a>Para organizar dados em grupos  
  
1.  Na página **Organizar campos** , arraste Product_Category_Name até **Grupos de linhas**.  
  
2.  Arraste Channel_Name até **Grupos de colunas**.  
  
3.  Arraste `Net_QTY` até **Valores**.  
  
     `Net_QTY` é agregado automaticamente pela função Sum, a agregação padrão para campos numéricos. O valor é `[Sum(Net_QTY)]`.  
  
     Para exibir outras funções de agregação disponíveis, abra a lista suspensa. Não altere a função de agregação.  
  
4.  Arraste `Net_Sales_Return` até **Valores** e coloque-o abaixo de `[Sum(Net_QTY)]`.  
  
     As etapas 3 e 4 especificam os dados a serem exibidos na matriz.  
  
##  <a name="1d-add-subtotals-and-totals"></a><a name="MTotals"></a>1d. Adicionar subtotais e totais  
 Você pode mostrar subtotais e totais gerais em relatórios. Os dados no relatório principal são exibidos como um indicador; você removerá o total geral depois de concluir o assistente.  
  
#### <a name="to-add-subtotals-and-grand-totals"></a>Para adicionar subtotais e totais gerais  
  
1.  Na **página Escolher o layout,** em **Opções,** verifique se **os subtotais e totais de exibição estão selecionados.**  
  
     O painel Visualizar do assistente exibe uma matriz com quatro linhas.  Quando você executar o relatório, cada linha será exibida da seguinte maneira: a primeira linha é o grupo de colunas, a segunda linha contém os títulos das colunas, a terceira linha contém os dados da categoria do produto (`[Sum(Net_ QTY)]` e `[Sum(Net_Sales)]`) e a quarta linha contém os totais.  
  
2.  Clique em **Próximo**.  
  
##  <a name="1e-choose-a-style"></a><a name="MStyle"></a>1e. Escolha um estilo  
 Aplique o estilo Ardósia ao relatório. Esse é o mesmo estilo usado pelo relatório detalhado.  
  
#### <a name="to-specify-a-style"></a>Para especificar um estilo  
  
1.  Na página **Escolha um Estilo,** no painel Estilos, selecione Ardósia.  
  
2.  Clique em **Concluir**.  
  
3.  Para visualizar o relatório, clique em **Executar**.  
  
##  <a name="2-remove-the-grand-total-row"></a><a name="MGrandTotal"></a>2. Remova a grande linha total  
 Os valores de dados são mostrados como estados do indicador, inclusive o totais dos grupos de colunas. Remova a linha que exibe o total geral.  
  
#### <a name="to-remove-the-grand-total-row"></a>Para remover a linha de total geral  
  
1.  Para mudar para o modo design, clique em **Design**.  
  
2.  Clique na linha Total (a última linha da matriz), clique com o botão direito do mouse e clique em **Excluir Linhas**.  
  
3.  Para visualizar o relatório, clique em **Executar**.  
  
##  <a name="3-configure-text-box-action-for-drillthrough"></a><a name="MDrillthrough"></a>3. Configure a ação da caixa de texto para perfuração  
 Para habilitar o detalhamento, especifique uma ação em uma caixa de texto no relatório principal.  
  
#### <a name="to-enable-an-action"></a>Para habilitar uma ação  
  
1.  Para mudar para o modo design, clique em **Design**.  
  
2.  Clique com o botão direito do mouse na célula que contém Product_Category_Name e clique em **Propriedades da Caixa de Texto**.  
  
3.  Clique na guia **Ações**.  
  
4.  Selecione **Ir para relatar.**  
  
5.  Em **Especificar um relatório**, clique em **Procurar**e localize o relatório de detalhamento chamado ResellerVSOnlineDrillthrough.  
  
6.  Para adicionar um parâmetro para executar o relatório de detalhamento, clique em **Adicionar**.  
  
7.  Na lista **Nome** , selecione ProductProductCategoryName.  
  
8.  Em **Valor**, digite `[Product_Category_Name.UniqueName]`.  
  
     Product_Category_Name é um campo do conjunto de dados.  
  
    > [!IMPORTANT]  
    >  Você deve incluir a propriedade `UniqueName` porque a ação de detalhamento exige um valor exclusivo.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-format-the-drillthrough-field"></a>Para formatar o campo de detalhamento  
  
1.  Clique com o botão direito do mouse na célula que contém o `Product_Category_Name`e clique em **Propriedades da Caixa de Texto**.  
  
2.  Clique na guia **Fonte** .  
  
3.  Na lista **Efeitos** , selecione **Sublinhar**.  
  
4.  Na lista **Cor** , selecione **Azul**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Para visualizar o relatório, clique em **Executar**.  
  
 Os nomes das categorias de produto estão no formato de link comum (azul e sublinhado).  
  
##  <a name="4-replace-numeric-values-with-indicators"></a><a name="MIndicators"></a>4. Substitua valores numéricos por indicadores  
 Use indicadores para mostrar o estado de quantidades e vendas dos canais Online e de Revendedor.  
  
#### <a name="to-add-an-indicator-for-net-qty-values"></a>Para adicionar um indicador para valores de QTD Líquida  
  
1.  Para mudar para o modo design, clique em **Design**.  
  
2.  Na faixa de opções, clique no ícone **Retângulo** e clique na célula `[Sum(Net QTY)]` do grupo de linhas `[Product_Category_Name]` no grupo de colunas `Channel_Name` .  
  
3.  Na faixa de opções, clique no ícone **Indicador** e clique dentro do retângulo. A caixa de diálogo **Selecionar Tipo de Indicador** é aberta com o indicador **Direcional** selecionado.  
  
4.  Clique no tipo **3 Sinais** e em **OK**.  
  
5.  Clique com o botão direito do mouse no indicador e, no painel Dados do Medidor, clique na seta para baixo ao lado de **(Não especificado)**. Selecione `Net_QTY`.  
  
6.  Repita as etapas 2 a 5 para a célula `[Sum(Net QTY)]` no grupo de linhas `[Product_Category_Name]` dentro de **Total**.  
  
#### <a name="to-add-an-indicator-for-net-sales-values"></a>Para adicionar um indicador para valores de Vendas Líquidas  
  
1.  Na faixa de opções, clique no ícone **Retângulo** e clique dentro da célula `[Sum(Net_Sales)]` no grupo de linhas `[Product_Category_Name]` do grupo de colunas `Channel_Name` .  
  
2.  Na faixa de opções, clique no ícone **Indicador** e clique dentro do retângulo.  
  
3.  Clique no tipo **3 Sinais** e em **OK**.  
  
4.  Clique com o botão direito do mouse no indicador e, no painel Dados do Medidor, clique na seta para baixo ao lado de **(Não especificado)**. Selecione `Net_Sales`.  
  
5.  Repita as etapas 1 a 4 para a célula `[Sum(Net_Sales)]` no grupo de linhas `[Product_Category_Name]` dentro de **Total**.  
  
6.  Para visualizar o relatório, clique em **Executar**.  
  
##  <a name="5-update-parameter-properties"></a><a name="MParameter"></a>5. Atualizar propriedades do parâmetro  
 Por padrão, os parâmetros estão visíveis, o que não é apropriado para este relatório. Você atualizará as propriedades dos parâmetros para tornar os parâmetros internos.  
  
#### <a name="to-make-the-parameter-internal"></a>Para tornar o parâmetro interno  
  
1.  No painel Dados do Relatório, expanda **Parâmetros**.  
  
2.  Clique com o botão direito do mouse em `@ProductProductCategoryName,` e clique em **Propriedades do Parâmetro**.  
  
3.  Na guia **Geral** , clique em **Interno**.  
  
4.  Opcionalmente, clique nas guias **Valores Disponíveis** e **Valores Padrão** e examine as opções. Não altere nenhuma opção nessas guias.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="6-add-a-report-title"></a><a name="MTitle"></a>6. Adicione um título de relatório  
 Adicione um título ao relatório principal.  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas de Categorias de Produtos de 2009: Categoria Online e Revendedor:**.  
  
3.  Selecione o texto que você digitou.  
  
4.  Na guia **Início** da faixa de opções, no grupo Fonte, selecione a fonte **Times New Roman** , tamanho **16 pt** e os estilos **Negrito** e **Itálico** .  
  
5.  Para visualizar o relatório, clique em **Executar**.  
  
##  <a name="7-save-the-main-report-to-a-sharepoint-library"></a><a name="MSave"></a>7. Salve o relatório principal em uma biblioteca sharepoint  
 Salve o relatório principal em uma biblioteca do SharePoint.  
  
#### <a name="to-save-the-report"></a>Para salvar o relatório  
  
1.  Para mudar para o modo design, clique em **Design**.  
  
2.  No botão Construtor de Relatórios, clique em **Salvar**.  
  
3.  Opcionalmente, para mostrar uma lista de servidores de relatório e sites do SharePoint usados recentemente, clique em **Sites e Servidores Recentes**.  
  
4.  Selecione ou digite o nome do site do SharePoint onde você tem permissão para salvar relatórios. A URL da biblioteca do SharePoint tem a seguinte sintaxe:  
  
    ```  
    Http://<ServerName>/<Sites>/  
    ```  
  
5.  Navegue para a biblioteca onde você deseja salvar o relatório.  
  
6.  Em **Nome**, substitua o nome padrão por **ResellerVSOnlineMain**.  
  
    > [!IMPORTANT]  
    >  Salve o relatório principal no mesmo local onde você salvou o relatório detalhado. Para salvar os relatórios principal e de detalhamento em sites ou bibliotecas diferentes, confirme se a ação **Ir para o relatório** no relatório principal aponta para o local correto do relatório de detalhamento.  
  
7.  Clique em **Save** (Salvar).  
  
##  <a name="8-run-the-main-and-drillthrough-reports"></a><a name="MRunReports"></a>8. Execute os relatórios principais e perfurados  
 Execute o relatório principal e clique nos valores da coluna de categorias de produto para executar o relatório detalhado.  
  
#### <a name="to-run-the-reports"></a>Para executar os relatórios  
  
1.  Abra a biblioteca do SharePoint onde os relatórios foram salvos.  
  
2.  Clique duas vezes em ResellerVSOnlineMain.  
  
     O relatório é executado e exibe informações de vendas de categorias de produtos.  
  
3.  Clique no link **Games and Toys** na coluna que contém nomes de categorias de produto.  
  
     O relatório detalhado é executado exibindo apenas os valores da categoria de produto Games and Toys.  
  
4.  Para retornar ao relatório principal, clique no botão voltar do Internet Explorer.  
  
5.  Opcionalmente, explore outras categorias de produto clicando nos respectivos nomes.  
  
## <a name="see-also"></a>Consulte Também  
 [Tutoriais &#40;relatório&#41;](report-builder-tutorials.md)  
  
  
