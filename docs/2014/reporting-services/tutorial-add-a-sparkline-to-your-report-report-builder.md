---
title: 'Tutorial: Adicionar um minigráfico ao relatório (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a543182d5c367be9cc1be875f05c1ab5d4c9bfcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099038"
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>Tutorial: Adicionar um minigráfico ao relatório (Construtor de Relatórios)
  Neste tutorial, você cria um relatório de tabela básico com base em dados de vendas de exemplo e, em seguida, adiciona um minigráfico a uma célula da tabela.  
  
 Uma versão aprimorada do relatório criado por você neste tutorial está disponível como um relatório de exemplo do Construtor de Relatórios da [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obter mais informações sobre como baixar este relatório de exemplo e outros, consulte [Construtor de relatórios relatórios de exemplo](https://go.microsoft.com/fwlink/?LinkId=184851). A ilustração a seguir mostra o relatório de exemplo semelhante ao que você criará.  
  
 ![rs_SparklineMatrixTutorial](../../2014/tutorials/media/rs-sparklinematrixtutorial.gif "rs_SparklineMatrixTutorial")  
  
 O vídeo [como: criar um minigráfico em uma tabela (Construtor de relatórios vídeo)](https://technet.microsoft.com/bi/ff871942.aspx) ilustra como criar um relatório semelhante com minigráficos.  
  
##  <a name="BackToTop"></a>O que você aprenderá  
 Neste tutorial, você aprenderá a fazer o seguinte:  
  
 1. [Criar um relatório com uma tabela](#CreateTable)  
  
 2. [Criar uma consulta no Assistente de Tabela ou Matriz](#Query)  
  
 3. [Adicionar um minigráfico à tabela](#Sparkline)  
  
 4. [Alinhar os minigráficos vertical e horizontalmente](#AlignSparklines)  
  
### <a name="other-optional-steps"></a>Outras etapas opcionais  
 5. [Formatar dados como moeda](#FormatCurrency)  
  
 6. [Formatar dados como datas](#FormatDates)  
  
 7. [Alterar a Largura das Colunas](#Width)  
  
 8. [Adicionar um título de relatório](#Title)  
  
 9. [Salvar o relatório](#Save)  
  
 Tempo estimado para concluir este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="CreateTable"></a>1. criar um relatório com uma tabela  
  
#### <a name="to-create-a-report"></a>Para criar um relatório  
  
1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.  
  
     A caixa de diálogo **introdução** é aberta.  
  
    > [!NOTE]  
    >  Se a caixa de diálogo **introdução** não for exibida, no botão **Construtor de relatórios** , clique em **novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Tabela ou Matriz**.  
  
4.  Na página **Escolher um conjunto de dados** , selecione **Criar um conjunto de dados**e clique em **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
    > [!NOTE]  
    >  Este tutorial não precisa de dados específicos; ele só precisa de uma conexão com um banco de dados [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . Se você já tiver uma conexão de fonte de dados listada em **Conexões de Fonte de Dados**, será possível selecioná-la e ir para a etapa 10. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  Clique em **Nova**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
6.  Em **Nome**, digite **Vendas de Produtos**, um nome para a fonte de dados.  
  
7.  Em **Selecionar um tipo de conexão**, verifique se a opção **Microsoft SQL Server** está selecionada.  
  
8.  Em **Cadeia de conexão**, digite o seguinte texto:  
  
     **Fonte de dados\<= servername>**  
  
     A expressão \<servername>, por exemplo, Report001, especifica um computador no qual uma instância do SQL Server mecanismo de banco de dados está instalada. Como os dados do relatório não são extraídos de um banco de dados do SQL Server, você não precisa incluir o nome de um banco de dados. O banco de dados padrão no servidor especificado é usado para analisar a consulta.  
  
9. Clique em **Credenciais**. Insira as credenciais necessárias para acessar a fonte de dados externa.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Você voltará à página **Escolher uma conexão com uma fonte de dados** .  
  
11. Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**.  
  
     A mensagem "Conexão criada com êxito" será exibida.  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. Clique em **Próximo**.  
  
##  <a name="Query"></a>2. criar uma consulta no assistente de tabela  
 Em um relatório, é possível usar um conjunto de dados compartilhado que tenha uma consulta predefinida. Se preferir, crie um conjunto de dados inserido para ser usado somente em seu relatório. Neste tutorial, você criará um conjunto de dados inserido.  
  
> [!NOTE]  
>  Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-create-a-query"></a>Para criar uma consulta  
  
1.  Na página **Criar uma consulta** , o designer de consultas relacionais é aberto. Para este tutorial, você usará o designer de consulta baseado em texto.  
  
2.  Clique em **Editar Como Texto**. O designer de consulta baseado em texto exibe um painel de consulta e um painel de resultados.  
  
3.  Cole a consulta [!INCLUDE[tsql](../includes/tsql-md.md)] a seguir na caixa **Consulta** .  
  
    ```  
    SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2010-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  Na barra de ferramentas do designer de consultas, clique em executar (**!**).  
  
     A consulta é executada e exibe o conjunto de resultados dos campos **SalesDate**, **subcategoria**, **produto**, **vendas**e **quantidade**.  
  
5.  Clique em **Próximo**.  
  
6.  Na página **Organizar campos** , arraste **Sales** até **Valores**.  
  
     As **vendas** são agregadas pela função SUM. O valor é [Sum(Sales)].  
  
7.  Arraste **Product** até **Grupos de linhas**.  
  
8.  Arraste **SalesDate** até **Grupos de colunas**.  
  
9. Clique em **Próximo**.  
  
10. Na página **Escolher o layout** , em **Opções**, verifique se a opção **Mostrar subtotais e totais gerais** está selecionada.  
  
     O painel Visualizar do assistente exibe uma tabela com três linhas. Ao executar o relatório, cada linha será exibida da seguinte forma:  
  
    1.  A primeira linha aparecerá uma vez para a tabela a fim de mostrar os títulos da coluna.  
  
    2.  A segunda linha será repetida uma vez para cada produto e exibirá o nome do produto, o total por dia e o total da linha.  
  
    3.  A terceira linha aparecerá uma vez para a tabela a fim de exibir totais gerais.  
  
11. Clique em **Próximo**.  
  
12. Na página **Escolha um estilo** , no painel **Estilos** , selecione **Ardósia**.  
  
     O painel Visualizar exibirá um exemplo da tabela com esse estilo.  
  
13. Clique em **Concluir**.  
  
14. A tabela é adicionada à superfície de design. A tabela tem três colunas e três linhas.  
  
     Pesquisar o painel Agrupamento. Se você não conseguir ver o painel Agrupamento, no menu **Exibir** , clique em **Agrupamento**. O painel Grupos de Linhas mostra um grupo de linhas: **Product**. O painel Grupos de Colunas mostra um grupo de colunas: **SalesDate**. Os dados detalhados são todos os dados recuperados pela consulta do conjunto de dados.  
  
15. Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Sparkline"></a>3. adicionar um minigráfico  
  
#### <a name="to-add-a-sparkline-chart-to-a-table"></a>Para adicionar um minigráfico a uma tabela  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Selecione a coluna Total na tabela.  
  
3.  Clique com o botão direito do mouse, aponte para **Inserir Coluna**e clique em **Esquerda**.  
  
4.  Na nova coluna, clique com o botão direito do mouse na linha [Product], aponte para a guia **Inserir** faixa de bits e clique em **minigráfico**.  
  
5.  Verifique se o primeiro minigráfico na linha da **coluna** está selecionado e clique em **OK**.  
  
6.  Clique no minigráfico para mostrar o painel Dados do Gráfico.  
  
7.  Clique no sinal de mais (+) na caixa valores e clique em **vendas**.  
  
     Os valores no campo **Sales** agora são os valores do minigráfico.  
  
8.  Clique no sinal de mais (+) na caixa grupos de categorias e, em seguida, clique em **SalesDate**.  
  
9. Clique em **Executar** para visualizar o relatório.  
  
     Observe que há minigráficos em cada linha da tabela, mas eles não estão corretos. As barras nos gráficos não se alinham. Como só há quatro barras na segunda linha de dados, as barras são mais largas do que as barras na primeira linha, que tem seis. Não é possível comparar valores para cada produto por dia. Elas precisam se alinhar.  
  
     Também observe que, para cada linha, a maior barra na linha é da altura da linha. Isso também é enganador, porque os maiores valores para cada linha não são iguais: o maior valor para o criador de filmes de orçamento é $10400, mas o maior valor para o slim digital é $26576-mais do que duas vezes maior. Além disso, as barras maiores nessas duas linhas têm aproximadamente a mesma altura. Também é preciso fazer isso para dimensioná-las com os outros minigráficos.  
  
     ![rs_SprklineMtrxUnaligndBars](../../2014/tutorials/media/rs-sprklinemtrxunaligndbars.gif "rs_SprklineMtrxUnaligndBars")  
  
##  <a name="AlignSparklines"></a>4. alinhar os minigráficos vertical e horizontalmente  
 Os Minigráficos são difíceis de ler quando nem todos usam as mesmas medições. Os eixos horizontal e vertical de cada um deles precisa corresponder ao resto.  
  
#### <a name="to-set-alignment-for-the-sparklines-in-the-table"></a>Para definir o alinhamento dos minigráficos na tabela  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique com o botão direito do mouse no minigráfico e clique em **Propriedades do Eixo Vertical**.  
  
3.  Marque a caixa de seleção **Alinhar eixos em** .  
  
     Tablix1 está aparecendo na lista. Essa é a única opção. Isso define a altura das barras em cada minigráfico referente às outras.  
  
4.  Clique em **OK**.  
  
5.  Clique com o botão direito do mouse no minigráfico e clique em **Propriedades do Eixo Horizontal**.  
  
6.  Marque a caixa de seleção **Alinhar eixos em** .  
  
     Tablix1 está aparecendo na lista. Essa é a única opção. Isso define a largura das barras em cada minigráfico referente às outras. Se alguns minigráficos tiverem menos barras em sequência do que outros, esses minigráficos terão espaços em branco para os dados não encontrados.  
  
7.  Clique em **OK**.  
  
8.  Clique em **Executar** para visualizar o relatório novamente.  
  
 Observe que todas as barras agora estão alinhadas com as barras nas outras linhas.  
  
##  <a name="FormatCurrency"></a>5. (opcional) formatar dados como moeda  
 Por padrão, os dados de resumo do campo **Sales** exibem um número geral. Formate-o para exibir o número como moeda. Ative/desative **Estilos de Espaço Reservado** para exibir caixas de texto formatadas e texto de espaço reservado como valores de exemplo.  
  
#### <a name="to-format-a-currency-field"></a>Para formatar um campo de conversor de moedas  
  
1.  Clique em **design** para alternar para o modo Design.  
  
2.  Clique na célula na segunda linha (sob a linha títulos de coluna) na coluna **SalesDate** e arraste para selecionar todas as células que contêm `[Sum(Sales)]`.  
  
3.  Na guia **Início** , no grupo **Número** , clique no botão **Moeda** . As células são alteradas para mostrar a moeda formatada.  
  
     Se a configuração regional for Inglês (Estados Unidos), o texto de exemplo padrão será [**$12,345.00**]. Se você não vir um valor de moeda de exemplo, clique em **estilos de espaço reservado** no grupo **números** e clique em **valores de exemplo**.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
 Os valores de resumo para exibição de **vendas** como moeda.  
  
##  <a name="FormatDates"></a>6. (opcional) formatar dados como datas  
 Por padrão, o campo **SalesDate** exibe informações de data e hora. É possível formatá-lo para exibir somente a data.  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>Para formatar um campo de data como o formato padrão  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na célula que contém `[SalesDate]`.  
  
3.  Na faixa de opções, na guia **início** , no grupo **número** , na lista suspensa, selecione **Data**.  
  
     A célula exibe a data de exemplo **[1/31/2000]**. Se uma data de exemplo não estiver visível, clique em **Estilos de Espaço Reservado** no grupo **Números** e clique em **Valores de Exemplo**.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
 Os valores de **SalesDate** são exibidos no formato de data padrão.  
  
##  <a name="Width"></a>7. (opcional) alterar larguras de coluna  
 Por padrão, cada célula da tabela contém uma caixa de texto. Uma caixa de texto é expandida verticalmente para acomodar o texto quando a página é renderizada. No relatório renderizado, cada linha é expandida até a altura da caixa de texto renderizada mais alta da linha. A altura da linha na superfície de design não tem nenhum efeito na altura da linha no relatório renderizado.  
  
 Para reduzir a quantidade de espaço vertical que cada linha ocupa, expanda a largura da coluna para acomodar em uma única linha o conteúdo esperado das caixas de texto da coluna.  
  
#### <a name="to-change-the-width-of-columns"></a>Para alterar a largura das colunas  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na tabela de forma que os identificadores de coluna e linha sejam exibidos acima e ao lado da tabela.  
  
     As barras em cinza ao longo da parte superior e ao lado da tabela são os identificadores de coluna e de linha.  
  
3.  Aponte para a linha entre os identificadores de coluna para que o cursor seja alterado para uma seta dupla. Arraste as colunas de acordo com o tamanho desejado. Por exemplo, expanda a coluna do **produto** para que o nome do produto seja exibido em uma linha.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Title"></a>8. (opcional) adicionar um título de relatório  
 Um título é exibido na parte superior do relatório. É possível colocar o título em um cabeçalho do relatório. No entanto, se ele não usar um cabeçalho, será possível colocar o título em uma caixa de texto na parte superior do corpo do relatório. Neste tutorial, você usará a caixa de texto colocada automaticamente na parte superior do corpo do relatório.  
  
 O texto pode ser aprimorado ainda mais aplicando-se estilos, tamanhos e cores de fontes diferentes a frases e caracteres individuais do texto. Para obter mais informações, consulte [Formatar o texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas de Produtos**e clique fora da caixa de texto.  
  
3.  Clique com o botão direito do mouse na caixa de texto que contém **Vendas de Produtos** e clique em **Propriedades da Caixa de Texto**.  
  
4.  Na caixa de diálogo **Propriedades da Caixa de Texto** , clique em **Fonte**.  
  
5.  Na lista **Tamanho** , selecione **18pt**.  
  
6.  Na lista **cor** , selecione **bordô**.  
  
7.  Selecione **Negrito**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a>9. salvar o relatório  
 Salve o relatório em um servidor de relatório ou no computador. Se você não salvar o relatório no servidor de relatório, vários recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como partes do relatório e sub-relatórios, não estarão disponíveis.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de relatórios** , clique em **salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
     A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por **Vendas de Produtos**.  
  
5.  Clique em **Save** (Salvar).  
  
 O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de relatórios** , clique em **salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu computador**e procure a pasta na qual você quer salvar o relatório.  
  
3.  Em **Nome**, substitua o nome padrão por **Vendas de Produtos**.  
  
4.  Clique em **Save** (Salvar).  
  
## <a name="next-steps"></a>Próximas etapas  
 Isso conclui o tutorial para criar um relatório de tabela com minigráficos. Para obter mais informações sobre minigráficos, consulte [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [TUTORIAIS &#40;Construtor de Relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
