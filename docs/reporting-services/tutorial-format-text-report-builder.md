---
title: "Tutorial: Formatar texto (Construtor de Relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
caps.latest.revision: "16"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4f040a1c915a03b95d57aa7f77b0d5cf611025ec
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="tutorial-format-text-report-builder"></a>Tutorial: Formatar texto (Construtor de Relatórios)

Neste tutorial, você treina como formatar texto de várias maneiras em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . É possível testar diferentes formatos. 

Depois de configurar o relatório em branco com a fonte de dados e o conjunto de dados, é possível escolher os formatos que você quer explorar. A ilustração a seguir mostra um relatório semelhante ao que você criará.  
  
![report-build-format-report](../reporting-services/media/report-build-format-report.png) 
  
Em uma etapa, você comete um erro de propósito, para poder ver o porquê do erro. Em seguida, você corrige o erro para obter o efeito desejado.  
    
Tempo estimado para concluir este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="CreateReport"></a>Criar um relatório em branco com uma fonte de dados e um conjunto de dados  
  
### <a name="to-create-a-blank-report"></a>Para criar um relatório em branco  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
 
2.  No painel esquerdo da caixa de diálogo **Guia de Introdução** , verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Relatório em Branco**.  
  
### <a name="to-create-a-data-source"></a>Para criar uma fonte de dados  
  
1.  No painel Dados do Relatório, clique em **Nova** > **Fonte de Dados**.  

    Se o painel **Dados do Relatório** não estiver visível, na guia **Exibir** , marque **Dados do Relatório**.
  
2.  Na caixa **Nome** , digite: **TextDataSource**  
  
3.  Clique em **Usar uma conexão inserida no meu relatório**.  
  
4.  Verifique se o tipo de conexão é Microsoft SQL Server e, na caixa **Cadeia de conexão** , digite: `Data Source = <servername>`  
  
    > [!NOTE]  
    > A expressão `<servername>`, por exemplo, Report001, especifica um computador no qual há uma instância do Mecanismo de Banco de Dados do SQL Server instalada. Este tutorial não precisa de dados específicos. Ele só precisa de uma conexão com um banco de dados do SQL Server. Se você já tiver uma conexão de fonte de dados listada em **Conexões de Fonte de Dados**, será possível selecioná-la e ir para o próximo procedimento, “Para criar uma fonte de dados”. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-dataset"></a>Para criar um conjunto de dados  
  
1.  No painel Dados do Relatório, clique em **Novo** > **Conjunto de Dados**.  
  
2.  Verifique se a fonte de dados é **TextDataSource**.  
  
3.  Na caixa **Nome** , digite: **TextDataset.**  
  
4.  Verifique se o tipo de consulta **Texto** está selecionado e, em seguida, clique em **Designer de Consulta**.  
  
5.  Clique em **Editar como Texto**.  
  
6.  Cole a seguinte consulta no painel de consulta:  

    > [!NOTE]  
    > Neste tutorial, como já contém os valores de dados, a consulta não precisa de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  Clique em Executar (**!**) para executar a consulta.  
  
    Os resultados da consulta são os dados disponíveis a serem exibidos no relatório.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

9.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="AddField"></a>Adicionar um campo à superfície de design do relatório  
Se você quiser que um campo do conjunto de dados seja exibido em um relatório, seu primeiro impulso poderá ser de arrastá-lo diretamente para a superfície de design. Este exercício aponta por que isso não funciona e o que fazer em vez disso.  
  
### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>Para adicionar um campo ao relatório (e obter o resultado errado)  
  
1.  Arraste o campo **FullName** do painel Dados do Relatório até a superfície de design.  
  
    O Construtor de Relatórios cria uma caixa de texto com uma expressão, representada como `<Expr>`.  
  
2.  Clique em **Executar**.  
  
    Apenas um registro, **Fernando Ross**, está visível, o primeiro registro na consulta em ordem alfabética. O campo não se repete para mostrar os outros registros nesse campo.  
  
3.  Clique em **Design** para retornar à exibição de design.  
  
4.  Selecione a expressão `<Expr>` na caixa de texto.  
  
5.  No painel Propriedades, na propriedade **Valor** , você vê o seguinte (se o painel Propriedades não estiver visível, na guia **Exibir** , marque **Propriedades**):  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
    A função `First` foi projetada para recuperar apenas o primeiro valor em um campo, e foi isso o que ela fez.  
  
    Arrastar o campo diretamente para a superfície de design criou uma caixa de texto. Por si, as caixas de texto não são regiões de dados, logo, elas não exibem dados de um conjunto de dados do relatório. As caixas de texto em regiões de dados, como tabelas, matrizes e listas, exibem dados.  
  
