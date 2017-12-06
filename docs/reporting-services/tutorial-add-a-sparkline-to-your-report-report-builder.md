---
title: "Tutorial: Adicionar um minigráfico ao relatório (Construtor de Relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
caps.latest.revision: "17"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2821641b938291ac67fefb08e4e174f8113db033
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>Tutorial: Adicionar um minigráfico ao relatório (Construtor de Relatórios)

Neste tutorial do [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)], você cria uma tabela básica com um minigráfico em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .   
  
Minigráficos e barras de dados são gráficos pequenos e simples que transmitem muitas informações em um espaço pequeno, geralmente em tabelas e matrizes dos relatórios do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . A ilustração a seguir mostra um relatório semelhante ao que você criará.  
  
![report-builder-sparkline-final](../reporting-services/media/report-builder-sparkline-final.png)  
     
Tempo estimado para concluir este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="CreateTable"></a>1. Criar um relatório com uma tabela  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Tabela ou Matriz**.  
  
4.  Na página **Escolher um conjunto de dados** , selecione **Criar um conjunto de dados** > **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
    > [!NOTE]  
    > Este tutorial não precisa de dados específicos. Ele só precisa de uma conexão com um banco de dados do SQL Server. Se você já tiver uma conexão de fonte de dados listada em **Conexões de Fonte de Dados**, será possível selecioná-la e ir para a etapa 10. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  Clique em **Nova**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
6.  Em **Nome**, digite **Vendas de Produtos**, um nome para a fonte de dados.  
  
7.  Em **Selecionar um tipo de conexão**, verifique se a opção **Microsoft SQL Server** está selecionada.  
  
8.  Em **Cadeia de conexão**, digite o seguinte texto:  
  
    `Data Source\=<servername>`  
  
    A expressão `<servername>`, por exemplo, Report001, especifica um computador no qual há uma instância do Mecanismo de Banco de Dados do SQL Server instalada. Como os dados do relatório não são extraídos de um banco de dados do SQL Server, você não precisa incluir o nome de um banco de dados. O banco de dados padrão no servidor especificado é usado para analisar a consulta.  
  
9. Clique em **Credenciais**. Insira as credenciais necessárias para acessar a fonte de dados externa.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Você voltará à página **Escolher uma conexão com uma fonte de dados** .  
  
11. Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**.  
  
    A mensagem "Conexão criada com êxito" será exibida.  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. Clique em **Avançar**.  
  
## <a name="Query"></a>2. Criar uma consulta e o layout da tabela no Assistente de Tabela  
Em um relatório, é possível usar um conjunto de dados compartilhado que tenha uma consulta predefinida. Se preferir, crie um conjunto de dados inserido para ser usado somente em seu relatório. Neste tutorial, você criará um conjunto de dados inserido.  
  
> [!NOTE]  
> Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
### <a name="to-create-a-query-and-table-layout-in-the-table-wizard"></a>Para criar uma consulta e o layout da tabela no Assistente de Tabela 
  
1.  Na página **Criar uma consulta** , o designer de consultas relacionais é aberto. Para este tutorial, você usará o designer de consulta baseado em texto.  
  
2.  Clique em **Editar Como Texto**. O designer de consulta baseado em texto exibe um painel de consulta e um painel de resultados.  
  
