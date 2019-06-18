---
title: 'Tutorial: Criação de um relatório de tabela básico (Construtor de Relatórios) | Microsoft Docs'
ms.date: 06/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: d9e30521-f8ae-4c45-89c3-d40727f622f7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5a97a0cfc446a32e02172d22391dec8e5ca13af6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041193"
---
# <a name="tutorial-creating-a-basic-table-report-report-builder"></a>Tutorial: criando um relatório de tabela básico (Construtor de Relatórios)
Este tutorial ensina a criar um relatório de tabela básico com base em dados de vendas de exemplo. A ilustração a seguir mostra o relatório que você criará.  
  
![SSRS_Tutorial_Basic_Table_Report](../reporting-services/media/ssrs-tutorial-basic-table-report.png)  
  

Tempo estimado para concluir este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="CreateTable"></a>1. Criar um relatório usando um assistente  
Crie um relatório de tabela com o Assistente de Tabela ou Matriz. Há dois modos: design de relatório e design de conjunto de dados compartilhado. No modo design de relatório, especifique dados no painel de Dados do Relatório e o layout do relatório na superfície de design. No modo design de conjunto de dados compartilhado, crie consultas de conjunto de dados para compartilhar com outras pessoas. Neste tutorial, você usará o modo design de relatório.  
  
### <a name="to-create-a-report"></a>Para criar um relatório  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, selecione **Assistente de Tabela ou Matriz**.  
  
## <a name="DataConnection"></a>1a. Especificar uma conexão de dados no assistente de tabela  
Uma conexão de dados contém as informações para estabelecer conexões com uma fonte de dados externa, como um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Geralmente, você obtém as informações sobre a conexão e o tipo de credenciais a ser usado do proprietário da fonte de dados. Para especificar uma conexão de dados, você pode usar uma fonte de dados compartilhada do servidor de relatório ou criar uma fonte de dados inserida que será usada somente neste relatório.  
  
Neste tutorial, você usará uma fonte de dados inserida. Para saber mais sobre como usar fontes de dados compartilhadas, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
### <a name="to-create-an-embedded-data-source"></a>Para criar uma fonte de dados inserida  
  
1.  Na página **Escolher um conjunto de dados** , selecione **Criar um conjunto de dados**e clique em **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
2.  Clique em **Nova**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
3.  Em **Nome**, digite **Product_Sales** , um nome para a fonte de dados.  
  
4.  Em **Selecionar um tipo de conexão**, verifique se a opção **Microsoft SQL Server** está selecionada.  
  
