---
title: 'Tutorial: Criando um relatório de formato livre (Construtor de Relatórios) | Microsoft Docs'
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 249025217a11483d1538c7fe0c72ee1cf0832f3d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717244"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>Tutorial: criando um relatório de formato livre (Construtor de Relatórios)
Neste tutorial, você cria um relatório paginado que atua como um boletim informativo. Cada página exibe um texto estático, visuais de resumo e dados de vendas de exemplo detalhados.

![report-builder-free-form-report-complete](../reporting-services/media/report-builder-free-form-report-complete.png)

O relatório agrupa informações por território e exibe o nome do gerente de vendas do território, bem como informações detalhadas e resumidas sobre as vendas. Você começa com uma região de dados da lista como a base do relatório de forma livre e adiciona um painel decorativo com uma imagem, um texto estático com dados inseridos, uma tabela para mostrar informações detalhadas e, opcionalmente, gráficos de pizza e de colunas para exibir informações resumidas.  
  
Tempo estimado para concluir este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="BlankReport"></a>1. Criar um relatório em branco, uma fonte de dados e um conjunto de dados  
  
> [!NOTE]  
> Neste tutorial, como contém os valores de dados, a consulta não precisa de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
### <a name="to-create-a-blank-report"></a>Para criar um relatório em branco  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
  
2.  No painel esquerdo, verifique se a opção **Novo Relatório** está selecionada. 
 
3.  No painel direito, clique em **Relatório em Branco**.  
  
### <a name="to-create-a-new-data-source"></a>Para criar uma nova fonte de dados  
  
1.  No painel Dados do Relatório, clique em **Nova** > **Fonte de Dados**.  
  
2.  Na caixa **Nome** , digite: **ListDataSource**  
  
3.  Clique em **Usar uma conexão inserida no meu relatório**.  
  
4.  Verifique se o tipo de conexão é Microsoft SQL Server e, em seguida, na caixa **Cadeia de conexão**, digite: **Fonte de Dados = \<servername>**  
  
    **\<servername>**, por exemplo, Report001, especifica um computador no qual há uma instância do Mecanismo de Banco de Dados do SQL Server instalada. Como os dados deste relatório não são extraídos de um banco de dados SQL Server, você não precisa incluir o nome de um banco de dados. O banco de dados padrão no servidor especificado é usado apenas para analisar a consulta.  
  
5.  Clique em **Credenciais**e insira as credenciais necessárias para conexão à instância do Mecanismo de Banco de Dados do SQL Server.  
  
6.  Clique em **OK**.  
  
### <a name="to-create-a-new-dataset"></a>Para criar um novo conjunto de dados  
  
1.  No painel Dados do Relatório, clique em **Novo** > **Conjunto de Dados**.  
  
2.  Na caixa **Nome** , digite: **ListDataset**.  
  
3.  Clique em **Usar um conjunto de dados inserido em meu relatório**e verifique se a fonte de dados é **ListDataSource**.  
  
4.  Verifique se o tipo de consulta **Texto** está selecionado e, em seguida, clique em **Designer de Consulta**.  
  
5.  Clique em **Editar como Texto**.  
  