3.  Cole a consulta [!INCLUDE[tsql](../includes/tsql-md.md)] a seguir na caixa **Consulta** .  
  
    ```  
    SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  Na barra de ferramentas do designer de consultas, clique em Executar (**!**).  
  
    A consulta é executada e exibe o conjunto de resultados dos campos **SalesDate**, **Subcategory**, **Product**, **Sales**e **Quantity**.  
  
5.  Clique em **Avançar**.  
  
6.  Na página **Organizar campos** , arraste **Sales** até **Valores**.  
  
    **Sales** é agregado pela função Sum. O valor é [Sum(Sales)].  
  
7.  Arraste **Product** até **Grupos de linhas**.  
  
8.  Arraste **SalesDate** até **Grupos de colunas**.  

    ![report-builder-sparkline-arrange-fields](../reporting-services/media/report-builder-sparkline-arrange-fields.png)
  
9. Clique em **Avançar**.  
  
10. Na página **Escolher o layout** , em **Opções**, verifique se a opção **Mostrar subtotais e totais gerais** está selecionada.  
  
    O painel Visualizar do assistente exibe uma tabela com três linhas. Ao executar o relatório, cada linha será exibida da seguinte forma:  
  
    *  A primeira linha aparecerá uma vez para a tabela a fim de mostrar os títulos da coluna.  
  
    *  A segunda linha será repetida uma vez para cada produto e exibirá o nome do produto, o total por dia e o total da linha.  
  
    *  A terceira linha aparecerá uma vez para a tabela a fim de exibir totais gerais.  
    
    ![report-builder-sparkline-choose-layout](../reporting-services/media/report-builder-sparkline-choose-layout.png)
  
11. Clique em **Avançar**.  
  
12. Clique em **Concluir**.  
  
14. A tabela é adicionada à superfície de design. A tabela tem três colunas e três linhas.  
  
    Pesquisar o painel Agrupamento. Se você não conseguir ver o painel Agrupamento, no menu **Exibir** , clique em **Agrupamento**. O painel Grupos de Linhas mostra um grupo de linhas: **Product**. O painel Grupos de Colunas mostra um grupo de colunas: **SalesDate**. Os dados detalhados são todos os dados recuperados pela consulta do conjunto de dados.  
    
    ![report-builder-sparkline-grouping-pane](../reporting-services/media/report-builder-sparkline-grouping-pane.png)
  
15. Clique em **Executar** para visualizar o relatório.  

### <a name="FormatCurrency"></a>2a. Formatar dados como moeda  
Por padrão, os dados de resumo do campo **Sales** exibem um número geral. Formate-o para exibir o número como moeda. Ative/desative **Estilos de Espaço Reservado** para exibir caixas de texto formatadas e texto de espaço reservado como valores de exemplo.  
  
1.  Clique em **Design** a fim de alternar para a exibição de design.  
  
2.  Clique na célula da segunda linha (sob a linha dos cabeçalhos de coluna) na coluna **SalesDate** . Mantenha pressionada a tecla Ctrl e selecione todas as células que contêm `[Sum(Sales)]`. 

    ![report-builder-select-sum-sales](../reporting-services/media/report-builder-select-sum-sales.png) 
  
3.  Na guia **Início** > grupo **Número**, clique em **Moeda**. As células são alteradas para mostrar a moeda formatada.  

    ![report-builder-placeholder-currency](../reporting-services/media/report-builder-placeholder-currency.png)
  
    Se a configuração regional for Inglês (Estados Unidos), o texto de exemplo padrão será [**$12,345.00**]. Se um valor de moeda de exemplo não estiver visível, no grupo **Números** , clique em **Estilos de Espaço Reservado** > **Valores de Exemplo**.  
    
    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)
   
### <a name="FormatDates"></a>2b. (Opcional) Formatar dados como datas  
Por padrão, o campo **SalesDate** exibe informações de data e hora. É possível formatá-lo para exibir somente a data.  
  
1.  Clique na célula que contém `[SalesDate]`.  
  
3.  Na guia **Início** > grupo **Número** > **Data**.  
  
    A célula exibe a data de exemplo **[1/31/2000]**.
     
4.  Clique em **Executar** para visualizar o relatório.  
  
Os valores de **SalesDate** são exibidos no formato de data padrão e os valores de resumo de **Sales** são exibidos como moeda.   
  
## <a name="Sparkline"></a>3. Adicionar um minigráfico    
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Selecione a coluna Total na tabela.  
  
3.  Clique com o botão direito do mouse, aponte para **Inserir Coluna**e clique em **Esquerda**.  

    ![report-builder-add-column-left](../reporting-services/media/report-builder-add-column-left.png)
  
4.  Na nova coluna, clique com o botão direito do mouse na célula da linha `[Product]` > **Inserir** > **Minigráfico**.  

    ![report-builder-insert-sparkline](../reporting-services/media/report-builder-insert-sparkline.png)
  
5.  Na caixa de diálogo **Selecionar Tipo de Minigráfico** , verifique se o primeiro minigráfico na linha **Coluna** está selecionado e clique em **OK**.  
  
6.  Clique no minigráfico para mostrar o painel Dados do Gráfico.  
  
7.  Clique no sinal de adição (+) na caixa Valores e em **Sales**. 

    ![report-builder-sparkline-values](../reporting-services/media/report-builder-sparkline-values.png) 
  
    Os valores no campo **Sales** agora são os valores do minigráfico.  
  
8.  Clique no sinal de adição (+) na caixa Grupos de Categorias e em **SalesDate**.  
  
9. Clique em **Executar** para visualizar o relatório.  
  
    Observe que as barras nos gráficos de minigráfico não estão alinhadas entre si. Como só há quatro barras na segunda linha de dados, as barras são mais largas do que as barras na primeira linha, que tem seis. Não é possível comparar valores para cada produto por dia. Elas precisam ser alinhadas.  
  
    Além disso, para cada linha, a barra mais alta é a altura da linha. Isso também é confuso, porque os maiores valores de cada linha não são iguais: o maior valor de Budget Movie-Maker é US$ 10.400, mas o maior valor de Slim Digital é US$ 26.576 – mais de duas vezes maior. Além disso, as barras maiores nessas duas linhas têm aproximadamente a mesma altura. Todos os minigráficos precisam usar a mesma escala.  
  
     ![report-builder-sparkline-misaligned](../reporting-services/media/report-builder-sparkline-misaligned.png)
  
## <a name="AlignSparklines"></a>4. Alinhar os minigráficos vertical e horizontalmente  
Os minigráficos são difíceis de ler quando todos não apresentam as mesmas medidas. Os eixos horizontal e vertical de cada um deles precisa corresponder ao resto.  
   
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique com o botão direito do mouse no minigráfico e clique em **Propriedades do Eixo Vertical**.  
  
3.  Marque a caixa de seleção **Alinhar eixos em** . Tablix1 é a única opção da lista.  
  
     Isso define a altura das barras em cada minigráfico referente às outras. 
  
4.  Clique em **OK**.  
  
5.  Clique com o botão direito do mouse no minigráfico e clique em **Propriedades do Eixo Horizontal**.  
  
6.  Marque a caixa de seleção **Alinhar eixos em** . Tablix1 é a única opção da lista. 
  
    Isso define a largura das barras em cada minigráfico referente às outras. Se alguns minigráficos tiverem menos barras em sequência do que outros, esses minigráficos terão espaços em branco para os dados não encontrados.  
  
7.  Clique em **OK**.  
  
8.  Clique em **Executar** para visualizar o relatório novamente.  
  
Agora todas as barras em cada minigráfico são alinhadas às barras dos outros minigráficos, e as alturas são relativas.  
  
![report-builder-sparkline-aligned](../reporting-services/media/report-builder-sparkline-aligned.png)
  
## <a name="Width"></a>7. (Opcional) Alterar larguras da coluna  
Por padrão, cada célula da tabela contém uma caixa de texto. Uma caixa de texto é expandida verticalmente para acomodar o texto quando a página é renderizada. No relatório renderizado, cada linha é expandida até a altura da caixa de texto renderizada mais alta da linha. A altura da linha na superfície de design não tem nenhum efeito na altura da linha no relatório renderizado.  
  
Para reduzir a quantidade de espaço vertical que cada linha ocupa, expanda a largura da coluna para acomodar em uma única linha o conteúdo esperado das caixas de texto da coluna.  
  
### <a name="to-change-the-width-of-columns"></a>Para alterar a largura das colunas  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na tabela para que as barras cinza sejam exibidas acima e ao lado da tabela. Esses são os identificadores de linha e de coluna
  
3.  Aponte para a linha entre os identificadores de coluna para que o cursor seja alterado para uma seta dupla. Arraste a coluna **Product** para que o nome do produto seja exibido em uma linha.  
  
4.  Clique em **Executar** para visualizar o relatório e veja se ele é grande o suficiente.  
  
## <a name="Title"></a>8. (Opcional) Adicionar um título de relatório  
Um título é exibido na parte superior do relatório. É possível colocar o título em um cabeçalho do relatório. No entanto, se ele não usar um cabeçalho, será possível colocar o título em uma caixa de texto na parte superior do corpo do relatório. Neste tutorial, você usará a caixa de texto colocada automaticamente na parte superior do corpo do relatório.  
  
O texto pode ser aprimorado ainda mais aplicando-se estilos, tamanhos e cores de fontes diferentes a frases e caracteres individuais do texto. Para obter mais informações, consulte [Formatar o texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas por Data**e clique fora da caixa de texto.  
  
3.  Marque a caixa de texto que contém **Vendas de Produtos**.  
  
4.  Na guia Início > grupo **Fonte** > para **Cor**, selecione **Azul-petróleo**.  
  
7.  Selecione **Negrito**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Save"></a>9. Salvar o relatório  
Salve o relatório em um servidor de relatório ou no computador. Se você não salvar o relatório no servidor de relatório, vários recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como partes do relatório e sub-relatórios, não estarão disponíveis.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
    A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por **Vendas de Produtos**.  
  
5.  Clique em **Salvar**.  
  
O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu computador**e procure a pasta na qual você quer salvar o relatório.  
  
3.  Em **Nome**, substitua o nome padrão por **Vendas de Produtos**.  
  
4.  Clique em **Salvar**.  
  
## <a name="next-steps"></a>Próximas etapas  

Isso conclui o tutorial para criar um relatório de tabela com minigráficos. Para obter mais informações sobre minigráficos, consulte [Minigráficos e barras de dados](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
[Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md) 
[Construtor de Relatórios no SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