6.  Selecione a caixa de texto (se a expressão estiver selecionada, pressione ESC para marcar a caixa de texto) e pressione a tecla DEL.  
  
### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>Para adicionar um campo ao relatório (e obter o resultado certo)  
  
1.  Na guia **Inserir** da faixa de opções, na área **Regiões de Dados** , clique em **Lista**. Clique na superfície de design e, em seguida, arraste-a para criar uma caixa com aproximadamente 5,08 centímetros de largura e 2,54 centímetros de altura.  
  
2.  Arraste o campo **FullName** do painel Dados do Relatório até a caixa de listagem.  
  
    Desta vez, o Construtor de Relatórios cria uma caixa de texto com a expressão `[FullName]` .  
  
3.  Clique em **Executar**.  
  
    Observe que, desta vez, a caixa se repete para mostrar todos os registros na consulta.  
  
4.  Clique em **Design** para retornar à exibição de design.  
  
5.  Selecione a expressão na caixa de texto.  
  
6.  No painel Propriedades, na propriedade **Valor** , o seguinte é exibido:  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
    Arrastando a caixa de texto até a região de dados da lista, você exibe os dados presentes no campo do conjunto de dados.  
  
7.  Selecione a caixa de listagem e pressione a tecla DEL.  
  
## <a name="AddTable"></a>Adicionar uma tabela à superfície de design do relatório  
Crie essa tabela para que você tenha um local para colocar os hiperlinks e o texto girado.   
  
1.  Na guia **Inserir** > **Tabela** > **Assistente de Tabela**.  
  
2.  Na página **Escolher um conjunto de dados** do Assistente de Nova Tabela ou Matriz, clique em **Escolher um conjunto de dados existente neste relatório ou em um conjunto de dados compartilhado** > **TextDataset (neste Relatório)** > **Avançar**.  
  
3.  Na página **Organizar campos** , arraste os campos **Territory**, **LinkText**e **Product** até **Grupos de Linhas**, arraste o campo **Sales** até **Valores**e clique em **Avançar**.  

    ![report-builder-text-arrange-fields](../reporting-services/media/report-builder-text-arrange-fields.png)
  
4.  Na página **Escolher o layout** , desmarque a caixa de seleção **Expandir/recolher grupos** para que seja possível ver toda a tabela e clique em **Avançar**. 
  
5.  Clique em **Concluir**.  
  
6.  Clique em **Executar**.  
  
    A tabela parece correta, mas tem duas linhas totais. A coluna **LinkText** não precisa de uma linha Total.  
    
    ![report-builder-format-2-totals](../reporting-services/media/report-builder-format-2-totals.png)
  
8.  Clique em **Design** para retornar à exibição de design.  
  
9. Selecione a célula **Total** na coluna **LinkText** e mantenha a tecla SHIFT pressionada e selecione as duas células à direita: a célula vazia na coluna **Product** e a célula `[Sum(Sales)]` da coluna **Sales** .  
  
11. Com essas três células selecionadas, clique com o botão direito do mouse em uma delas e clique em **Excluir Linhas**.  

    ![report-builder-format-delete-rows](../reporting-services/media/report-builder-format-delete-rows.png)
  
12. Clique em **Executar**.  

    Agora ele tem somente uma linha Total.
    
    ![report-builder-format-one-total](../reporting-services/media/report-builder-format-one-total.png)
  
## <a name="AddHyperlink"></a>Adicionar um hiperlink ao relatório  
Nesta seção, você adiciona um hiperlink ao texto na tabela da seção anterior.  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique com o botão direito do mouse na célula que contém `[LinkText]`e clique em **Propriedades da Caixa de Texto**.  
  
3.  Na guia **Ação** , clique em **Ir para URL**.  
  
5.  Na caixa **Selecionar URL** , clique em **[URL]**e em **OK**.  
  
6.  Observe que o texto não parece diferente. Você precisa fazê-lo parecer um texto de link.  
  
7.  Selecione `[LinkText]`.  
  
8.  Na guia **Início** > **Fonte**, selecione **Sublinhado** e altere **Cor** para **Azul**.  
  
9. Clique em **Executar**.  
  
    O texto agora se parece com um link.  
    
    ![report-builder-format-hyperlink](../reporting-services/media/report-builder-format-hyperlink.png)
  
10. Clique em um link. Se o computador estiver conectado à Internet, um navegador abrirá um tópico da Ajuda do Construtor de Relatórios.  
  
## <a name="RotateText"></a>Girar texto no relatório  
Nesta seção, você gira um texto na tabela das seções anteriores.  
 
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na célula que contém `[Territory].`  
  
