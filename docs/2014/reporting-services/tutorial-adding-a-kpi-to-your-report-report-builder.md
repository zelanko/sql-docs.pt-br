---
title: 'Tutorial: Adicionando um KPI ao relatório (construtor de relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5e00afd4954a328e767ccb2d991338d9dffb1dff
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296444"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>Tutorial: Adicionando um KPI ao relatório (construtor de relatórios)
  O KPI (indicador chave de desempenho) é um valor mensurável que tem importância comercial. Este tutorial ensina a incluir um KPI em um relatório. Nesse cenário, o resumo das vendas por subcategorias de produto é o KPI. O estado atual do KPI é mostrado usando-se cores e indicadores.  
  
 A ilustração a seguir mostra o relatório que você criará.  
  
 ![rs_AddKPITutorial](../../2014/tutorials/media/rs-addkpitutorial.gif "rs_AddKPITutorial")  
  
##  <a name="BackToTop"></a> O que você aprenderá  
 Neste tutorial, você aprenderá a adicionar um KPI definindo a cor do plano de fundo das células da tabela com base no valor da célula, além de adicionar e configurar um indicador. Você também aprende a escrever a expressão que define a cor do plano de fundo das células da tabela.  
  
 Este tutorial contém os seguintes procedimentos:  
  
