---
title: 'Tutorial: Criar um relatório de matriz (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f87c1188b0abd1b576da63412829464368275b0f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098916"
---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>Tutorial: Criar um relatório de matriz (Construtor de Relatórios)
  Este tutorial ensina a criar um relatório de matriz básico com base em dados de vendas de exemplo. A matriz tem grupos de linhas e de colunas aninhados e um grupo de colunas adjacente. Você também aprenderá a formatar colunas e a girar texto. A ilustração a seguir mostra um relatório semelhante ao que você criará.  
  
 ![rs_CreateMatixReportTutorial](../../2014/tutorials/media/rs-creatematixreporttutorial.gif "rs_CreateMatixReportTutorial")  
  
 Uma versão aprimorada do relatório que você criará neste tutorial está disponível como um relatório de exemplo do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Report Builder. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [relatórios de exemplo do construtor de relatórios](https://go.microsoft.com/fwlink/?LinkId=184851).  
  
##  <a name="BackToTop"></a> O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
1.  [Criar um relatório de matriz e um conjunto de dados de novo Assistente de tabela ou matriz](#CreateMatrix)  
  
2.  [Organizar dados e escolha o Layout e estilo no novo Assistente de tabela ou matriz](#Groups)  
  
3.  [Formatar dados](#FormatData)  
  
4.  [Adicionar grupo de colunas adjacente](#AdjacentGroup)  
  
5.  [Alterar larguras da coluna](#Width)  
  
6.  [Mesclar células na matriz](#MergeCells)  
  
7.  [Adicionar um cabeçalho de relatório e o título de relatório](#HeaderTitle)  
  
8.  [Salvar o relatório](#Save)  
  
### <a name="other-optional-step"></a>Outra etapa opcional  
  
1.  [Girar texto caixa em 270 graus](#RotateTextBox)  
  
 Tempo estimado para concluir este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="CreateMatrix"></a> 1. Criar um relatório de matriz e um conjunto de dados no Assistente de Nova Tabela ou Matriz  
 Dos **guia de Introdução** caixa de diálogo Construtor de relatórios, escolha uma fonte de dados, criar um conjunto de dados inserido e, em seguida, exiba os dados em uma matriz.  
  
> [!NOTE]  
>  Neste tutorial, como já contém os valores de dados, a consulta não precisa de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-create-a-new-matrix"></a>Para criar uma nova matriz  
  
1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.  
  
    > [!NOTE]  
    >  A caixa de diálogo **Guia de Introdução** deve ser exibida. Caso contrário, no botão Construtor de relatórios, clique em **New**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Tabela ou Matriz**.  
  
4.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados**.  
  
5.  Clique em **Avançar**.  
  
6.  Sobre o **escolher uma conexão a uma fonte de dados** página, selecione uma fonte de dados existente ou navegue até o servidor de relatório e, em seguida, selecione uma fonte de dados. Se não houver nenhuma fonte de dados disponível ou você não tiver acesso a um servidor de relatório, em vez disso, será possível usar uma fonte de dados inserida. Para obter mais informações sobre como criar uma fonte de dados inserida, consulte [Tutorial: Ciar um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Clique em **Avançar**.  
  
8.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
9. Copie e cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. Clique em **Avançar**.  
  
##  <a name="Groups"></a> 2. Organizar dados e escolha o Layout e estilo no novo Assistente de tabela ou matriz  
 Use o assistente para fornecer um design inicial no qual exibir dados. O painel de visualização no assistente ajuda a visualizar o resultado dos dados de agrupamento antes de concluir o design da matriz.  
  
#### <a name="to-organize-data-into-groups-and-choose-a-layout-and-style"></a>Para organizar dados em grupos e escolher um layout e um estilo  
  
1.  Na página **Organizar campos** , arraste Territory de **Campos disponíveis** até **Grupos de linhas**.  
  
2.  Arraste SalesDate até **Grupos de linhas** e coloque-o abaixo de Territory.  
  
     A ordem na qual os campos são listados em **Grupos de linhas** define a hierarquia do grupo. As etapas 1 e 2 organizam os valores dos campos primeiro por território e, em seguida, por data das vendas.  
  
3.  Arraste Subcategory até **Grupos de colunas**.  
  
4.  Arraste Product até **grupos de colunas** e coloque-o abaixo de Subcategory.  
  
     A ordem na qual os campos são listados em **grupos de colunas** define a hierarquia de grupo.  
  
     As etapas 3 e 4 organizam os valores dos campos primeiro por subcategoria e, em seguida, por produto.  
  
5.  Arraste Sales até **Valores**.  
  
     Sales é resumido com a função Soma, a função padrão para resumir campos numéricos.  
  
6.  Arraste Quantity até **Valores**.  
  
     Quantity é resumida com a função Soma.  
  
     As etapas 5 e 6 especificam os dados a serem exibidos nas células de dados da matriz.  
  
7.  Clique em **Avançar**.  
  
8.  Na página Escolher o Layout, em **Opções**, verifique se a opção **Mostrar subtotais e totais gerais** está selecionada.  
  
9. Verifique se a opção **Bloqueado, subtotal abaixo** está selecionada.  
  
10. Verifique se a opção **Expandir/recolher grupos** está selecionada.  
  
11. Clique em **Avançar**.  
  
12. Na página Escolha um estilo, no painel Estilos, selecione **Slate**.  
  
13. Clique em **Concluir**.  
  
     A matriz é adicionada à superfície de design. O painel Grupos de Linhas mostra dois grupos de linhas: Território e SalesDate. O painel Grupos de Colunas mostra dois grupos de colunas: Subcategoria e Produto. Os dados detalhados são todos os dados recuperados pela consulta do conjunto de dados.  
  
14. Clique em **Executar** para visualizar o relatório.  
  
 Para cada produto vendido em uma data específica, a matriz mostra a subcategoria a que o produto pertence e o território das vendas.  
  
##  <a name="FormatData"></a> 3. Formatar dados  
 Por padrão, os dados resumidos do campo Sales exibem um número geral e o campo SalesDate exibe informações de data e hora. Formate o campo Sales para exibir o número como moeda e o campo SalesDate para exibir apenas a data. Ative/desative **Estilos de Espaço Reservado** para exibir caixas de texto formatadas e texto de espaço reservado como valores de exemplo.  
  
#### <a name="to-format-fields"></a>Para formatar campos  
  
1.  Clique em **Design** a fim de alternar para a exibição de design.  
  
2.  Pressione a tecla Ctrl e, em seguida, selecione as nove células que contenham `[Sum(Sales)]`.  
  
3.  Na guia **Início** , no grupo **Número** , clique em **Moeda**. As células são alteradas para mostrar a moeda formatada.  
  
     Se a configuração regional for Inglês (Estados Unidos), o texto de exemplo padrão será [**$12,345.00**]. Se você não vir um valor de moeda de exemplo, clique em **estilos de espaço reservado** na **números** agrupar e, em seguida, clique em **valores de exemplo**.  
  
4.  Clique na célula que contém `[SalesDate]`.  
  
5.  No **número** grupo, na lista suspensa, selecione **data**.  
  
     A célula exibe a data de exemplo **[1/31/2000]**. Se uma data de exemplo não estiver visível, clique em **Estilos de Espaço Reservado** no grupo **Números** e clique em **Valores de Exemplo**.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
 Os valores de data só exibem datas e os valores de vendas são exibidos como moeda.  
  
##  <a name="AdjacentGroup"></a> 4. Adicionar grupo de colunas adjacente  
 É possível aninhar grupos de linhas e de colunas em relações de pai e filho ou adjacentes em relações de irmão.  
  
 Adicione um grupo de colunas adjacente ao grupo de colunas Subcategory, copie células para popular o novo grupo de colunas e, em seguida, use uma expressão para criar o valor do cabeçalho do grupo de colunas.  
  
#### <a name="to-add-an-adjacent-column-group"></a>Para adicionar um grupo de colunas adjacente  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique com o botão direito do mouse na célula que contém `[Subcategory]`, aponte para **Adicionar Grupo**e clique em **Adjacente à Direita**.  
  
     A caixa de diálogo **Grupo Tablix** é aberta.  
  
3.  Na lista **Agrupar Por** , selecione SalesDate e clique em **OK**.  
  
     Um novo grupo de colunas é adicionado à esquerda do grupo de colunas Subcategory.  
  
4.  Clique com o botão direito do mouse na célula do novo grupo de colunas que contém `[SalesDate],` e clique em **Expressão**.  
  
5.  Copie a expressão a seguir para a caixa Expressão.  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
     Essa expressão extrai o nome do dia da semana da data das vendas. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md).  
  
6.  Clique com o botão direito do mouse na célula do grupo de colunas Subcategory que contém Total e clique em **Copiar**.  
  
7.  Clique com o botão direito do mouse na célula logo abaixo da célula que contém a expressão criada na etapa 5 e clique em **Colar**.  
  
8.  Pressione a tecla Ctrl.  
  
9. No grupo Subcategory, clique no cabeçalho da coluna Sales e nas três células abaixo dela, clique com o botão direito do mouse nela e clique em **Copiar**.  
  
10. Cole as quatro células nas quatro células vazias do novo grupo de colunas.  
  
11. Clique em **Executar** para visualizar o relatório.  
  
 O relatório inclui colunas nomeadas Monday e Tuesday. O conjunto de dados contém apenas dados referentes a esses dois dias.  
  
> [!NOTE]  
>  Se os dados incluíssem outros dias, o relatório também incluiria colunas para eles. Cada coluna tem um cabeçalho de coluna, `Sales`e os totais de vendas por território.  
  
##  <a name="Width"></a> 5. Alterar a Largura das Colunas  
 Um relatório que inclua uma matriz normalmente se expande horizontalmente, bem como verticalmente, quando executado. O controle da expansão horizontal será especialmente importante se você planejar exportar o relatório para formatos como Microsoft Word ou Adobe PDF, usados em relatórios impressos. Se o relatório se expandir horizontalmente em várias páginas, será difícil compreender o relatório impresso. Para minimizar a expansão horizontal, é possível redimensionar colunas seguindo exclusivamente a largura necessária para exibir os dados sem quebra de texto. Também é possível renomear colunas para que os títulos se ajustem à largura necessária para exibir os dados.  
  
#### <a name="to-rename-and-resize-the-columns"></a>Para renomear e redimensionar as colunas  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Selecione o texto na coluna Quantity mais à esquerda e digite **QTY**.  
  
     O título da coluna agora é QTY.  
  
3.  Repita a etapa 2 para as outras colunas nomeadas Quantity. Há duas delas.  
  
4.  Clique na matriz para que os identificadores de coluna e de linha sejam exibidos acima e ao lado da matriz.  
  
     As barras em cinza ao longo da parte superior e ao lado da tabela são os identificadores de coluna e de linha.  
  
5.  Para redimensionar a coluna QTY mais à esquerda, aponte para a linha entre os identificadores de coluna de forma que o cursor seja alterado para uma seta dupla. Arraste a coluna para a esquerda até que ela tenha 1,27 centímetros de largura.  
  
     Uma largura da coluna de 1,27 centímetros é suficiente para exibir a quantidade.  
  
6.  Repita a etapa 5 para as outras colunas nomeadas QTY.  
  
7.  Clique em **Executar** para visualizar o relatório.  
  
 As colunas no relatório que contenha quantidades agora são nomeadas QTY e estão mais estreitas.  
  
##  <a name="MergeCells"></a> 6. Mesclar células na matriz  
 A área de canto está no canto superior esquerdo da matriz. Dependendo do número de grupos de linhas e de colunas na matriz, o número de células na área de canto varia. A matriz, interna neste tutorial, tem quatro células na área de canto. As células são organizadas em duas linhas e duas colunas, o que reflete a profundidade das hierarquias dos grupos de linhas e de colunas. As quatro células não são usadas neste relatório, e você as mesclará em uma só.  
  
#### <a name="to-merge-matrix-cells"></a>Para mesclar células na matriz  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na matriz para que os identificadores de coluna e de linha sejam exibidos acima e ao lado da matriz.  
  
3.  Pressione a tecla Ctrl e, em seguida, selecione as quatro células de canto.  
  
4.  As células com o botão direito e, em seguida, clique em **mesclar células**.  
  
5.  Clique com botão direito na célula de canto e, em seguida, clique em **propriedades da caixa de texto**.  
  
6.  Clique na guia **Preenchimento** .  
  
7.  Clique o (***fx***) botão **cor de preenchimento**.  
  
8.  Copie e cole a expressão a seguir na caixa de expressão.  
  
    ```  
    #96a4b2  
    ```  
  
     Trata-se do valor hexadecimal RGB de uma cor azul acinzentada usada no estilo Ardósia.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Clique em **Executar** para visualizar o relatório.  
  
 A matriz de canto superior é uma única célula e tem a mesma cor das células dos grupos de linhas e de colunas.  
  
##  <a name="HeaderTitle"></a> 7. Adicionar um cabeçalho e um título de relatório  
 Um título é exibido na parte superior do relatório. É possível colocar o título em um cabeçalho do relatório. No entanto, se ele não usar um cabeçalho, será possível colocar o título em uma caixa de texto na parte superior do corpo do relatório. Neste tutorial, você irá remover a caixa de texto na parte superior do relatório e adicionar um título ao cabeçalho.  
  
#### <a name="to-add-a-report-header-and-report-title"></a>Para adicionar um cabeçalho e um título de relatório  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na caixa de texto na parte superior do corpo do relatório que contém **clique para adicionar título**, em seguida, pressione a tecla Delete.  
  
3.  Sobre o **inserir** guia de faixa de opções, clique em **cabeçalho** e, em seguida, clique em **Adicionar cabeçalho**.  
  
     Um cabeçalho é adicionado à parte superior do corpo do relatório.  
  
4.  Na guia **Inserir** , clique em **Caixa de Texto**e arraste uma caixa de texto para dentro do cabeçalho do relatório. Crie a caixa de texto com 15,24 centímetros de comprimento e 1,90 centímetros de altura e posicione-a no lado esquerdo do cabeçalho do relatório.  
  
5.  Na caixa de texto, digite **Vendas por Região, Subcategoria e Dia**.  
  
6.  Selecione o texto que você digitou, clique com botão direito e depois clique em **propriedades de texto**.  
  
    > [!NOTE]  
    >  Para formatar caracteres simultaneamente, eles devem ser contíguos.  
  
7.  No **propriedades de texto** caixa de diálogo, clique em **fonte**.  
  
8.  No **Font** lista, selecione **Times New Roman**; na **tamanho** selecione **24 pt**, na **cor** selecione  **Bordô**e, na **estilo** selecionar **itálico**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Clique em **Executar** para visualizar o relatório.  
  
 O relatório inclui um título do relatório no cabeçalho do relatório.  
  
##  <a name="Save"></a> 8. Salvar o relatório  
 É possível salvar relatórios em um servidor de relatório, em uma biblioteca do SharePoint ou no computador.  
  
 Neste tutorial, salve o relatório em um servidor de relatório. Se você não tiver acesso ao servidor de relatório, salve o relatório no computador.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
     A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for estabelecida, você verá o conteúdo da pasta de relatório que o administrador do servidor de relatório especificou como o local de relatório padrão.  
  
4.  Em **Nome**, substitua o nome padrão por **SalesByTerritorySubcategory**.  
  
5.  Clique em **Salvar**.  
  
 O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu Computador**e, em seguida, navegue até a pasta na qual você deseja salvar o relatório.  
  
3.  Em **Nome**, substitua o nome padrão por **SalesByTerritorySubcategory**.  
  
4.  Clique em **Salvar**.  
  
##  <a name="RotateTextBox"></a> 9. (Opcional) Girar caixa de texto em 270 graus  
 Um relatório com matrizes pode se expandir horizontal e verticalmente quando executado. Girando-se caixas de texto verticalmente, ou em 270 graus, é possível economizar espaço horizontal. Em seguida, o relatório renderizado é estreitado e, se exportado para um formato como o Microsoft Word, será mais provável o ajuste em uma página impressa.  
  
 Uma caixa de texto também pode exibir texto na horizontal, vertical (de cima para baixo). Para obter mais informações, consulte [Caixas de texto &#40;Construtor de Relatórios e SSRS&#41;](report-design/text-boxes-report-builder-and-ssrs.md).  
  
#### <a name="to-rotate-text-box-270-degrees"></a>Para girar caixa de texto em 270 graus  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na célula que contenha `[Territory].`  
  
3.  No painel Propriedades, localize a propriedade WritingMode e na lista suspensa, selecione **Rotate270**.  
  
     Se o painel Propriedades não estiver aberto, clique na guia **Exibir** da faixa de opções e selecione **Propriedades**.  
  
4.  Verificar se a propriedade CanGrow está definida como `True`.  
  
5.  Redimensione a coluna Territory para ter 1,27 centímetro de largura e exclua o título da coluna.  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
 O nome de território é escrito verticalmente, de baixo para cima. A altura do grupo de linhas Territory varia de acordo com o tamanho do nome do território.  
  
## <a name="next-steps"></a>Próximas etapas  
 Isso conclui o tutorial sobre como criar um relatório de matriz. Para obter mais informações sobre matrizes, consulte [tabelas, matrizes e listas de &#40;construtor de relatórios e SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md), [matrizes &#40;construtor de relatórios e SSRS&#41;](report-design/create-a-matrix-report-builder-and-ssrs.md), [ Áreas da região de dados Tablix &#40;relatórios e SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md), e [células da região de dados Tablix, linhas e colunas &#40;construtor de relatórios&#41; e o SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