6.  Copie e cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
7.  Clique no ícone **Executar** (!) para executar a consulta.  
  
    Os resultados da consulta são os dados disponíveis a serem exibidos no relatório.  
  
    ![report-builder-free-form-tutorial-data](../reporting-services/media/report-builder-free-form-tutorial-data.png) 
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="List"></a>2. Adicionar e configurar uma lista  
No [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , a região de dados da lista é ideal para criar relatórios de forma livre. Ela se baseia na região de dados *tablix* , assim como tabelas e matrizes. Para obter mais informações, consulte [Criar faturas e formulários com listas](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
Você usará uma lista para exibir as informações de vendas das regiões de vendas em um relatório formatado como um boletim informativo. As informações são agrupadas por território. Você irá adicionar um novo grupo de linhas que reúne dados por território e, em seguida, excluir o grupo de linhas interno Detalhes.  
  
### <a name="to-add-a-list"></a>Para adicionar uma lista  
  
1.  Na guia **Inserir** > **Regiões de Dados** > **Lista**. 

2. Clique no corpo do relatório (entre as áreas do título e do rodapé) e arraste para criar a caixa de listagem. Crie a caixa de listagem com cerca de 18 centímetros de altura e 16 centímetros de largura. Para obter o tamanho exato, no painel **Propriedades** , em **Posição**, digite valores para as propriedades **Largura** e **Altura** .
  
    > [!NOTE]  
    > Esse relatório usa o tamanho de papel Carta (21,6 X 27,9) e margens de 2,54 centímetros. Uma caixa de listagem com mais de 23 centímetros de altura ou mais de 16 centímetros de largura pode gerar páginas em branco.  
  
2.  Clique dentro da caixa de listagem, clique com o botão direito do mouse na barra, na parte superior da lista, e clique em **Propriedades do Tablix**.  
  
    ![report-builder-free-form-tablix-properties](../reporting-services/media/report-builder-free-form-tablix-properties.png) 
  
3.  Na lista suspensa **Nome do conjunto de dados** , selecione **ListDataset**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Clique com o botão direito do mouse na lista e clique em **Propriedades do Retângulo**.  
  
6.  Na guia **Geral** , marque a caixa de seleção **Adicionar uma quebra de página após** .  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>Para adicionar um novo grupo de linhas e excluir o grupo Detalhes  
  
1.  No painel Grupos de Linhas, clique com o botão direito do mouse no grupo Detalhes, aponte para **Adicionar Grupo**e clique em **Grupo Pai**.  
  
    ![report-builder-free-form-add-parent-group](../reporting-services/media/report-builder-free-form-add-parent-group.png)  
  
2.  Na lista **Agrupar por** , selecione `[Territory].`  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Uma coluna que contém a célula `[Territory]` é adicionada à lista.
  
4.  Clique com o botão direito do mouse na coluna Territory da lista e clique em **Excluir Colunas**.  
  
    ![report-builder-free-form-delete-columns](../reporting-services/media/report-builder-free-form-delete-columns.png)
  
5.  Selecione **Excluir somente colunas**.  
  
6.  No painel Grupos de Linhas, clique com o botão direito do mouse no grupo **Detalhes** > **Excluir Grupo**.  
   
7.  Clique em **Excluir somente grupo**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Graphics"></a>3. Adicionar elementos gráficos  
Uma das vantagens de usar uma região de dados da lista é que você pode adicionar itens de relatório como retângulos e caixas de texto em qualquer lugar, em vez de estar limitado a um layout de tabela. Você aprimorará a aparência do relatório, adicionando um gráfico (um retângulo preenchido com uma cor).  
  
### <a name="to-add-graphic-elements-to-the-report"></a>Para adicionar elementos gráficos ao relatório  
  
1.  Na guia **Inserir** , selecione **Retângulo**. 

2. Clique no canto superior esquerdo da lista e arraste para criar o retângulo com 17,78 centímetros de altura e 8,89 centímetros de largura. Novamente, para obter o tamanho exato, no painel **Propriedades** , em **Posição**, digite valores para **Largura** e **Altura**.
  
2.  Clique com o botão direito do mouse no retângulo > **Propriedades do Retângulo**.  
  
3.  Clique na guia **Preenchimento** .  
  
4.  Em **Cor de preenchimento**, selecione **Cinza-claro**.  
   
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
O lado esquerdo do relatório agora tem um gráfico vertical que consiste em um retângulo cinza-claro, conforme mostrado na imagem a seguir.  
  
![report-builder-free-form-gray-rectangle](../reporting-services/media/report-builder-free-form-gray-rectangle.png)
 
## <a name="Text"></a>4. Adicionar texto de formato livre  
Você pode adicionar caixas de texto para exibir um texto estático que é repetido em cada página de relatório, bem como campos de dados.  
  
### <a name="to-add-text-to-the-report"></a>Para adicionar texto ao relatório  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Na guia **Inserir** > **Caixa de Texto**. Clique no canto superior esquerdo da lista, dentro do retângulo que você adicionou anteriormente, e arraste para criar a caixa de texto com 9,76 centímetros de largura e 12,70 centímetros de altura.  
  
3.  Com o cursor na caixa de texto, digite: **Boletim informativo para** . Inclua um espaço após a palavra “para”, para separar o texto do campo que será adicionado na próxima etapa.   
  
    ![Adicionar texto do cabeçalho do boletim informativo](../reporting-services/media/tutorial-newsletterfor.png "Adicionar texto do cabeçalho do boletim informativo")  
  
4.  Arraste o campo `[Territory]` de ListDataSet no painel Dados do Relatório até a caixa de texto e coloque-o após “Boletim informativo para”.  
  
    ![report-builder-free-form-territory-field](../reporting-services/media/report-builder-free-form-territory-field.png)
  
5.  Selecione o texto e o campo `[Territory]` .  
  
6.  Na guia **Início** > **Fonte**, selecione: 
  
    *  **Segoe Semibold**.
    *  **20 pt**.
    *  **Tomate**.  
  
9. Coloque o cursor abaixo do texto que você digitou na etapa 3 e digite: **Hello** com um espaço após a palavra para separar o texto e o campo que será adicionado na próxima etapa.  
 
10. Arraste o campo `[FullName]` de ListDataSet no painel Dados do Relatório até a caixa de texto, coloque-o após “Hello”, e digite uma vírgula (,).  
   
11. Selecione o texto que você adicionou nas etapas anteriores.
  
12. Na guia **Início** > **Fonte**, selecione: 
  
    *  **Segoe Semibold**.
    *  **16 pt**.
    *  **Black**.  
   
15. Coloque o cursor abaixo do texto que você adicionou nas etapas 9 a 13 e copie e cole o seguinte texto sem sentido:  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. 
    Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. 
    Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
 
    ```  
  
16. Selecione o texto que você acabou de adicionar.  
  
17.  Na guia **Início** > **Fonte**, selecione: 
  
      *  **Interface do usuário do Segoe**.
      *  **10 pt**.
      *  **Black**.  
 
20. Coloque o cursor dentro da caixa de texto, abaixo do texto sem sentido e digite: **Parabéns pelo seu total de vendas de**, com um espaço após a palavra para separar o texto e o campo que será adicionado na próxima etapa. 
  
21. Arraste o campo Sales até a caixa de texto, coloque-o depois do texto que você digitou na etapa anterior e digite um ponto de exclamação (!).  

25. Selecione o texto e o campo que você acabou de adicionar.  
  
17.  Na guia **Início** > **Fonte**, selecione: 
  
      *  **Segoe Semibold**.
      *  **16 pt**.
      *  **Black**.  
  
22. Selecione apenas o campo `[Sales]`, clique com o botão direito do mouse no campo > **Expressão**.  
  
23. Na caixa **Expressão** , altere a expressão para incluir a função Sum da seguinte forma:  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    ![report-builder-free-form-text-box](../reporting-services/media/report-builder-free-form-text-box.png)
 
29. Com `[Sum(Sales)]` ainda selecionado, na guia **Início** > grupo **Número** > **Moeda**.  
  
30. Clique com o botão direito do mouse na caixa de texto com o texto “Clique para adicionar título” e clique em **Excluir**.  
  
31. Selecione a caixa de listagem. Selecione as duas setas com duas pontas e mova-as para a parte superior da página.  

    ![report-builder-drag-list](../reporting-services/media/report-builder-drag-list.png)
  
32. Clique em **Executar** para visualizar o relatório.  
  
O relatório exibe texto estático e cada página de relatório inclui dados pertencentes a um território. As vendas são formatadas como moeda.  
  
![report-builder-newsletter-page-preview](../reporting-services/media/report-builder-newsletter-page-preview.png)
  
## <a name="Table"></a>5. Adicionar uma tabela para mostrar detalhes de vendas  
Use o Assistente de Nova Tabela e Matriz para adicionar uma tabela ao relatório de formato livre. Depois de concluir o assistente, você adicionará manualmente uma linha para totais.  
  
### <a name="to-add-a-table"></a>Para adicionar uma tabela  
  
1.  Na guia **Inserir** > área **Regiões de Dados** > **Tabela** > **Assistente de Tabela**.  
  
2.  Na página **Escolher um conjunto de dados** , clique em **ListDataset** > **Avançar**.  
  
4.  Na página **Organizar campos** , arraste o campo Product de **Campos disponíveis** até **Valores**.  
  
5.  Repita a etapa 3 para SalesDate, Quantity e Sales. Posicione SalesDate abaixo de Product, Quantity abaixo de SalesDate e Sales abaixo de SalesDate.  
  
6.  Clique em **Avançar**.  
  
7.  Na página **Escolha o layout** , exiba o layout da tabela.  
  
    A tabela é simples: cinco colunas sem nenhum grupo de linhas nem de colunas. Por não haver nenhum grupo, as opções de layout relacionadas aos grupos não estão disponíveis. Você atualizará manualmente a tabela para incluir um total no tutorial posteriormente.  
  
8.  Clique em **Avançar**.  
  
9. Clique em **Concluir**.  
  
11. Arraste a tabela para baixo da caixa de texto que você adicionou na lição 4.  
  
    > [!NOTE]  
    > Verifique se a tabela está dentro da caixa de listagem e dentro do retângulo cinza.  
  
12. Com a tabela selecionada, no painel **Grupo de Linhas** , clique com o botão direito do mouse em **Detalhes** > **Adicionar Total** > **Após**.  
  
    ![report-builder-free-form-table-totals](../reporting-services/media/report-builder-free-form-table-totals.png)
  
13. Selecione a célula na coluna Product e digite **Total**.

    ![report-builder-free-form-type-total](../reporting-services/media/report-builder-free-form-type-total.png)

12. Selecione o campo [SalesDate]. Na guia **Início** > **Número**, altere **Padrão** para **Data**.

13. Selecione os campos [Sum(Sales)]. Na guia **Início** > **Número**, altere **Padrão** para **Moeda**.

Clique em **Executar** para visualizar o relatório.  
  
O primeiro relatório exibe uma tabela com detalhes e totais de vendas.  
  
![report-builder-free-form-with-table](../reporting-services/media/report-builder-free-form-with-table.png)
   
## <a name="Save"></a>6. Salvar o relatório  
É possível salvar relatórios em um servidor de relatório, em uma biblioteca do SharePoint ou no computador.  
  
Neste tutorial, salve o relatório em um servidor de relatório. Se você não tiver acesso ao servidor de relatório, salve o relatório no computador.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
    A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por **SalesInformationByTerritory**.  
  
5.  Clique em **Salvar**.  
  
O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu Computador**e, em seguida, navegue até a pasta na qual você deseja salvar o relatório.  
  
3.  Em **Nome**, substitua o nome padrão por **SalesInformationByTerritory**.  
  
4.  Clique em **Salvar**.  
  
## <a name="Line"></a>7. (Opcional) Adicionar uma linha para separar áreas do relatório  
Adicione uma linha para separar as áreas editoriais e detalhadas do relatório.  
  
### <a name="to-add-a-line"></a>Para adicionar uma linha  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Na guia **Inserir** > **Itens de Relatório** > **Linha**.  
  
3.  Desenhe uma linha abaixo da caixa de texto adicionada na lição 4.  
  
4.  Clique na linha e, na guia **Início** > **Borda**, selecione:
     * **Largura** – selecione **3** pt.
     * **Cor** – selecione **Tomate**.  
  
## <a name="Visualization"></a>8. (Opcional) Adicionar visualizações de dados de resumo  
Os retângulos ajudam a controlar a renderização do relatório. Posicione um gráfico de pizza e de colunas dentro de um retângulo para garantir que o relatório seja renderizado da maneira desejada.  
  
### <a name="to-add-a-rectangle"></a>Para adicionar um retângulo  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Na guia **Inserir** > **Itens de Relatório** >  **Retângulo**. Arraste o retângulo para dentro da caixa de listagem à direita da tabela para criar um retângulo com cerca de 6 centímetros de largura e 20 centímetros de altura.  
  
3.  Com o novo retângulo selecionado, no painel Propriedades, crie **BorderColor LightGrey**, **BorderStyle Solid**e **BorderWidth 2 pt**. 

4. Alinhe as partes superiores do retângulo e da tabela.  
  
## <a name="to-add-a-pie-chart"></a>Para adicionar um gráfico de pizza  
  
1.  Na guia **Inserir** > **Visualizações de Dados** > **Gráfico** > **Assistente de Gráfico**.  
  
2.  Na página **Escolher um conjunto de dados** , clique em **ListDataset** > **Avançar**.  
  
3.  Clique em **Pizza** > **Avançar**.  
  
4.  Na página Organizar Campos de Gráfico, arraste Product até **Categorias**.  
  
5.  Arraste Quantity até **Valores**e clique em **Avançar**.  
  
6.  Clique em **Concluir**.  
  
8.  Redimensione o gráfico exibido no canto superior esquerdo do relatório para que ele tenha cerca de 4 centímetros de altura e 5 centímetros de largura.  
  
9. Arraste o gráfico para dentro do retângulo.  
   
10. Selecione o título do gráfico e digite: **Quantidades Vendidas do Produto**.  
  
12. Na guia **Início** > **Fonte**, crie o título:
    * **Fonte** **Interface do usuário do Sego Seminegrito**.
    * **Tamanho** **12 pt**.
    * **Cor** **Black**.  

13. Clique com o botão direito do mouse na legenda > **Propriedades da Legenda**.

14. Na guia **Geral** , em **Posição da legenda**, selecione o ponto central na parte inferior. 
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

16. Arraste para criar a região do gráfico com uma altura maior, se necessário.

     ![report-builder-free-form-pie](../reporting-services/media/report-builder-free-form-pie.png)
  
## <a name="to-add-a-column-chart"></a>Para adicionar um gráfico de colunas  
  
1.  Na guia **Inserir** > **Visualizações de Dados** > **Gráfico** > **Assistente de Gráfico**.  
  
2.  Na página **Escolher um conjunto de dados** , clique em **ListDataset**e em **Avançar**.  
  
3.  Clique em **Coluna**e em **Avançar**.  
  
4.  Na página **Organizar campos de gráfico** , arraste o campo Product até o painel **Categorias**.  
  
5.  Arraste Sales até **Valores** e clique em **Avançar**.  
  
    Os valores são exibidos no eixo vertical.  
  
6.  Clique em **Concluir**.  
  
    Um gráfico de colunas é adicionado ao canto superior esquerdo do relatório.  
  
8.  Redimensione o gráfico para que ele tenha cerca de 6 centímetros de largura e quase 10 centímetros de altura.  
  
9. Arraste o gráfico para dentro do retângulo, abaixo do gráfico de pizza.  
   
10. Selecione o título do gráfico e digite: **Vendas de Produtos**.  
  
12. Na guia **Início** > **Fonte**, crie o título:
    * **Fonte** **Interface do usuário do Sego Seminegrito**.
    * **Tamanho** **12 pt**.
    * **Cor** **Black**.  
  
15. Clique com o botão direito do mouse na legenda e, em seguida, clique em **Excluir Legenda**.  
  
    > [!NOTE]  
    > A remoção da legenda facilitará a leitura do gráfico quando ele for pequeno.  
  
    ![report-builder-free-form-column](../reporting-services/media/report-builder-free-form-column.png)

12. Selecione o eixo do gráfico e, na guia *Início** > **Número** > **Moeda**.

13. Selecione **Diminuir Decimal** duas vezes para que o número mostre apenas dólares, sem centavos.      
### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>Para verificar se os gráficos estão dentro do retângulo  

Você pode usar retângulos como contêineres para outros itens em uma página de relatório. Leia mais sobre [retângulos como contêineres](../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md).
  
1.  Selecione o retângulo criado e ao qual você adicionou os gráficos anteriormente nesta lição.  
  
    No painel Propriedades, a propriedade **Name** exibe o nome do retângulo.  
  
    ![report-builder-free-form-rectangle-name](../reporting-services/media/report-builder-free-form-rectangle-name.png) 
  
2.  Clique no gráfico de pizza.  
  
3.  No painel **Propriedades** , verifique se a propriedade **Parent** contém o nome do retângulo.  
  
     ![report-builder-free-form-pie-parent](../reporting-services/media/report-builder-free-form-pie-parent.png) 
  
4.  Clique no gráfico de colunas e repita a etapa 3.  
  
    > [!NOTE]  
    > Se os gráficos não estiverem dentro do retângulo, o relatório renderizado não exibirá os gráficos juntos.  
  
### <a name="to-make-the-charts-the-same-size"></a>Para deixar os gráficos com o mesmo tamanho  
  
1.  Selecione o gráfico de pizza, pressione a tecla Ctrl e selecione o gráfico de colunas.  
  
2.  Com ambos os gráficos selecionados, clique com o botão direito do mouse > **Layout** > **Ajustar para Mesma Largura**.  
  
    > [!NOTE]  
    > O item no qual você clica primeiro determina a largura de todos os itens selecionados.  
  
3.  Clique em **Executar** para visualizar o relatório.  
  
O relatório agora exibe dados de vendas resumidos em gráficos de pizza e de colunas.  
  

  
## <a name="next-steps"></a>Next Steps  
Isso conclui o tutorial sobre como criar um relatório de forma livre.  
  
Para obter mais informações sobre listas, consulte: 
* [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) 
* [Criar faturas e formulários com listas](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)
* [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
Para obter mais informações sobre designers de consultas, consulte [Designers de Consultas &#40;Construtor de Relatórios&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9) e [Interface do usuário do Designer de Consultas Baseadas em Texto &#40;Construtor de Relatórios&#41;](../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
## <a name="see-also"></a>Consulte Também  
[Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md) 
  