1.  [Criar um relatório de tabela e o conjunto de dados do Assistente de tabela ou matriz](#Table)  
  
2.  [Organizar dados, escolher Layout e estilo de Assistente de tabela ou matriz](#CompleteWizard)  
  
3.  [Usar cores do plano de fundo para exibir um KPI](#BackgroundColors)  
  
4.  [Exibir um KPI usando um medidor](#Gauge)  
  
5.  [Exibir um KPI usando um indicador](#Indicator)  
  
6.  [Adicionar um título de relatório](#Title)  
  
7.  [Salvar o relatório](#Save)  
  
> [!NOTE]  
>  Neste tutorial, as etapas do assistente são consolidadas em dois procedimentos: um para criar o conjunto de dados e um para criar uma tabela. Para obter instruções passo a passo sobre como navegar até um servidor de relatório, escolher uma fonte de dados, criar um conjunto de dados e executar o assistente, consulte o primeiro tutorial nesta série: [Tutorial: Criando um relatório de tabela básica &#40;construtor de relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo estimado para concluir este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Table"></a> 1. Criar um relatório de tabela e conjunto de dados no Assistente de Tabela ou Matriz  
 Dos **guia de Introdução** caixa de diálogo, escolha uma fonte de dados, criar um conjunto de dados inserido e exibe os dados em uma tabela.  
  
> [!NOTE]  
>  Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-create-a-new-table"></a>Para criar uma tabela nova  
  
1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.  
  
     A caixa de diálogo **Guia de Introdução** é exibida.  
  
    > [!NOTE]  
    >  Se o **guia de Introdução** caixa de diálogo não aparece, no botão Construtor de relatórios, clique em **New**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Tabela ou Matriz**.  
  
4.  Na página Escolha um conjunto de dados, clique em **criar um conjunto de dados**.  
  
5.  Clique em **Avançar**.  
  
6.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou procure o servidor de relatório e selecione uma fonte de dados. Se não houver nenhuma fonte de dados disponível ou se você não tiver acesso a um servidor de relatório, será possível usar uma fonte de dados inserida. Para obter mais informações, consulte [Tutorial: Criando um relatório de tabela básica &#40;construtor de relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Clique em **Avançar**.  
  
8.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
9. Copie e cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
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
  
10. Clique em **Avançar**.  
  
##  <a name="CompleteWizard"></a> 2. Organizar dados, escolher layout e estilo no Assistente de Tabela ou Matriz  
 Use o assistente para fornecer um design inicial no qual exibir dados. O painel de visualização no assistente ajuda a visualizar o resultado do agrupamento de dados antes de concluir o design da tabela ou da matriz.  
  
#### <a name="to-organize-data-into-groups-choose-a-layout-and-a-style"></a>Para organizar dados em grupos, escolha um layout e um estilo  
  
1.  Na página Organizar campos, arraste Product até **Valores**.  
  
2.  Arraste Quantity até **Values** e coloque-o abaixo de Product.  
  
     O campo Quantity é resumido com a função Sum, a função padrão para resumir campos numéricos.  
  
3.  Arraste Sales até **Valores** e coloque-o abaixo de Quantity.  
  
     As etapas 1, 2 e 3 especificam os dados a serem exibidos na tabela.  
  
4.  Arraste SalesDate até **Grupos de linhas**.  
  
5.  Arraste Subcategory até **Grupos de linhas** e coloque-o abaixo de SalesDate.  
  
     As etapas 4 e 5 organizam os valores dos campos primeiro por data e depois por todas as vendas nessa data.  
  
6.  Clique em **Avançar**.  
  
     Quando você executar o relatório, a tabela exibirá cada data, todas as ordens de cada data e todos os produtos, quantidades e totais de vendas de cada pedido.  
  
7.  Na página Escolher o Layout, em **Opções**, verifique se a opção **Mostrar subtotais e totais gerais** está selecionada.  
  
8.  Verifique se a opção **Bloqueado, subtotal abaixo** está selecionada.  
  
9. Desmarque a opção **Expandir/recolher grupos**.  
  
     Neste tutorial, o relatório criado não usa o recurso de detalhamento que permite a um usuário expandir uma hierarquia de grupo pai para exibir linhas de grupo filho e linhas de detalhes.  
  
10. Clique em **Avançar**.  
  
11. Na página Escolher um Estilo, no painel Estilos, selecione um estilo.  
  
     A ilustração do relatório concluído mostra o relatório usando o estilo Oceano.  
  
12. Clique em **Concluir**.  
  
     A tabela é adicionada à superfície de design. A tabela tem cinco colunas e cinco linhas. O painel de grupos de linhas mostra três grupos de linhas: SalesDate, Subcategory e Details. Os dados detalhados são todos os dados recuperados pela consulta do conjunto de dados.  
  
13. Clique em **Executar** para visualizar o relatório.  
  
 Para cada produto vendido em uma data específica, a tabela exibe o nome do produto, a quantidade vendida e o total da venda. Os dados são organizados primeiro pela data da venda e depois pela subcategoria.  
  
##  <a name="BackgroundColors"></a> 3. Usar cores do plano de fundo para exibir um KPI  
 As cores do plano de fundo podem ser definidas como uma expressão avaliada quando você executa o relatório.  
  
#### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>Para exibir o estado atual de um KPI usando cores de plano de fundo  
  
1.  Na tabela, clique com botão direito duas células para baixo do `[Sum(Sales)]` célula (linha de subtotal que exibe as vendas de uma subcategoria) e depois clique em **propriedades da caixa de texto**.  
  
2.  No **preencher**, clique no **fx** lado de **cor de preenchimento** opção e digite a seguinte expressão no **definir expressão para: BackgroundColor** campo:  
  
 `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
 Isso altera a cor do plano de fundo para verde, usando a tonalidade de verde denominada "Verde-limão", para cada célula que contém uma soma agregada para `[Sum(Sales)]` maior ou igual a 5000. Os valores de `[Sum(Sales)]` entre 2500 e 5000 são coloridos de amarelo. Os valores menores que 2500 são coloridos de vermelho.  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  Clique em **Executar** para visualizar o relatório.  
  
 Na linha de subtotal que exibe as vendas de uma subcategoria, a cor do plano de fundo da célula é vermelha, amarela ou verde, dependendo da soma das vendas.  
  
##  <a name="Gauge"></a> 4. Exibir um KPI usando um medidor  
 Um medidor representa um único valor em um conjunto de dados. Este tutorial usa um medidor linear horizontal porque sua forma e simplicidade facilitam a leitura, mesmo quando menor e usado dentro de uma célula da tabela. Para obter mais informações, consulte [Medidores &#40;Construtor de Relatórios e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md).  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>Para exibir o estado presente de um KPI que usa um medidor  
  
1.  Alterne para o modo Design.  
  
2.  Na tabela, clique com botão direito no manipulador de coluna da célula que você alterou no procedimento anterior, aponte para **Inserir coluna**e, em seguida, clique em **direita**. Uma nova coluna é adicionada à tabela.  
  
3.  Tipo de **KPI** no título da coluna.  
  
4.  No **inserir** guia, o **regiões de dados** , clique em **medidor**e, em seguida, clique na superfície de design fora da tabela. A caixa de diálogo **Selecionar Tipo de Medidor** é exibida.  
  
5.  Clique em **Linear**. O primeiro tipo de medidor linear **Horizontal**, está selecionada.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Um medidor é adicionado à superfície de design.  
  
7.  No painel Dados do Relatório, arraste Sales para o indicador. Quando você arrasta Sales pelo indicador, o painel Dados do Medidor é aberto.  
  
8.  Solte Sales na **valores** lista.  
  
     Quando você solta o campo no medidor, o campo é agregado através da função Sum interna.  
  
9. Clique com botão direito do ponteiro no medidor e clique em **propriedades do ponteiro**.  
  
10. Na **tipo de ponteiro**, selecione **barra**. Isso altera o ponteiro de um marcador para uma barra que será mais visível quando o medidor for adicionado à tabela.  
  
11. Clique em **preenchimento do ponteiro**. Na **cor secundária** escolher **amarelo**. O padrão de preenchimento de gradiente mudará de branco para amarelo.  
  
12. Clique com o botão direito do mouse na escala do medidor e clique em **Propriedades da Escala**.  
  
13. Defina as **máximo** opção como 25000.  
  
    > [!NOTE]  
    >  Em vez de uma constante como 25.000, é possível usar uma expressão para calcular dinamicamente o valor da opção **Máximo** . A expressão usaria a agregação do recurso de agregação e semelhante à expressão `=Max(Sum(Fields!Sales.value), "Tablix1")`.  
  
14. Arraste o medidor dentro da tabela para a terceira célula na linha do subtotal que exibe as vendas de uma subcategoria da coluna que você inseriu.  
  
    > [!NOTE]  
    >  Talvez você precise redimensionar a coluna para que o medidor linear horizontal se ajuste à célula. Para redimensionar a coluna, clique em um cabeçalho de coluna e use as alças para redimensionar as células horizontal e verticalmente.  
  
15. Clique em **Executar** para visualizar o relatório.  
  
     O comprimento horizontal da barra no medidor é alterado de acordo com o valor do KPI.  
  
16. (Opcional) Adicione um pin máximo para resolver o estouro de forma que qualquer valor acima do máximo da escala sempre aponte para o pin máximo:  
  
    1.  Abra o painel Propriedades.  
  
    2.  Clique na escala. As propriedades da escala linear são exibidas no painel Propriedades.  
  
    3.  No **Pins da escala** categoria, expanda o **MaximumPin** nó.  
  
    4.  Defina a **habilitar** propriedade `True`. Um pin é exibido depois do valor de máximo na escala.  
  
    5.  Definir **BorderColor** para `Lime`.  
  
17. Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Indicator"></a> 5. Exibir um KPI usando um indicador  
 Indicadores são medidores pequenos e simples que comunicam valores de dados em um relance. Por conta de seu tamanho e simplicidade, os indicadores costumam ser usados em tabelas e matrizes. Para obter mais informações, consulte [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md).  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>Para exibir o estado atual de um KPI usando um indicador  
  
1.  Alterne para o modo Design.  
  
2.  Na tabela, clique com botão direito no manipulador de coluna da célula que você alterou no procedimento anterior, aponte para **Inserir coluna**e, em seguida, clique em **direita**. Uma nova coluna é adicionada à tabela.  
  
3.  Tipo de **KPI** no título da coluna.  
  
4.  Clique na célula do subtotal da subcategoria.  
  
5.  No **inserir** guia, o **regiões de dados** agrupar, clique duas vezes em **indicador.**  
  
     A caixa de diálogo **Selecionar Tipo de Indicador** será aberta.  
  
6.  Clique em **formas**. O primeiro tipo de forma **3 semáforos (não Coroados),** está selecionado.  
  
     Você usará esse indicador no tutorial.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     O indicador é adicionado à superfície de design.  
  
8.  Clique com o botão direito do mouse no indicador e clique em **Propriedades do Indicador**.  
  
9. Clique em **valores e estados**.  
  
10. Na lista suspensa de valores, selecione **[SUM (Sales)]**, mas não altere nenhuma outra opção.  
  
     Por padrão, a sincronização de dados ocorre na região de dados e o valor **Tablix1**, o nome da região de dados da tabela no relatório, é exibido na caixa **Escopo de sincronização** .  
  
     Nesse relatório, é possível alterar também o escopo de um indicador colocado na célula do subtotal da subcategoria para sincronização no campo SalesDate.  
  
11. Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Title"></a> 6. Adicionar um título de relatório  
 Um título é exibido na parte superior do relatório. É possível colocar o título em um cabeçalho do relatório. No entanto, se ele não usar um cabeçalho, será possível colocar o título em uma caixa de texto na parte superior do corpo do relatório. Você usará a caixa de texto colocada automaticamente na parte superior do corpo do relatório.  
  
 O texto pode ser aprimorado ainda mais aplicando-se estilos, tamanhos e cores de fontes diferentes a frases e caracteres individuais do texto. Para obter mais informações, consulte [Formatar o texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Tipo de **KPI de vendas do produto**e, em seguida, clique fora da caixa de texto.  
  
3.  Opcionalmente, clique com botão direito a caixa de texto que contém **KPI de vendas do produto**, clique em **propriedades da caixa de texto**e, em seguida, na guia fonte, selecione os estilos de fontes diferentes, tamanhos e cores.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
##  <a name="Save"></a> 7. Salvar o relatório  
 Salve o relatório em um servidor de relatório ou no computador. Se você não salvar o relatório no servidor de relatório, vários recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como partes do relatório e sub-relatórios, não estarão disponíveis.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
     A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por **KPI de Vendas de Produtos**.  
  
5.  Clique em **Salvar**.  
  
 O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu computador**e procure a pasta na qual você quer salvar o relatório.  
  
> [!NOTE]  
>  Se você não tiver acesso a um servidor de relatório, clique em **Área de Trabalho**, **Meus Documentos**ou **Meu computador** e salve o relatório no computador.  
  
1.  Em **Nome**, substitua o nome padrão por **KPI de Vendas de Produtos**.  
  
2.  Clique em **Salvar**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você completou com êxito o tutorial Adicionando um KPI ao relatório. Para obter mais informações, consulte medidores (construtor de relatórios) [indicadores &#40;construtor de relatórios e SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