5.  Em **Cadeia de Conexão**, digite o seguinte texto, em que \<servername> é o nome de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
    ```  
    Data Source=<servername>  
    ```  
  
    Como você usará uma consulta que contém os dados, em vez de recuperá-los de um banco de dados, a cadeia de conexão não incluirá o nome do banco de dados. Para saber mais, veja [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
6.  Clique na guia **Credenciais** . Insira as credenciais necessárias para acessar a fonte de dados externa.  
  
7. Clique na guia Geral novamente. Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**.  
  
    A mensagem "Conexão criada com êxito" será exibida.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Você voltará à página **Escolher uma conexão com uma fonte de dados** , com a nova fonte de dados selecionada.  
  
9. Clique em **Avançar**.  
  
## <a name="Query"></a>1b. Criar uma Consulta no Assistente de Tabela  
Em um relatório, é possível usar um conjunto de dados compartilhado que tem uma consulta predefinida. Se preferir, crie um conjunto de dados inserido para ser usado somente neste relatório. Neste tutorial, você criará um conjunto de dados inserido.  
  
> [!NOTE]  
> Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
### <a name="to-create-a-query"></a>Para criar uma consulta  
  
1.  Na página **Criar uma consulta** , o designer de consultas relacionais é aberto. Para este tutorial, você usará o designer de consulta baseado em texto.  
  
    Clique em **Editar Como Texto**. O designer de consulta baseado em texto exibe um painel de consulta e um painel de resultados.  
  
2.  Cole a consulta [!INCLUDE[tsql](../includes/tsql-md.md)] a seguir na caixa superior em branco.  
  
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
  
3.  Na barra de ferramentas do designer de consultas, clique em **Executar** ( **!** ).  
  
    A consulta executa e exibe o conjunto de resultados para os campos SalesDate, Subcategory, Product, Sales e Quantity.  
  
    No conjunto de resultados, os cabeçalhos das colunas têm como base os nomes na consulta. No conjunto de dados, os cabeçalhos das colunas se transformam nos nomes dos campos e são salvos no relatório. Depois de concluir o assistente, você poderá usar o painel de Dados do Relatório para exibir a coleção de campos do conjunto de dados.  
  
4.  Clique em **Avançar**.  
  
## <a name="Groups"></a>1c. Organizar Dados em Grupos no Assistente de Tabela  
Quando você seleciona campos nos quais fazer agrupamentos, cria uma tabela com linhas e colunas que exibem dados detalhados e dados agregados.  
  
### <a name="to-organize-data-into-groups"></a>Para organizar dados em grupos  
  
1.  Na página **Organizar campos** , arraste Product até **Valores**.  
  
2.  Arraste Quantity até **Values** e coloque-o abaixo de Product.  
  
    Quantity é automaticamente agregado pela função Sum, a função de agregação padrão para campos numéricos. O valor é [Sum(Quantity)].  
  
    Selecione a seta ao lado de [Sum(Quantity)] para exibir outras funções de agregação disponíveis. Não altere a função de agregação.  
  
3.  Arraste Sales até **Values** e coloque-o abaixo de [Sum(Quantity)].  
  
    Sales é agregado pela função Sum. O valor é [Sum(Sales)].  
  
    As etapas 1, 2 e 3 especificam os dados a serem exibidos na tabela.  
  
4.  Arraste SalesDate até **Grupos de linhas**.  
  
5.  Arraste Subcategory até **Grupos de linhas** e coloque-o abaixo de SalesDate.  
  
    As etapas 4 e 5 organizam os valores dos campos primeiro por data e depois por subcategoria de produto dessa data.  
  
6.  Clique em **Avançar**.  
  
## <a name="Subtotals"></a>1d. Adicionar Linhas de Subtotal e de Total no Assistente de Tabela  
Depois de criar grupos, é possível adicionar e formatar linhas nas quais exibir valores de agregação dos campos. Você pode optar por exibir todos os dados ou deixar um usuário expandir e recolher dados agrupados de forma interativa.  
  
### <a name="to-add-subtotals-and-totals"></a>Para adicionar subtotais e totais  
  
1.  Na página **Escolher o layout** , em **Opções**, verifique se a opção **Mostrar subtotais e totais gerais** está selecionada.  
  
2.  Verifique se a opção **Bloqueado, subtotal abaixo** está selecionada.  
  
    O painel Visualizar assistente exibe uma tabela com cinco linhas. Ao executar o relatório, cada linha será exibida da seguinte forma:  
  
    1.  A primeira linha será repetida uma vez para a tabela para mostrar títulos de coluna.  
  
    2.  A segunda linha será repetida uma vez para cada item de linha no pedido de vendas e exibirá o nome do produto, a quantidade do pedido e o total da linha.  
  
    3.  A terceira linha será repetida uma vez para cada pedido de vendas para exibir subtotais por pedido.  
  
    4.  A quarta será repetida uma vez para cada data de pedido de vendas para exibir subtotais por dia.  
  
    5.  A quinta linha será repetida uma vez para a tabela para mostrar totais gerais.  
  
3.  Desmarque a opção **Expandir/recolher grupos**. Neste tutorial, o relatório criado não usa o recurso de detalhamento que permite a um usuário expandir uma hierarquia de grupo pai para exibir linhas de grupo filho e linhas de detalhes.  
  
4.  Clique em **Avançar** para visualizar a tabela e clique em **Concluir**.  
  
A tabela é adicionada à superfície de design. A tabela tem 5 colunas e 5 linhas. O painel Grupos de Linhas mostra três grupos de linhas: SalesDate, Subcategory e Details. Os dados detalhados são todos os dados recuperados pela consulta do conjunto de dados.  
  
## <a name="FormatCurrency"></a>2. Formatar dados como moeda  
Por padrão, os dados resumidos do campo Sales exibe um número geral. Formate-o para exibir o número como moeda.   
  
### <a name="to-format-a-currency-field"></a>Para formatar um campo de conversor de moedas  
  
1.  Para ver as caixas de texto formatadas e o texto de espaço reservado como valores de exemplo modo de exibição de Design, na guia **Início**, no grupo **Número**, clique na seta ao lado do ícone **Estilos de Espaço Reservado** > **Valores de Exemplo**.  
  
2.   Clique na célula da segunda linha (na linha dos cabeçalhos das colunas) na coluna Vendas e arraste-a para baixo para selecionar todas as células que contenham `[Sum(Sales)]`.  
  
3.  Na guia **Início** , no grupo **Número** , clique no botão **Moeda** . As células são alteradas para mostrar a moeda formatada.  
  
    Se a configuração regional for Inglês (Estados Unidos), o texto de exemplo padrão será [ **$12,345.00**]. Se um valor de moeda de exemplo não estiver visível, na guia **Início**, no grupo **Número**, clique na seta ao lado do ícone **Estilos de Espaço Reservado** > **Valores de Exemplo**.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
Os valores resumidos de Vendas são exibidos como conversor de moedas.  
  
## <a name="FormatDate"></a>3. Formatar dados como data  
Por padrão, o campo SalesDate exibe a data e hora. É possível formatá-lo para exibir somente a data.  
  
### <a name="to-format-a-date-field-as-the-default-format"></a>Para formatar um campo de data como o formato padrão  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na célula que contém `[SalesDate]`.  
  
3.  Na Faixa de Opções, na guia **Início** , no grupo **Número** , clique na seta e selecione **Data**.  
  
    A célula exibe a data de exemplo **[1/31/2000]** . Se uma data de exemplo não estiver visível, na guia **Início**, no grupo **Número**, clique na seta ao lado do ícone **Estilos de Espaço Reservado** > **Valores de Exemplo**.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
Os valores SalesDate são exibidos no formato de data padrão.  
  
### <a name="to-change-the-date-format-to-a-custom-format"></a>Para alterar o formato de data para um formato personalizado  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na célula que contém `[SalesDate]`.  
  
3.  Na guia **Início** , no grupo **Número** , clique na seta no canto inferior direito para abrir a caixa de diálogo.  
  
    A caixa de diálogo **Propriedades da Caixa de Texto** é aberta.  
  
4.  No painel Categoria, verifique se a opção **Data** está selecionada.  
  
5.  No painel **Tipo** , selecione **31 de janeiro de 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    A célula exibe a data de exemplo **[31 de janeiro de 2000]** .  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
O valor de SalesDate exibe o nome do mês, em vez do número do mês.  
  
## <a name="Width"></a>4. Alterar a Largura das Colunas  
Por padrão, cada célula da tabela contém uma caixa de texto. Uma caixa de texto é expandida verticalmente para acomodar o texto quando a página é renderizada. No relatório renderizado, cada linha é expandida até a altura da caixa de texto renderizada mais alta da linha. A altura da linha na superfície de design não tem nenhum efeito na altura da linha no relatório renderizado.  
  
Para reduzir a quantidade de espaço vertical que cada linha ocupa, expanda a largura da coluna para acomodar em uma única linha o conteúdo esperado das caixas de texto da coluna.  
  
### <a name="to-change-the-width-of-table-columns"></a>Para alterar a largura das colunas da tabela  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na tabela de forma que os identificadores de coluna e linha sejam exibidos acima e ao lado da tabela.  
  
    As barras em cinza ao longo da parte superior e ao lado da tabela são os identificadores de coluna e de linha.  
  
3.  Aponte para a linha entre os identificadores de coluna para que o cursor seja alterado para uma seta dupla. Arraste as colunas de acordo com a largura desejada. Por exemplo, expanda a coluna Produto, de forma que o nome do produto seja exibido em uma linha.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="Title"></a>5. Adicionar um título de relatório  
Um título é exibido na parte superior do relatório. É possível colocar o título em um cabeçalho do relatório. No entanto, se ele não usar um cabeçalho, será possível colocar o título em uma caixa de texto na parte superior do corpo do relatório. Neste tutorial, você usará a caixa de texto colocada automaticamente na parte superior do corpo do relatório.  
  
O texto pode ser aprimorado ainda mais aplicando-se estilos, tamanhos e cores de fontes diferentes a frases e caracteres individuais do texto. Para obter mais informações, consulte [Formatar o texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas de Produtos**e clique fora da caixa de texto.  
  
3.  Clique com o botão direito do mouse na caixa de texto que contém **Vendas de Produtos** e clique em **Propriedades da Caixa de Texto**.  
  
4.  Na caixa de diálogo **Propriedades da Caixa de Texto** , clique em **Fonte**.  
  
5.  Na lista **Tamanho** , selecione **18pt**.  
  
6.  Na lista **Cor** , selecione **Azul-centáurea**.  
  
7.  Selecione **Negrito**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Save"></a>6. Salvar o relatório  
Salve o relatório em um servidor de relatório ou no computador. Se você não salvar o relatório no servidor de relatório, vários recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como partes do relatório e sub-relatórios, não estarão disponíveis.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  Clique em **Arquivo** > **Salvar Como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
    A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua **Sem Título** por **Product_Sales**.  
  
5.  Clique em **Salvar**.  
  
O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  Clique em **Arquivo** > **Salvar Como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu computador**e procure a pasta na qual você quer salvar o relatório.  
  
3.  Em **Nome**, substitua **Sem Título** por **Vendas de Produtos**.  
  
4.  Clique em **Salvar**.  
  
## <a name="Export"></a>7. Exportar o relatório  
Os relatórios podem ser exportados para diferentes formatos, como Microsoft Excel e arquivos CSV (valores separados por vírgula). Para obter mais informações, consulte [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
Neste tutorial, você exportará o relatório para o Excel e definirá uma propriedade no relatório para atribuir um nome personalizado à guia Pasta de Trabalho.  
  
### <a name="to-specify-the-workbook-tab-name"></a>Para especificar o nome da guia Pasta de Trabalho  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique em qualquer lugar da superfície de design, fora do relatório.  
  
3.  No painel Propriedades, localize a propriedade InitialPageName e digite **Vendas de Produtos em Excel**.  
  
    > [!NOTE]  
    > Se o painel Propriedades não estiver visível, na guia **Exibir** , selecione **Propriedades**.  
    > Se uma propriedade não estiver visível no painel Propriedades, tente selecionar o botão **Alfabético** na parte superior do painel para ordenar todas as propriedades em ordem alfabética.   
  
### <a name="to-export-a-report-to-excel"></a>Para exportar um relatório para o Excel  
  
1.  Clique em **Executar** para visualizar o relatório.  
  
2.  Na faixa de opções, clique em **Exportar** > **Excel**.  
  
    O é aberto.  
  
3.  Na caixa de diálogo **Salvar Como** , navegue até o local em que você quer salvar o arquivo.  
  
4.  Na caixa de texto **Nome do arquivo** , digite **Product_Sales_Excel**.  
  
5.  Verifique se o tipo de arquivo é **Excel (\*.xlsx)** .  
  
6.  Clique em **Salvar**.  
  
### <a name="to-view-the-report-in-excel"></a>Para exibir o relatório no Excel  
  
1.  Abra a pasta em que você salvou a pasta de trabalho e clique duas vezes em **Product_Sales_Excel.xlsx**.  
  
2.  Verifique se o nome da guia de pasta de trabalho é **Vendas de Produtos em Excel**.  
  
## <a name="next-steps"></a>Next Steps  
Isso conclui o passo a passo sobre como criar um relatório de tabela básico. Para obter mais informações sobre tabelas, consulte [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
[Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md)  
[Construtor de Relatórios no SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

