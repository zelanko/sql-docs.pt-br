---
title: 'Tutorial: Criar um relatório de tabela básico (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9e30521-f8ae-4c45-89c3-d40727f622f7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93213609abbc3e274cc61207d02b3828f9b90d7d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099031"
---
# <a name="tutorial-creating-a-basic-table-report-report-builder"></a>Tutorial: Criar um relatório de tabela básico (Construtor de Relatórios)
  Este tutorial ensina a criar um relatório de tabela básico com base em dados de vendas de exemplo. A ilustração a seguir mostra o relatório que você criará.  
  
 ![rs_CreateBasicReportTutorial](../../2014/tutorials/media/rs-createbasicreporttutorial.gif "rs_CreateBasicReportTutorial")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
1.  [Criar um Novo Relatório em Introdução](#CreateTable)  
  
    1.  [Especificar uma conexão de dados no assistente de tabela](#DataConnection)  
  
    2.  [Criar uma Consulta no Assistente de Tabela](#Query)  
  
    3.  [Organizar Dados em Grupos no Assistente de Tabela](#Groups)  
  
    4.  [Adicionar Linhas de Subtotal e de Total no Assistente de Tabela](#Subtotals)  
  
    5.  [Escolher um Estilo no Assistente de Tabela](#Style)  
  
2.  [Formatar dados como moeda](#FormatCurrency)  
  
3.  [Formatar dados como data](#FormatDate)  
  
4.  [Alterar a Largura das Colunas](#Width)  
  
5.  [Adicionar um título de relatório](#Title)  
  
6.  [Salvar o relatório](#Save)  
  
7.  [Exportar o relatório](#Export)  
  
 Tempo estimado para concluir este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-new-report-from-getting-started"></a><a name="CreateTable"></a>1. criar um novo relatório de Introdução  
 Crie um relatório de tabela na caixa de diálogo **introdução** . Há dois modos: design de relatório e design de conjunto de dados compartilhado. No modo design de relatório, especifique dados no painel de Dados do Relatório e o layout do relatório na superfície de design. No modo design de conjunto de dados compartilhado, crie consultas de conjunto de dados para compartilhar com outras pessoas. Neste tutorial, você usará o modo design de relatório.  
  
#### <a name="to-create-a-new-report"></a>Para criar um novo relatório  
  
1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.  
  
     A caixa de diálogo **Guia de Introdução** é aberta.  
  
    > [!NOTE]  
    >  Se a caixa de diálogo **introdução** não for exibida, no botão **Construtor de relatórios** , clique em **novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, verifique se a opção **Assistente de Tabela ou Matriz** está selecionada.  
  
##  <a name="1a-specify-a-data-connection-in-the-table-wizard"></a><a name="DataConnection"></a>1a. Especificar uma conexão de dados no assistente de tabela  
 Uma conexão de dados contém as informações para estabelecer conexões com uma fonte de dados externa, como um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Geralmente, você obtém as informações sobre a conexão e o tipo de credenciais a ser usado do proprietário da fonte de dados. Para especificar uma conexão de dados, você pode usar uma fonte de dados compartilhada do servidor de relatório ou criar uma fonte de dados inserida que será usada somente neste relatório.  
  
 Neste tutorial, você usará uma fonte de dados inserida. Para saber mais sobre como usar fontes de dados compartilhadas, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
#### <a name="to-create-an-embedded-data-source"></a>Para criar uma fonte de dados inserida  
  
1.  Na página **Escolher um conjunto de dados** , selecione **Criar um conjunto de dados**e clique em **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
2.  Clique em **Novo**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
3.  Em **nome**, digite **vendas do produto** um nome para a fonte de dados.  
  
4.  Em **Selecionar um tipo de conexão**, verifique se a opção **Microsoft SQL Server** está selecionada.  
  
5.  Em **cadeia de conexão**, digite o seguinte texto, em que * \<ServerName>* é o nome de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]uma instância do:  
  
    ```  
    Data Source=<servername>  
    ```  
  
     Como você usará uma consulta que contém os dados, em vez de recuperá-los de um banco de dados, a cadeia de conexão não incluirá o nome do banco de dados. Para saber mais, veja [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
6.  Clique em **Credenciais**. Insira as credenciais necessárias para acessar a fonte de dados externa.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Você voltará à página **Escolher uma conexão com uma fonte de dados** .  
  
8.  Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**.  
  
     A mensagem "Conexão criada com êxito" será exibida.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Clique em **Avançar**.  
  
##  <a name="1b-create-a-query-in-the-table-wizard"></a><a name="Query"></a>1B. Criar uma Consulta no Assistente de Tabela  
 Em um relatório, é possível usar um conjunto de dados compartilhado que tenha uma consulta predefinida. Se preferir, crie um conjunto de dados inserido para ser usado somente em seu relatório. Neste tutorial, você criará um conjunto de dados inserido.  
  
> [!NOTE]  
>  Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-create-a-query"></a>Para criar uma consulta  
  
1.  Na página **Criar uma consulta** , o designer de consultas relacionais é aberto. Para este tutorial, você usará o designer de consulta baseado em texto.  
  
     Clique em **Editar como texto**. O designer de consulta baseado em texto exibe um painel de consulta e um painel de resultados.  
  
2.  Cole a consulta [!INCLUDE[tsql](../includes/tsql-md.md)] a seguir na caixa **Consulta** .  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(9924.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
  
    ```  
  
3.  Na barra de ferramentas do designer de consultas, clique em **executar** (**!**).  
  
     A consulta executa e exibe o conjunto de resultados para os campos SalesDate, Subcategory, Product, Sales e Quantity.  
  
     No conjunto de resultados, os cabeçalhos das colunas têm como base os nomes na consulta. No conjunto de dados, os cabeçalhos das colunas se transformam nos nomes dos campos e são salvos no relatório. Depois de concluir o assistente, você poderá usar o painel de Dados do Relatório para exibir a coleção de campos do conjunto de dados.  
  
4.  Clique em **Avançar**.  
  
##  <a name="1c-organize-data-into-groups-in-the-table-wizard"></a><a name="Groups"></a>1C. Organizar Dados em Grupos no Assistente de Tabela  
 Quando você seleciona campos nos quais fazer agrupamentos, cria uma tabela com linhas e colunas que exibem dados detalhados e dados agregados.  
  
#### <a name="to-organize-data-into-groups"></a>Para organizar dados em grupos  
  
1.  Na página **organizar campos** , arraste produto para **valores**.  
  
2.  Arraste Quantity até **Values** e coloque-o abaixo de Product.  
  
     Quantity é automaticamente agregado pela função Sum, a função de agregação padrão para campos numéricos. O valor é [Sum(Quantity)].  
  
     Você pode abrir a lista suspensa para exibir as outras funções de agregação disponíveis. Não altere a função de agregação.  
  
3.  Arraste Sales até **Values** e coloque-o abaixo de [Sum(Quantity)].  
  
     Sales é agregado pela função Sum. O valor é [Sum(Sales)].  
  
     As etapas 1, 2 e 3 especificam os dados a serem exibidos na tabela.  
  
4.  Arraste SalesDate até **Grupos de linhas**.  
  
5.  Arraste Subcategory até **Grupos de linhas** e coloque-o abaixo de SalesDate.  
  
     As etapas 4 e 5 organizam os valores dos campos primeiro por data e depois por subcategoria de produto dessa data.  
  
6.  Clique em **Avançar**.  
  
##  <a name="1d-add-subtotal-and-total-rows-in-the-table-wizard"></a><a name="Subtotals"></a>1D. Adicionar Linhas de Subtotal e de Total no Assistente de Tabela  
 Depois de criar grupos, é possível adicionar e formatar linhas nas quais exibir valores de agregação dos campos. Você pode optar por exibir todos os dados ou deixar um usuário expandir e recolher dados agrupados de forma interativa.  
  
#### <a name="to-add-subtotals-and-totals"></a>Para adicionar subtotais e totais  
  
1.  Na página **escolher o layout** , em opções, verifique se a **opção** **Mostrar Subtotais e totais gerais** está selecionada.  
  
2.  Verifique se a opção **Bloqueado, subtotal abaixo** está selecionada.  
  
     O painel Visualizar assistente exibe uma tabela com cinco linhas. Ao executar o relatório, cada linha será exibida da seguinte forma:  
  
    1.  A primeira linha será repetida uma vez para a tabela para mostrar títulos de coluna.  
  
    2.  A segunda linha será repetida uma vez para cada item de linha no pedido de vendas e exibirá o nome do produto, a quantidade do pedido e o total da linha.  
  
    3.  A terceira linha será repetida uma vez para cada pedido de vendas para exibir subtotais por pedido.  
  
    4.  A quarta será repetida uma vez para cada data de pedido de vendas para exibir subtotais por dia.  
  
    5.  A quinta linha será repetida uma vez para a tabela para mostrar totais gerais.  
  
3.  Desmarque a opção **Expandir/recolher grupos**. Neste tutorial, o relatório criado não usa o recurso de detalhamento que permite a um usuário expandir uma hierarquia de grupo pai para exibir linhas de grupo filho e linhas de detalhes.  
  
4.  Clique em **Avançar**.  
  
##  <a name="1e-choose-a-style-in-the-table-wizard"></a><a name="Style"></a>1e. Escolher um Estilo no Assistente de Tabela  
 Um estilo especifica um estilo de fonte, um conjunto de cores e um estilo de borda.  
  
#### <a name="to-specify-a-table-style"></a>Para especificar um estilo de tabela  
  
1.  Na página **escolher um estilo** , no painel estilos, selecione oceano.  
  
     O painel Visualizar exibirá um exemplo da tabela com esse estilo.  
  
2.  Se preferir, clique nos demais estilos para visualizar exemplos de suas aplicações.  
  
3.  Clique em **Concluir**.  
  
 A tabela é adicionada à superfície de design. A tabela tem 5 colunas e 5 linhas. O painel Grupos de Linhas mostra três grupos de linhas: SalesDate, Subcategory e Details. Os dados detalhados são todos os dados recuperados pela consulta do conjunto de dados.  
  
##  <a name="2-format-data-as-currency"></a><a name="FormatCurrency"></a>2. formatar dados como moeda  
 Por padrão, os dados resumidos do campo Sales exibe um número geral. Formate-o para exibir o número como moeda. Ative/desative **Estilos de Espaço Reservado** para exibir caixas de texto formatadas e texto de espaço reservado como valores de exemplo.  
  
#### <a name="to-format-a-currency-field"></a>Para formatar um campo de conversor de moedas  
  
1.  Clique em **Design** a fim de alternar para a exibição de design.  
  
2.  Clique na célula da segunda linha (na linha dos cabeçalhos das colunas) na coluna Vendas e arraste-a para baixo para selecionar todas as células que contenham `[Sum(Sales)]`.  
  
3.  Na guia **Início** , no grupo **Número** , clique no botão **Moeda** . As células são alteradas para mostrar a moeda formatada.  
  
     Se a configuração regional for Inglês (Estados Unidos), o texto de exemplo padrão será [**$12,345.00**]. Se você não vir um valor de moeda de exemplo, clique em **estilos de espaço reservado** no grupo **números** e clique em **valores de exemplo**.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
 Os valores resumidos de Vendas são exibidos como conversor de moedas.  
  
##  <a name="3-format-data-as-date"></a><a name="FormatDate"></a>3. formatar dados como data  
 Por padrão, o campo SalesDate exibe informações de data e hora. É possível formatá-lo para exibir somente a data.  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>Para formatar um campo de data como o formato padrão  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na célula que contém `[SalesDate]`.  
  
3.  Na faixa de opções, na guia **início** , no grupo **número** , na lista suspensa, selecione **Data**.  
  
     A célula exibe a data de exemplo **[1/31/2000]**. Se uma data de exemplo não estiver visível, clique em **Estilos de Espaço Reservado** no grupo **Números** e clique em **Valores de Exemplo**.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
 Os valores SalesDate são exibidos no formato de data padrão.  
  
#### <a name="to-change-the-date-format-to-a-custom-format"></a>Para alterar o formato de data para um formato personalizado  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na célula que contém `[SalesDate]`.  
  
3.  Na guia **início** , no grupo **número** , clique no iniciador da caixa de diálogo.  
  
     O iniciador é a pequena seta no canto direito do grupo. A caixa de diálogo **Propriedades da Caixa de Texto** é aberta.  
  
4.  No painel Categoria, verifique se a opção **Data** está selecionada.  
  
5.  No painel **Tipo** , selecione **31 de janeiro de 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     A célula exibe a data de exemplo **[31 de janeiro de 2000]**.  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
 O valor de SalesDate é exibido com o nome do mês, e não com o número dele.  
  
##  <a name="4-change-column-widths"></a><a name="Width"></a>4. alterar larguras de coluna  
 Por padrão, cada célula da tabela contém uma caixa de texto. Uma caixa de texto é expandida verticalmente para acomodar o texto quando a página é renderizada. No relatório renderizado, cada linha é expandida até a altura da caixa de texto renderizada mais alta da linha. A altura da linha na superfície de design não tem nenhum efeito na altura da linha no relatório renderizado.  
  
 Para reduzir a quantidade de espaço vertical que cada linha ocupa, expanda a largura da coluna para acomodar em uma única linha o conteúdo esperado das caixas de texto da coluna.  
  
#### <a name="to-change-the-width-of-table-columns"></a>Para alterar a largura das colunas da tabela  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na tabela de forma que os identificadores de coluna e linha sejam exibidos acima e ao lado da tabela.  
  
     As barras em cinza ao longo da parte superior e ao lado da tabela são os identificadores de coluna e de linha.  
  
3.  Aponte para a linha entre os identificadores de coluna para que o cursor seja alterado para uma seta dupla. Arraste as colunas de acordo com o tamanho desejado. Por exemplo, expanda a coluna Produto, de forma que o nome do produto seja exibido em uma linha.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="5-add-a-report-title"></a><a name="Title"></a>5. adicionar um título de relatório  
 Um título é exibido na parte superior do relatório. É possível colocar o título em um cabeçalho do relatório. No entanto, se ele não usar um cabeçalho, será possível colocar o título em uma caixa de texto na parte superior do corpo do relatório. Neste tutorial, você usará a caixa de texto colocada automaticamente na parte superior do corpo do relatório.  
  
 O texto pode ser aprimorado ainda mais aplicando-se estilos, tamanhos e cores de fontes diferentes a frases e caracteres individuais do texto. Para obter mais informações, consulte [Formatar o texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas de Produtos**e clique fora da caixa de texto.  
  
3.  Clique com o botão direito do mouse na caixa de texto que contém **Vendas de Produtos** e clique em **Propriedades da Caixa de Texto**.  
  
4.  Na caixa de diálogo **Propriedades da Caixa de Texto** , clique em **Fonte**.  
  
5.  Na lista **Tamanho** , selecione **18pt**.  
  
6.  Na lista **Cor** , selecione **Azul-centáurea**.  
  
7.  Selecione **Negrito**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="6-save-the-report"></a><a name="Save"></a>6. salvar o relatório  
 Salve o relatório em um servidor de relatório ou no computador. Se você não salvar o relatório no servidor de relatório, vários recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como partes do relatório e sub-relatórios, não estarão disponíveis.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
     A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por **Vendas de Produtos**.  
  
5.  Clique em **Salvar**.  
  
 O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu computador**e procure a pasta na qual você quer salvar o relatório.  
  
3.  Em **Nome**, substitua o nome padrão por **Vendas de Produtos**.  
  
4.  Clique em **Salvar**.  
  
##  <a name="7-export-the-report"></a><a name="Export"></a>7. exportar o relatório  
 Os relatórios podem ser exportados para diversos formatos, como Microsoft Excel e CSV (valores separados por vírgulas). Para obter mais informações, consulte [Exportando relatórios &#40;Construtor de relatórios e SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md).  
  
 Neste tutorial, você exportará o relatório para o Excel e definirá uma propriedade no relatório para atribuir um nome personalizado à guia Pasta de Trabalho.  
  
#### <a name="to-specify-the-workbook-tab-name"></a>Para especificar o nome da guia Pasta de Trabalho  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique em qualquer ponto fora do relatório.  
  
3.  . No painel Propriedades, localize a propriedade InitialPageName e digite **Sales do produto Excel**.  
  
    > [!NOTE]  
    >  Se o painel Propriedades não estiver visível, clique na guia Exibir na faixa de e, em seguida, clique em **Propriedades**.  
  
#### <a name="to-export-a-report-to-excel"></a>Para exportar um relatório para o Excel  
  
1.  Clique em **Executar** para visualizar o relatório.  
  
2.  . Na faixa de faixas, clique em **Exportar**e, em seguida, clique em **Excel**.  
  
     A caixa de diálogo **Salvar como** é aberta.  
  
3.  Navegue até a pasta **documentos** .  
  
4.  Na caixa de texto **nome do arquivo** , digite **Sales do produto Excel**.  
  
5.  Verifique se o tipo de arquivo é **pasta de trabalho do Excel**.  
  
6.  Clique em **Salvar**.  
  
#### <a name="to-view-the-report-in-excel"></a>Para exibir o relatório no Excel  
  
1.  Abra a pasta **documentos** e clique duas vezes em **vendas de produtos Excel. xlsx**.  
  
2.  Verifique se o nome da guia de pasta de trabalho é **Vendas de Produtos em Excel**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Isso conclui o passo a passo sobre como criar um relatório de tabela básico. Para obter mais informações sobre tabelas, consulte [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [TUTORIAIS &#40;Construtor de Relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