3.  Na guia **Início** , na seção **Fonte** , clique no botão **Negrito** .  
  
4.  Se o painel Propriedades não estiver aberto, na guia **Exibir** , marque a caixa de seleção **Propriedades** .  
  
5.  Localize a propriedade WritingMode no painel Propriedades e altere-a de **Padrão** para **Rotate270**.  
 
    > [!NOTE]  
    > Quando as propriedades no painel Propriedades estiverem organizadas em categorias, WritingMode estará na categoria **Localização** . Verifique se você selecionou a célula, e não o texto WritingMode é uma propriedade da caixa de texto, não do texto.  

    ![report-builder-select-territory-cell](../reporting-services/media/report-builder-select-territory-cell.png)
   
6.  Na guia **Início** > seção **Parágrafo**, selecione **Meio** e **Centro** para localizar o texto no centro da célula vertical e horizontalmente.  
  
8.  Clique em Executar (**!**).  
  
Agora o texto na célula `[Territory]` é executado verticalmente da parte inferior para a parte superior das células.  

![report-builder-format-rotate-270](../reporting-services/media/report-builder-format-rotate-270.png)

## <a name="FormatCurrency"></a>Formatar moeda  
  
1.  Clique em **Design** a fim de alternar para a exibição de design.  
  
2.  Clique na célula da tabela superior que contenha `[Sum(Sales)]`, mantenha a tecla SHIFT pressionada e clique na célula da tabela inferior que contenha `[Sum(Sales)]`.  
  
3.  Na guia **Início** > grupo **Número** > botão **Moeda**.  
  
4.  (Opcional) Se a configuração regional for Inglês (Estados Unidos), o texto de exemplo padrão será [**US$ 12.345,00**]. Se um valor de moeda de exemplo não estiver visível, no grupo **Números** , clique em **Estilos de Espaço Reservado** > **Valores de Exemplo**.  

    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)
  
5.  (Opcional) Na guia **Início** , no grupo **Número** , clique no botão **Diminuir Decimais** duas vezes para exibir valores em dólares sem centavos.  
  
6.  Clique em Executar (**!**) para visualizar o relatório.  
  
O relatório agora exibe dados formatados e é mais fácil de ler.  

![report-build-format-report](../reporting-services/media/report-build-format-report.png)
    
## <a name="FormatHTML"></a>Exibindo texto com formatação HTML  
  
1.  Clique em **Design** a fim de alternar para a exibição de design.  
  
2.  Na guia **Inserir** , clique em **Caixa de Texto**e, na superfície de design, clique e arraste para criar uma caixa de texto abaixo da tabela, com cerca de 10 centímetros de largura e 8 centímetros de altura.  
  
3.  Copiar esse texto e cole-o na caixa de texto:  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  Arraste a borda inferior da caixa de texto para que todo o texto caiba. Observe que a superfície de design fica maior à medida que você arrasta.

5. Selecione todo o texto na caixa de texto.  
  
5.  Clique com o botão direito do mouse em todo o texto selecionado e clique em **Propriedades do Texto**.  
  
    Essa é uma propriedade do texto, não da caixa de texto, portanto, em uma caixa de texto você pode ter uma mistura de texto sem formatação e texto que usa marcas HTML como estilos.  
  
6.  Na página **Geral** , em **Tipo de marcação**, clique em **HTML – Interpretar marcas HTML como estilos**.  
  
7.  Clique em **OK**.  
  
8.  Clique em Executar (**!**) para visualizar o relatório.  
  
O texto na caixa de texto é exibido como um título, um parágrafo e uma lista com marcadores.  
  
![report-builder-format-html](../reporting-services/media/report-builder-format-html.png)

## <a name="Save"></a>Salvar o relatório  
É possível salvar relatórios em um servidor de relatório, em uma biblioteca do SharePoint ou no computador.  
  
Neste tutorial, salve o relatório em um servidor de relatório. Se você não tiver acesso ao servidor de relatório, salve o relatório no computador.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
    A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por um nome de sua escolha.

5.  Clique em **Salvar**.  
  
O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu Computador**e, em seguida, navegue até a pasta na qual você deseja salvar o relatório.  
  
3.  Em **Nome**, substitua o nome padrão por um nome de sua escolha. 
  
4.  Clique em **Salvar**.  

## <a name="next-steps"></a>Próximas etapas

Há várias maneiras de formatar um texto no Construtor de Relatórios. O [Tutorial: Criação de um relatório de forma livre](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md) contém mais exemplos.  

[Tutoriais do Construtor de Relatórios ](../reporting-services/report-builder-tutorials.md) 
[Formatação de Itens de Relatório](../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)  
[Construtor de Relatórios no SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
