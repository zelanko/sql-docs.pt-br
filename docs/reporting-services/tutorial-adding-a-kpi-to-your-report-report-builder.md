---
title: 'Tutorial: Adicionando um KPI ao relatório (Construtor de Relatórios) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee2333bc6d369bbc9908198d8cfa2fa18ce23065
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63041741"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>Tutorial: adicionando um KPI ao relatório (Construtor de Relatórios)
Neste tutorial do [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)], você adiciona um KPI (indicador chave de desempenho) a um relatório paginado do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)].  

Os KPIs são valores mensuráveis com importância comercial. Nesse cenário, o resumo das vendas por subcategorias de produto é o KPI. O estado atual do KPI é mostrado com cores, medidores e indicadores.
  
A ilustração a seguir é semelhante ao relatório que você criará.  
  
![report-builder-kpi-report](../reporting-services/media/report-builder-kpi-report.png)
    
> [!NOTE]  
> Neste tutorial, as etapas do assistente são consolidadas em dois procedimentos: um para criar o conjunto de dados e um para criar uma tabela. Para obter instruções passo a passo sobre como procurar um servidor de relatório, escolher uma fonte de dados, criar um conjunto de dados e executar o assistente, consulte o primeiro tutorial desta série: [Tutorial: Criação de um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo estimado para concluir este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Table"></a>1. Criar um relatório de tabela e conjunto de dados no Assistente de Tabela ou Matriz  
Nesta seção, você escolhe uma fonte de dados compartilhada, cria um conjunto de dados inserido e exibe os dados em uma tabela.  
 
### <a name="to-create-a-table-with-an-embedded-dataset"></a>Para criar uma tabela com um conjunto de dados inserido  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Tabela ou Matriz**.  
  
4.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados**.  
  
5.  Clique em **Próximo**.  
  
6.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou procure o servidor de relatório e selecione uma fonte de dados. Se não houver nenhuma fonte de dados disponível ou se você não tiver acesso a um servidor de relatório, será possível usar uma fonte de dados inserida. Para obter mais informações, consulte [Tutorial: Criando um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Clique em **Próximo**.  
  
8.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
9. Copie e cole a seguinte consulta no painel de consulta:  

    > [!NOTE]  
    > Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. Na barra de ferramentas do designer de consultas, clique em Executar ( **!** ).

11. Clique em **Próximo**.  
  
## <a name="CompleteWizard"></a>2. Organizar dados e escolher o layout no Assistente  
O Assistente de Tabela ou Matriz fornece um design inicial no qual os dados serão exibidos. O painel de visualização no assistente ajuda a visualizar o resultado do agrupamento de dados antes de concluir o design da tabela ou da matriz.  
  
### <a name="to-organize-data-into-groups-and-choose-a-layout"></a>Para organizar dados em grupos e escolher um layout 
  
1.  Na página Organizar campos, arraste Product até **Valores**.  
  
2.  Arraste Quantity até **Values** e coloque-o abaixo de Product.  
  
    O campo Quantity é resumido com a função Sum, a função padrão para resumir campos numéricos.  
  
3.  Arraste Sales até **Valores** e coloque-o abaixo de Quantity.  
  
    As etapas 1, 2 e 3 especificam os dados a serem exibidos na tabela.  
  
4.  Arraste SalesDate até **Grupos de linhas**.  
  
5.  Arraste Subcategory até **Grupos de linhas** e coloque-o abaixo de SalesDate.  
  
    As etapas 4 e 5 organizam os valores dos campos primeiro por data e depois por todas as vendas nessa data.  
  
6.  Clique em **Próximo**.  
  
    Quando você executar o relatório, a tabela exibirá cada data, todas as ordens de cada data e todos os produtos, quantidades e totais de vendas de cada pedido.  
  
7.  Na página Escolher o Layout, em **Opções**, verifique se a opção **Mostrar subtotais e totais gerais** está selecionada.  
  
8.  Verifique se a opção **Bloqueado, subtotal abaixo** está selecionada.  
  
9. Desmarque a opção **Expandir/recolher grupos**.  
  
    Neste tutorial, o relatório criado não usa o recurso de detalhamento que permite a um usuário expandir uma hierarquia de grupo pai para exibir linhas de grupo filho e linhas de detalhes.  
  
10. Clique em **Próximo**.  
  
11. Clique em **Concluir**.  
  
      A tabela é adicionada à superfície de design. A tabela tem cinco colunas e cinco linhas. O painel Grupos de Linhas mostra três grupos de linhas: SalesDate, Subcategory e Details. Os dados detalhados são todos os dados recuperados pela consulta do conjunto de dados. O painel Grupos de Colunas está vazio.  
      
      ![report-builder-kpi-row-groups](../reporting-services/media/report-builder-kpi-row-groups.png)
  
12. Clique em **Executar** para visualizar o relatório.  
  
Para cada produto vendido em uma data específica, a tabela exibe o nome do produto, a quantidade vendida e o total da venda. Os dados são organizados primeiro pela data da venda e depois pela subcategoria. 

![report-builder-kpi-basic-table](../reporting-services/media/report-builder-kpi-basic-table.png)
    
### <a name="format-dates-and-currency"></a>Formatar datas e moeda
Vamos aumentar a largura das colunas e definir o formato para as datas e a moeda.

1. Clique em **Design** para voltar para o modo Design.

2. Os nomes de Produto poderão usar mais espaço. Para aumentar a largura da coluna Produto, selecione a tabela inteira e arraste a borda direita da alça da colunas na parte superior da coluna Produto.

3. Pressione a tecla Ctrl e selecione as quatro células que contêm [Sum(Sales)].

4. Na guia **Início** > **Número** > **Moeda**. As células são alteradas para mostrar a moeda formatada.

   Se a configuração regional for Inglês (Estados Unidos), o texto de exemplo padrão será [$12,345.00]. Se um valor de moeda de exemplo não estiver visível, no grupo **Números** , clique em **Estilos de Espaço Reservado** > **Valores de Exemplo**.
    
    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)

5. (Opcional) Na guia **Início** , no grupo **Número** , clique no botão **Diminuir Decimais** duas vezes para exibir valores em dólares sem centavos.

6. Clique na célula que contém [SalesDate].

6. No grupo **Número** > **Data**.

   A célula exibe a data de exemplo [1/31/2000]. 

12. Clique em **Executar** para visualizar o relatório.  
 
![report-builder-kpi-format-numbers](../reporting-services/media/report-builder-kpi-format-numbers.png)

## <a name="BackgroundColors"></a>3. Usar cores do plano de fundo para exibir um KPI  
As cores do plano de fundo podem ser definidas como uma expressão avaliada quando você executa o relatório.  
  
### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>Para exibir o estado atual de um KPI usando cores de plano de fundo  
  
1.  Na tabela, clique com o botão direito do mouse na segunda célula `[Sum(Sales)]` (a linha do subtotal que exibe as vendas de uma subcategoria) e clique em **Propriedades da Caixa de Texto**. 

    Verifique se você selecionou a célula, não o texto na célula, para exibir **Propriedades da Caixa de Texto**. 
    
    ![report-builder-text-box-properties](../reporting-services/media/report-builder-text-box-properties.png)
  
2.  Em **Preencher** , clique no botão **fx** ao lado da opção **Cor de preenchimento** e insira a seguinte expressão no campo **Definir expressão para: BackgroundColor** :  
  
    `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
     Isso altera a cor da tela de fundo para “Verde-limão” de cada célula com uma soma agregada de `[Sum(Sales)]` maior ou igual a 5.000. Valores de `[Sum(Sales)]` entre 2.500 e 5.000 são “Amarelo”. Valores menores que 2.500 são “Vermelho”.  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  Clique em **Executar** para visualizar o relatório.  
  
Na linha de subtotal que exibe as vendas de uma subcategoria, a cor do plano de fundo da célula é vermelha, amarela ou verde, dependendo da soma das vendas.  

![report-builder-kpi-colors](../reporting-services/media/report-builder-kpi-colors.png)
  
## <a name="Gauge"></a>4. Exibir um KPI usando um medidor  
Um medidor representa um único valor em um conjunto de dados. Este tutorial usa um medidor linear horizontal porque sua forma e simplicidade facilitam a leitura, mesmo quando é menor e usado em uma célula da tabela. Para obter mais informações, consulte [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>Para exibir o estado presente de um KPI que usa um medidor  
  
1.  Mude novamente para o modo Design.  
  
2.  Na tabela, clique com o botão direito do mouse na alça da coluna Sales > **Inserir Coluna** > **Direita**. Uma nova coluna é adicionada à tabela.  

    ![report-builder-kpi-insert-column](../reporting-services/media/report-builder-kpi-insert-column.png)
  
3.  Digite **KPI Linear** no título de coluna.  
  
4.  Na guia **Inserir** > **Visualizações de Dados** > **Medidor** e, em seguida, clique na área de design fora da tabela.   
  
5.  Na caixa de diálogo **Selecionar Tipo de Medidor** , selecione o primeiro tipo de medidor linear, **Horizontal**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Um medidor é adicionado à superfície de design.  
  
7.  No conjunto de dados no painel Dados do Relatório, arraste o campo `Sales` até o medidor. O painel **Dados do Medidor** é exibido.  
  
    Quando você solta o campo `Sales` no medidor, o campo é inserido na lista **Valores** e é agregado por meio da função Sum interna.  
   
    ![report-builder-kpi-drag-sales-field](../reporting-services/media/report-builder-kpi-drag-sales-field.png)
   
9. No painel **Dados do Medidor** , clique na seta ao lado de **LinearPointer1** > **Propriedades do Ponteiro**.  
  
10. Na caixa de diálogo **Propriedades do Ponteiro Linear** > guia **Opções de Ponteiro** > **Tipo de Ponteiro**, verifique se a opção **Barra** está selecionada. 
 
11. Clique em **OK**.  
  
12. Clique com o botão direito do mouse na escala do medidor e clique em **Propriedades da Escala**.  
  
13. Na caixa de diálogo **Propriedades da Escala Linear** > guia **Geral**, defina **Máximo** como 25.000.  

    > [!NOTE]  
    > Em vez de uma constante como 25.000, é possível usar uma expressão para calcular dinamicamente o valor da opção **Máximo** . A expressão usaria a agregação do recurso de agregação e semelhante à expressão `=Max(Sum(Fields!Sales.value), "Tablix1")`.  

14. Na guia **Rótulos** , marque **Ocultar rótulos de escala**.

15. Clique em **OK**.
  
14. Arraste o medidor na tabela até a segunda célula vazia na coluna KPI Linear, na linha que exibe o subtotal de vendas do campo `Subcategory` , ao lado do campo ao qual você adicionou a fórmula de cor da tela de fundo.  
  
    > [!NOTE]  
    > Talvez você precise redimensionar a coluna para que o medidor linear horizontal se ajuste à célula. Para redimensionar a coluna, selecione a tabela e arraste as alças da coluna. A superfície de design do relatório é redimensionada para se ajustar à tabela.  
  
15. Clique em **Executar** para visualizar o relatório.  
  
    O comprimento horizontal da barra verde no medidor é alterado de acordo com o valor do KPI.  
  
![report-builder-linear-kpi](../reporting-services/media/report-builder-linear-kpi.png) 
  
## <a name="Indicator"></a>5. Exibir um KPI usando um indicador  
Indicadores são medidores pequenos e simples que comunicam valores de dados em um relance. Por conta de seu tamanho e simplicidade, os indicadores costumam ser usados em tabelas e matrizes. Para obter mais informações, consulte [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>Para exibir o estado atual de um KPI usando um indicador  
  
1.  Alterne para o modo Design.  
  
2.  Na tabela, clique com o botão direito do mouse na alça da coluna KPI Linear que você adicionou no último procedimento > **Inserir Coluna** > **Direita**. Uma nova coluna é adicionada à tabela.  
  
3.  Digite **KPI de Alerta** no título de coluna.  
  
4.  Clique na célula do subtotal da subcategoria, ao lado do medidor linear adicionado no último procedimento.  
  
5.  Na guia **Inserir** > **Visualizações de Dados** > clique duas vezes em **Indicador.**  
  
6.  Na caixa de diálogo **Selecionar Tipo de Indicador** , em **Formas**, selecione o primeiro tipo de forma, **3 Semáforos (Não Coroados)** .  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    O indicador é adicionado à célula na nova coluna KPI de Alerta.  
  
8.  Clique com o botão direito do mouse no indicador e clique em **Propriedades do Indicador**.  
  
9. Na guia **Valores e Estados** , na caixa **Valor** , selecione **[Sum(Sales)]** . Não altere nenhuma outra opção.  
  
    Por padrão, a sincronização de dados ocorre na região de dados e o valor **Tablix1**, o nome da região de dados da tabela no relatório, é exibido na caixa **Escopo de sincronização** .  
  
    Nesse relatório, é possível alterar também o escopo de um indicador colocado na célula do subtotal da subcategoria para sincronização no campo SalesDate.  
  
11. Clique em **OK**.

11. Clique em **Executar** para visualizar o relatório.  

![report-builder-kpi-stoplight](../reporting-services/media/report-builder-kpi-stoplight.png)
  
## <a name="Title"></a>6. Adicionar um título de relatório  
Um título é exibido na parte superior do relatório. É possível colocar o título em um cabeçalho do relatório. No entanto, se ele não usar um cabeçalho, será possível colocar o título em uma caixa de texto na parte superior do corpo do relatório. Nesta seção, você usa a caixa de texto colocada automaticamente na parte superior do corpo do relatório.  
  
Você pode aprimorar o texto ainda mais com a aplicação de estilos, tamanhos e cores de fontes diferentes a frases e caracteres individuais do texto. Para obter mais informações, consulte [Formatar o texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **KPIs de Vendas de Produtos**e clique fora da caixa de texto.  
  
3.  Opcionalmente, clique com o botão direito do mouse na caixa de texto que contém **KPI de Vendas de Produtos**, clique em **Propriedades da Caixa de Texto**e, na guia Fonte, selecione estilos, tamanhos e cores de fontes diferentes.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
## <a name="Save"></a>7. Salvar o relatório  
Salve o relatório em um servidor de relatório ou no computador. Se você não salvar o relatório no servidor de relatório, vários recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como partes do relatório e sub-relatórios, não estarão disponíveis.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
    A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por **KPI de Vendas de Produtos**.  
  
5.  Clique em **Save** (Salvar).  
  
O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu computador**e procure a pasta na qual você quer salvar o relatório.  
  
> [!NOTE]  
> Se você não tiver acesso a um servidor de relatório, clique em **Área de Trabalho**, **Meus Documentos**ou **Meu computador** e salve o relatório no computador.  
  
1.  Em **Nome**, substitua o nome padrão por **KPI de Vendas de Produtos**.  
  
2.  Clique em **Save** (Salvar).  
  
## <a name="next-steps"></a>Próximas etapas  
Você completou com êxito o tutorial Adicionando um KPI ao relatório. Para obter mais informações, consulte:
*  [Medidores](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)
* [Indicadores](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte Também  
* [Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md)
* [Construtor de Relatórios no SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

