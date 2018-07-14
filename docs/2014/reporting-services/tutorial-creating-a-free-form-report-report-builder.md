---
title: 'Tutorial: Criando um relatório de formato livre (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fe42fc3dd5e1398cc0e66ad2c37cd14a3fedd67a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202806"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>Tutorial: criando um relatório de formato livre (Construtor de Relatórios)
  Este tutorial ensina a criar um relatório de formulário livre do SSRS que se parece com uma carta de formulários. Você pode organizar itens de relatório para criar um formulário com caixas de texto, imagens e outras regiões de dados.  
  
 O relatório criado por você neste tutorial se baseia em dados de vendas de exemplo que estão incluídos no tutorial. O relatório agrupa informações por território e exibe o nome do gerente de vendas do território, bem como informações detalhadas e resumidas sobre as vendas. Você irá usar a região de dados da lista como a base do relatório de formato livre e, em seguida, adicionar um painel decorativo com uma imagem, um texto estático com dados inseridos, uma tabela para mostrar informações detalhadas e, opcionalmente, gráficos de pizza e de colunas para exibir informações resumidas.  
  
##  <a name="BackToTop"></a> O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
-   [Criar um relatório em branco, a fonte de dados e o conjunto de dados](#BlankReport)  
  
-   [Adicionar e configurar uma lista](#List)  
  
-   [Adicionar elementos gráficos](#Graphics)  
  
-   [Adicionar texto de formato livre](#Text)  
  
-   [Adicionar uma tabela para mostrar detalhes](#Table)  
  
-   [Formatar dados](#Format)  
  
-   [Salvar o relatório](#Save)  
  
### <a name="other-optional-steps"></a>Outras etapas opcionais  
  
-   [Adicione uma linha para separar áreas do relatório](#Line)  
  
-   [Adicionar visualização de dados de resumo](#Visualization)  
  
 Tempo estimado para concluir este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="BlankReport"></a> 1. Criar um relatório em branco, uma fonte de dados e um conjunto de dados  
  
> [!NOTE]  
>  Neste tutorial, como a consulta contém os valores de dados, o relatório não precisa de uma fonte de dados externa. O uso desse tipo de dados internos é ótimo para fins de aprendizado, mas a abordagem torna a consulta longa. para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
#### <a name="to-create-a-blank-report"></a>Para criar um relatório em branco  
  
1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.  
  
    > [!NOTE]  
    >  A caixa de diálogo **Guia de Introdução** deve ser exibida. Se ela não for exibida, usando o botão do Construtor de Relatórios, clique em **Novo**.  
  
2.  No painel esquerdo da caixa de diálogo **Guia de Introdução** , verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Relatório em Branco**.  
  
#### <a name="to-create-a-new-data-source"></a>Para criar uma nova fonte de dados  
  
1.  No painel de dados do relatório, clique em **Nova**e em **Fonte de Dados**.  
  
2.  No `Name` , digite: **ListDataSource**  
  
3.  Clique em **Usar uma conexão inserida no meu relatório**.  
  
4.  Verifique se o tipo de conexão é Microsoft SQL Server e, em seguida, na caixa **Cadeia de conexão**, digite: **Fonte de Dados = \<servername>**  
  
     \<ServerName >, por exemplo, Report001, especifica um computador no qual uma instância do mecanismo de banco de dados do SQL Server está instalada. Como os dados do relatório não são extraídos de um banco de dados do SQL Server, você não precisa incluir o nome de um banco de dados. O banco de dados padrão no servidor especificado é usado para analisar a consulta.  
  
5.  Clique em **Credenciais**e insira as credenciais necessárias para conexão à instância do Mecanismo de Banco de Dados do SQL Server.  
  
6.  Clique em **OK**.  
  
#### <a name="to-create-a-new-dataset"></a>Para criar um novo conjunto de dados  
  
1.  No painel de dados do relatório, clique em **Novo**e em **Conjunto de Dados**.  
  
2.  No `Name` , digite: **ListDataset.**  
  
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
  
7.  Clique no ícone Executar para executar a consulta.  
  
     Os resultados da consulta são os dados disponíveis a serem exibidos no relatório.  
  
     ![Designer de consulta](../../2014/tutorials/media/tutorial-querydesigner.png "Designer de consulta")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="List"></a> 2. Adicionar e configurar uma lista  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece três modelos de região de dados: tabela, matriz e lista. Esses modelos se baseiam na região de dados tablix.  
  
 Neste tutorial, você usará uma lista para exibir as informações sobre as vendas dos territórios de vendas em um relatório semelhante a um boletim informativo. As informações são agrupadas por território. Você irá adicionar um novo grupo de linhas que reúne dados por território e, em seguida, excluir o grupo de linhas interno Detalhes. O modelo de lista é ideal para criar relatórios de formulário livre. Para obter mais informações, consulte [lista &#40;construtor de relatórios e SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Esse relatório usa o tamanho de papel Carta (21,6 X 27,9) e margens de 2,54 centímetros. Uma página de relatório com mais de 22,86 centímetros de altura ou mais de 16,51 centímetros de largura pode gerar páginas em branco.  
  
#### <a name="to-add-a-list"></a>Para adicionar uma lista  
  
1.  Na guia **Inserir** da faixa de opções, na área **Regiões de Dados** , clique em **Lista** e, em seguida, arraste a lista para dentro do corpo do relatório. Crie a lista com cerca de 17,78 centímetros de altura e 15,87 centímetros de largura.  
  
2.  Clique dentro da lista, clique com o botão direito do mouse na parte superior da lista e clique em **Propriedades do Tablix**.  
  
     ![Lista de inclusão](../../2014/tutorials/media/tutorial-addinglistwithnumbers.png "adicionando lista")  
  
3.  Na lista suspensa **Nome do conjunto de dados** , selecione **ListDataset**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Clique com o botão direito do mouse na lista e clique em **Propriedades do Retângulo**.  
  
     ![Comando Propriedades do retângulo](../../2014/tutorials/media/tutorial-rectanglepropertiescommand.png "comando Propriedades do retângulo")  
  
6.  Na guia **Geral** , marque a caixa de seleção **Adicionar uma quebra de página após** .  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>Para adicionar um novo grupo de linhas e excluir o grupo Detalhes  
  
1.  No painel Grupos de Linhas, clique com o botão direito do mouse no grupo Detalhes, aponte para **Adicionar Grupo**e clique em **Grupo Pai**.  
  
     ![Comando grupo pai](../../2014/tutorials/media/tutorial-parentgroupcommand.png "comando grupo pai")  
  
2.  Na lista suspensa, selecione `[Territory].`  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Uma coluna é adicionada à lista. A coluna contém a célula `[Territory].`  
  
4.  Clique com o botão direito do mouse na coluna Territory da lista e clique em **Excluir Colunas**.  
  
     ![Excluir colunas](../../2014/tutorials/media/tutorial-deletecolumnscommand.png "excluir colunas")  
  
5.  Clique em **Excluir somente colunas**.  
  
     ![Excluir a caixa de diálogo colunas](../../2014/tutorials/media/tutorial-deletecolumnsdialog.png "caixa de diálogo Excluir colunas")  
  
6.  No painel Grupos de Linhas, clique com o botão direito do mouse no grupo **Detalhes** e, em seguida, clique em **Excluir Grupo**.  
  
     ![Excluir grupo de detalhes](../../2014/tutorials/media/tutorial-deletedetailsgroup.png "excluir detalhes do grupo")  
  
7.  Clique em **Excluir grupo apenas**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Graphics"></a> 3. Adicionar gráficos  
 Uma das vantagens de usar uma região de dados da lista é ser possível adicionar itens de relatório como retângulos e caixas de texto em qualquer lugar, em vez de haver limitação a um layout tabular. Você aprimorará a aparência do relatório, adicionando um gráfico (um retângulo preenchido com uma cor).  
  
#### <a name="to-add-graphic-elements-to-the-report"></a>Para adicionar elementos gráficos ao relatório  
  
1.  Sobre o **inserir** guia de faixa de opções, clique em **retângulo**e, em seguida, arraste um retângulo para o canto superior esquerdo da lista. Crie o retângulo com cerca de 17,78 centímetros de altura e 2,54 centímetros de largura.  
  
2.  Clique com o botão direito do mouse no retângulo e, em seguida, clique em **Propriedades do Retângulo**.  
  
3.  Clique na guia **Preenchimento** .  
  
4.  Na lista suspensa **Cor de preenchimento** , clique em **Mais Cores**e, em seguida, selecione a cor **Azul escuro** .  
  
     ![Selecione a cor de preenchimento](../../2014/tutorials/media/tutorial-selectfillcolorwithnumbers.png "cor de preenchimento de Select")  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Clique em **Executar** para visualizar o relatório.  
  
 O lado esquerdo do relatório agora tem um gráfico vertical que consiste em um retângulo cinza-escuro.  
  
##  <a name="Text"></a> 4. Adicionar texto de formato livre  
 Uma caixa de texto contém texto estático que é repetido em cada página de relatório, bem como campos de dados.  
  
#### <a name="to-add-text-to-the-report"></a>Para adicionar texto ao relatório  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Na guia **Inserir** da faixa de opções, clique em **Caixa de Texto**e, em seguida, arraste uma caixa de texto para o canto superior esquerdo da lista, mas dentro do retângulo adicionado por você anteriormente. Crie a caixa de texto com 7,62 centímetros de altura e 12,7 centímetros de largura.  
  
3.  Posicione o cursor na parte superior da caixa de texto e, em seguida, digite: **Boletim informativo para** .  
  
     ![Adicionar texto do cabeçalho do boletim informativo](../../2014/tutorials/media/tutorial-newsletterfor.png "Adicionar texto do cabeçalho do boletim informativo")  
  
    > [!NOTE]  
    >  Inclua o espaço extra após a palavra "para". O espaço separa o texto e o campo que você adicionará na próxima etapa.  
  
4.  Arraste o campo Territory para a caixa de texto e coloque-o depois do texto que você digitou na etapa 3.  
  
     ![Adicionar campo Territorial](../../2014/tutorials/media/tutorial-addterritorialfield.png "Territorial adicionar campo")  
  
5.  Selecione todo o texto, clique com o botão direito do mouse e, em seguida, clique em **Propriedades de Texto**.  
  
6.  Clique na guia **Fonte** .  
  
7.  Na lista **Fonte** , selecione **Times New Roman**. Em **Tamanho** , selecione **20 pt**, em **Cor** , selecione **Vermelho**.  
  
     ![Propriedades de texto](../../2014/tutorials/media/tutorial-textpropertieswithnumbers.png "propriedades de texto")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Posicione o cursor abaixo do texto que você digitou na etapa 3 e digite: **Olá** .  
  
    > [!NOTE]  
    >  Inclua o espaço extra após a palavra "Olá". O espaço separa o texto e o campo que você adicionará na próxima etapa.  
  
10. Arraste o campo NomeCompleto para a caixa de texto e coloque-o depois do texto que você digitou na etapa 9 e, em seguida, digite uma vírgula (,).  
  
     ![Adicionar campo de nome completo](../../2014/tutorials/media/tutorial-addfullnamefield.png "campo Adicionar nome completo")  
  
11. Selecione o texto que você adicionou nas etapas 9 e 10, clique com o botão direito do mouse e, em seguida, clique em **Propriedades de Texto**.  
  
12. Clique na guia **Fonte** .  
  
13. Na lista **Fonte** , selecione **Times New Roman**. Em **Tamanho** , selecione **16 pt**, em **Cor** , selecione **Preto** .  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. Posicione o cursor abaixo do texto que você adicionou nas etapas de 9 a 13 e, em seguida, copie e cole o seguinte texto "greeked":  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
    Nulla facilisi. Proin ligula enim, porta ut tincidunt id, adipiscing sit amet eros. Ut purus sem, bibendum et vulputate sit amet, facilisis eget magna. Sed aliquam erat non erat eleifend hendrerit. Ut a ligula est, sit amet eleifend enim. Ut et nisl enim, sit amet adipiscing augue. Vivamus eu arcu ac libero posuere elementum. Integer condimentum bibendum venenatis. Integer odio tellus, feugiat in pellentesque semper, interdum nec sem. Sed cursus euismod sem, ut elementum sapien placerat vel.   
    ```  
  
16. Selecione o texto que você adicionou na etapa 15, clique com o botão direito do mouse e, em seguida, clique em **Propriedades de Texto**.  
  
17. Clique na guia **Fonte** .  
  
18. Na lista **Fonte** , selecione **Arial**; em **Tamanho** , selecione **10 pt**, em **Cor** , selecione **Preto**.  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![Adicione o texto do boletim informativo](../../2014/tutorials/media/tutorial-newslettertext.png "adicionar texto do boletim informativo")  
  
20. Posicione o cursor abaixo do texto que você colou na etapa 15 e, em seguida, digite: **Parabéns pelo total de vendas de** .  
  
    > [!NOTE]  
    >  Inclua o espaço extra após a palavra "de". O espaço separa o texto e o campo que você adicionará na próxima etapa.  
  
21. Arraste o campo Sales para a caixa de texto, coloque-o depois do texto que você digitou na etapa 20 e, em seguida, digite um ponto de exclamação (!).  
  
22. Realce o campo vendas, o campo com o botão direito e, em seguida, clique em **expressão**.  
  
23. Na caixa de expressão, altere a expressão para incluir a função Soma da seguinte forma:  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![Adicionar uma expressão ao campo Vendas](../../2014/tutorials/media/tutorial-addexpressiontosalesfield.png "adicionar uma expressão ao campo vendas")  
  
25. Selecione o texto que você adicionou nas etapas de 20 a 23, clique com o botão direito do mouse e, em seguida, clique em **Propriedades de Texto**.  
  
26. Clique na guia **Fonte** .  
  
27. Na lista **Fonte** , selecione **Times New Roman**. Em **Tamanho** , selecione **16 pt**, em **Cor** , selecione **Vermelho**.  
  
28. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
29. Selecione `[Sum(Sales)]` e, na guia **Página Inicial** , no grupo **Número** , clique no botão **Moeda** .  
  
     ![Adicionar símbolo de moeda](../../2014/tutorials/media/tutorial-addcurrencysymbol.png "adicionar símbolo de moeda")  
  
30. Clique com o botão direito do mouse na caixa de texto com o texto “Clique para adicionar título” e clique em **Excluir**.  
  
31. Selecione a caixa de listagem e, usando as teclas de direção, mova-a para parte superior da página.  
  
32. Clique em **Executar** para visualizar o relatório.  
  
 O relatório exibe texto estático e cada página de relatório inclui dados pertencentes a um território. As vendas são formatadas como moeda.  
  
 ![Visualização do boletim informativo](../../2014/tutorials/media/tutorial-newsletters.png "visualização do boletim informativo")  
  
##  <a name="Table"></a> 5. Adicionar uma tabela para mostrar detalhes de vendas  
 Use o Assistente de Nova Tabela e Matriz para adicionar uma tabela ao relatório de formato livre. Depois de concluir o assistente, você adicionará manualmente uma linha para totais.  
  
#### <a name="to-add-a-table"></a>Para adicionar uma tabela  
  
1.  Na guia **Inserir** da faixa de opções, na área **Regiões de Dados** , clique em **Tabela**e em **Assistente de tabela**.  
  
2.  Na página Escolha um conjunto de dados, clique em **ListDataset**.  
  
3.  Clique em **Avançar**.  
  
4.  Na página **Organizar campos** , arraste o campo Product de **Campos disponíveis** até **Valores**.  
  
5.  Repita a etapa 4 para SalesDate, Quantity e Sales. Posicione SalesDate abaixo de Product, Quantity abaixo de SalesDate e Sales abaixo de SalesDate.  
  
6.  Clique em **Avançar**.  
  
7.  Na página **Escolha o layout** , exiba o layout da tabela.  
  
     A tabela é muito simples. Ela consiste em cinco colunas e não tem nenhum grupo de linhas ou de colunas. Por não haver nenhum grupo, as opções de layout relacionadas aos grupos não estão disponíveis. Você atualizará manualmente a tabela para incluir um total no tutorial posteriormente.  
  
8.  Clique em **Avançar**.  
  
9. Na página **Escolha um estilo** , no painel **Estilos** , selecione **Ardósia**.  
  
10. Clique em **Concluir**.  
  
11. Arraste a tabela para baixo da caixa de texto que você adicionou na lição 4.  
  
    > [!NOTE]  
    >  Verifique se a tabela está dentro da lista.  
  
12. Depois de confirmado que a tabela está selecionada, no painel Grupo de Linhas, clique com o botão direito do mouse em Detalhes, aponte para **Adicionar Total**e, em seguida, clique em **Depois**.  
  
     ![Adicionar relatório total](../../2014/tutorials/media/tutorial-addtotal.png "adicionar total do relatório")  
  
13. Clique em **Executar** para visualizar o relatório.  
  
 O primeiro relatório exibe uma tabela com detalhes e totais de vendas.  
  
 ![Totais de vendas no relatório](../../2014/tutorials/media/tutorial-reportsalestotals.png "totais de vendas no relatório")  
  
##  <a name="Format"></a> 6. Formatar dados  
 Formate dados numéricos como moeda e datas somente como dia e hora.  
  
#### <a name="to-format-fields-table"></a>Para formatar a tabela de campos  
  
1.  Clique em **Design** a fim de alternar para a exibição de design.  
  
2.  Clique nas células da tabela que contenham `[Sum(SalesSales)]` e, na guia **Página Inicial** , no grupo **Número** , clique no botão **Moeda** .  
  
     ![Adicionar o símbolo de moeda para somar vendas](../../2014/tutorials/media/tutorial-sumsales-currencysymbol.png "adicionar o símbolo de moeda para somar vendas")  
  
3.  Clique na célula que contenha `[SalesDate]` e, no grupo **Número** , na lista suspensa, selecione **Data**.  
  
4.  Clique em **Executar** para visualizar o relatório.  
  
 O relatório agora exibe dados formatados e é mais fácil de ler.  
  
 ![Formatar totais de vendas no relatório](../../2014/tutorials/media/tutorial-reportsalestotals-formatted.png "Formatar totais de vendas no relatório")  
  
##  <a name="Save"></a> 7. Salvar o relatório  
 É possível salvar relatórios em um servidor de relatório, em uma biblioteca do SharePoint ou no computador. Você também pode exportar o relatório para uma variedade de formatos, como Word e PDF, executando o relatório e selecionando o formato do menu **Exportar** .  
  
 Neste tutorial, salve o relatório em um servidor de relatório. Se você não tiver acesso ao servidor de relatório, salve o relatório no computador.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
     A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Na `Name`, substitua o nome padrão por **SalesInformationByTerritory**.  
  
5.  Clique em **Salvar**.  
  
 O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu Computador**e, em seguida, navegue até a pasta na qual você deseja salvar o relatório.  
  
3.  Na `Name`, substitua o nome padrão por **SalesInformationByTerritory**.  
  
4.  Clique em **Salvar**.  
  
##  <a name="Line"></a> 8. (Opcional) Adicionar uma linha para separar áreas do relatório  
 Adicione uma linha para separar as áreas editoriais e detalhadas do relatório.  
  
#### <a name="to-add-a-line"></a>Para adicionar uma linha  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Na guia **Inserir** da faixa de opções, na área **Itens do Relatório** , clique em **Linha**.  
  
3.  Desenhe uma linha abaixo da caixa de texto de formato livre que você adicionou na lição 4.  
  
4.  Clique na linha.  
  
5.  Clique na guia **Página Inicial** .  
  
6.  Na área **Borda** , para a largura, selecione **4 1/2** pt e, para a cor, selecione **Vermelho**.  
  
     ![Adicionar linha ao relatório](../../2014/tutorials/media/tutorial-reportwithline.png "Adicionar linha ao relatório")  
  
##  <a name="Visualization"></a> 9. (Opcional) Adicionar visualização de dados resumidos  
 Os retângulos ajudam a controlar a renderização do relatório. Posicione um gráfico de pizza e de colunas dentro de um retângulo para garantir que o relatório seja renderizado da maneira desejada.  
  
#### <a name="to-add-a-rectangle"></a>Para adicionar um retângulo  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Na guia **Inserir** da faixa de opções, na área **Itens do Relatório** , clique em **Retângulo**e, em seguida, arraste o retângulo para dentro da lista, à direita da tabela. Crie o retângulo com 6,45 centímetros de altura e 10,16 centímetros de largura.  
  
3.  Alinhe as partes superiores do retângulo e da tabela.  
  
#### <a name="to-add-a-pie-chart"></a>Para adicionar um gráfico de pizza  
  
1.  Na guia **Inserir** da faixa de opções, na área **Visualizações de Dados** , clique em **Gráfico** e em **Assistente de Gráfico**.  
  
2.  Na página Escolha um conjunto de dados, clique em **ListDataset**e em **Avançar**.  
  
3.  Clique em **Pizza**e em **Avançar**.  
  
4.  Na página Organizar Campos de Gráfico, arraste Product até **Categorias**.  
  
5.  Arraste Quantity até **valores**e, em seguida, clique em **próxima**.  
  
6.  Na página **Escolha um estilo** , no painel **Estilos** , selecione **Ardósia**.  
  
7.  Clique em **Concluir**.  
  
8.  Redimensione o gráfico exibido no canto superior esquerdo do relatório para que ele tenha 3,81 centímetros de altura e 5,08 centímetros de largura.  
  
9. Arraste o gráfico para dentro do retângulo.  
  
     ![Adicionar gráfico de pizza](../../2014/tutorials/media/tutorial-addpiechart.png "adicionar gráfico de pizza")  
  
10. Clique com o botão direito do mouse no título do gráfico e, em seguida, clique em **Propriedades do Título**.  
  
11. Na caixa de diálogo **Propriedades do Título do Gráfico** , em Texto do título, digite: **Quantidades Vendidas do Produto**.  
  
12. Clique na guia **Fonte** e, na lista **Tamanho** , em **10pt**.  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-column-chart"></a>Para adicionar um gráfico de colunas  
  
1.  Na guia **Inserir** da faixa de opções, na área **Visualizações de Dados** , clique em **Gráfico** e em **Assistente de Gráfico**.  
  
2.  Na página **Escolha um conjunto de dados** , clique em **ListDataset**e em **Avançar**.  
  
3.  Clique em **Coluna**e em **Avançar**.  
  
4.  Na página Organizar campos de gráfico, arraste o campo produto até **categorias**.  
  
5.  Arraste Sales até **Valores** e clique em **Avançar**.  
  
     Os valores são exibidos no eixo vertical.  
  
6.  Na página **Escolha um estilo** , no painel **Estilos** , selecione **Ardósia**.  
  
7.  Clique em **Concluir**.  
  
     Um gráfico de colunas é adicionado ao canto superior esquerdo do relatório.  
  
8.  Redimensione o gráfico para que ele tenha 5,08 centímetros de largura e 5,08 centímetros de altura.  
  
9. Arraste o gráfico para dentro do retângulo, abaixo do gráfico de pizza.  
  
     ![Adicionar gráfico de colunas](../../2014/tutorials/media/tutorial-addcolumnchart.png "adicionar gráfico de coluna")  
  
10. Clique com o botão direito do mouse no título do gráfico e, em seguida, clique em **Propriedades do Título**.  
  
11. Na caixa de diálogo **Propriedades do Título do Gráfico** , em Texto do título, digite: **Vendas do Produto**.  
  
12. Clique na guia **Fonte** e, na lista **Tamanho** , clique em **10pt**e, em seguida, clique em **OK**.  
  
13. No gráfico de colunas, clique com o botão direito do mouse no eixo vertical e, em seguida, desmarque **Mostrar Título do Eixo**.  
  
14. Repita a etapa 13 para o eixo horizontal.  
  
15. Clique com o botão direito do mouse na legenda e, em seguida, clique em **Excluir Legenda**.  
  
    > [!NOTE]  
    >  A remoção dos títulos dos eixos e da legenda deixará o gráfico mais legível quando ele for pequeno.  
  
 ![Alterar títulos de gráfico e remover o título do eixo](../../2014/tutorials/media/tutorial-columnchart-newtitle-noaxistitle.png "alterar títulos de gráfico e remover o título do eixo")  
  
#### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>Para verificar se os gráficos estão dentro do retângulo  
  
1.  Clique no retângulo que você adicionou anteriormente nesta lição.  
  
     No painel Propriedades, o `Name` propriedade exibe o nome do retângulo.  
  
     ![Nome do retângulo](../../2014/tutorials/media/tutorial-rectanglename.png "nome do retângulo")  
  
2.  Clique no gráfico de pizza.  
  
3.  No **propriedades** painel, verifique o `Parent` propriedade contém o nome do retângulo.  
  
     ![Pai da propriedade para o gráfico de pizza](../../2014/tutorials/media/tutorial-piechart-parentproperty.png "pai da propriedade para o gráfico de pizza")  
  
4.  Clique no gráfico de colunas e repita as etapas 2 e 3.  
  
    > [!NOTE]  
    >  Se os gráficos não estiverem dentro do retângulo, o relatório renderizado não exibirá os gráficos juntos.  
  
#### <a name="to-make-the-charts-the-same-size"></a>Para deixar os gráficos com o mesmo tamanho  
  
1.  Clique no gráfico de pizza, pressione a tecla Ctrl e, em seguida, clique no gráfico de colunas.  
  
2.  Com ambos os gráficos selecionados, clique com o botão direito do mouse, aponte para **Layout**e, em seguida, clique em **Mesma Largura**.  
  
     ![As larguras do gráfico de fazer a mesma](../../2014/tutorials/media/tutorial-makechartssamewidth.png "igualar as larguras do gráfico")  
  
    > [!NOTE]  
    >  O item no qual você clica primeiro determina a largura de todos os itens selecionados.  
  
3.  Clique em **Executar** para visualizar o relatório.  
  
 O relatório agora exibe dados de vendas resumidos em gráficos de pizza e de colunas.  
  
 ![Tutorial, relatório de forma livre do SSRS](../../2014/tutorials/media/tutorial-reportfinal.png "tutorial, relatório de forma livre do SSRS")  
  
## <a name="more-information"></a>Mais Informações  
 Para obter mais informações sobre listas, consulte [tabelas, matrizes e listas de &#40;construtor de relatórios e SSRS&#41;](report-design/tables-matrices-and-lists-report-builder-and-ssrs.md), [lista &#40;construtor de relatórios e SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md), [dados Tablix Áreas da região &#40;relatórios e SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md), e [células da região de dados Tablix, linhas e colunas &#40;construtor de relatórios&#41; e o SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Para obter mais informações sobre designers de consultas, consulte [Designers de Consultas &#40;Construtor de Relatórios&#41;](../../2014/reporting-services/query-designers-report-builder.md) e [Interface do usuário do Designer de Consultas Baseadas em Texto &#40;Construtor de Relatórios&#41;](report-data/text-based-query-designer-user-interface-report-builder.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
