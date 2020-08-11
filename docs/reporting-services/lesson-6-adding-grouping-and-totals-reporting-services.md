---
title: 'Lição 6: Adicionar agrupamentos e totais (Reporting Services) | Microsoft Docs'
description: Saiba como adicionar agrupamentos e totais ao relatório do Reporting Services para organizar e resumir seus dados.
ms.date: 04/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5d149bb85834ae9c775e414e405889631a81f288
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243258"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lição 6: Adicionar agrupamentos e totais (Reporting Services)

Nesta lição final do tutorial, você adicionará agrupamentos e totais ao relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para organizar e resumir os dados.  

## <a name="to-group-data-in-a-report"></a>Para agrupar dados em um relatório

1. Selecione a guia **Design**.
2. Se o painel **Grupos de Linhas** não estiver visível, clique com o botão direito do mouse na superfície de design e selecione **Exibir** >**Agrupamento**.
3. No painel **Dados do Relatório**, arraste o campo `[Date]` para o painel **Grupos de Linhas**. Coloque-o acima da linha exibida como **= (Detalhes)** .

    > [!NOTE]
    > Observe que agora a alça de linha exibe um colchete para indicar um grupo. Agora a tabela também tem duas colunas de expressão `[Date]`, uma em cada lado de uma linha pontilhada vertical.
    >
    >![grupo de datas adicionado](media/rs-basictablegroups1design.png "grupo de datas adicionado")
4. No painel **Dados do Relatório**, arraste o campo `[Order]` para o painel **Grupos de Linhas**. Coloque-o abaixo de **Data** e acima de **= (Detalhes)** .

    ![ssrs_ssdt_addorderfield](media/ssrs-ssdt-addorderfield.png)

    > [!NOTE]
    > Observe que agora o identificador de linha exibe dois colchetes, ![ssrs_ssdt_rowgroupdoublehandles](media/ssrs-ssdt-rowgroupdoublehandles.png), para indicar dois grupos. Agora a tabela também tem duas colunas de expressão `[Order]`.

5. Exclua as colunas originais da expressão `[Date]` e `[Order]` à direita da linha dupla. Selecione as alças de coluna das duas colunas, clique com o botão direito do mouse e selecione **Excluir Colunas**. O Designer de Relatórios remove as expressões de linhas individuais, assim somente as expressões de grupos são exibidas.

    ![Selecionar colunas para exclusão](media/rs-basictablegroupsdeletecols.gif "Selecionar colunas para exclusão")

6. Para formatar a nova coluna `[Date]`, clique com botão direito do mouse na célula da região de dados que contém a expressão `[Date]` e selecione **Propriedades da Caixa de Texto**.
7. Selecione **Número**, na caixa de listagem de coluna à extrema esquerda, e **Data** na caixa de listagem **Categoria**.
8. Na caixa de listagem **Tipo**, selecione **31 de janeiro de 2000**.
9. Selecione **OK** para aplicar o formato.
10. Visualize novamente o relatório. Ele deve estar como mostrado abaixo:

    ![rs_BasicTableGroupsPreview](media/rs-basictablegroupspreview.png)

## <a name="adding-totals-to-a-report"></a>Adicionar totais a um relatório

1. Alterne para o modo **Design**.
2. Clique com o botão direito do mouse na célula da região de dados que contém a expressão `[LineTotal]` e selecione **Adicionar Total**. O Designer de Relatórios adiciona uma linha com uma soma do valor monetário de cada pedido.
3. Clique com o botão direito do mouse na célula que contém o campo `[Qty]` e clique em **Adicionar Total**. O Designer de Relatórios adiciona uma soma da quantidade de cada pedido à linha de totais.
4. Na célula vazia à esquerda da célula `Sum[Qty]`, digite a cadeia de caracteres "Total de Pedidos".
5. Você pode adicionar uma cor do plano de fundo à linha de total. Selecione as duas células de soma e a célula de rótulo.  
6. No menu **Formato**, selecione o quadrado **Cor da Tela de Fundo** > **Cinza Claro**.
7. Selecione **OK** para aplicar o formato.

   ![Modo de exibição de Design: Tabela básica com total do pedido](media/rs-basictablesumlinetotaldesign.gif "Modo de exibição de Design: tabela básica com o total do pedido")

## <a name="add-the-daily-total-to-the-report"></a>Adicionar o total diário ao relatório

1. Clique com botão direito do mouse na célula de expressão `[Order]` e selecione **Adicionar Total** > **Após**. O Designer de Relatórios adiciona uma nova linha contendo as somas dos valores `[Qty]` e `[Linetotal]` para cada dia e a cadeia de caracteres "Total" na parte inferior da coluna de expressão `[Order]`.
2. Digite a palavra "Diário" depois da palavra "Total" na mesma célula para que apareça "Total Diário".
3. Selecione essa célula, as duas células adjacentes de total à direita e a célula vazia entre eles.
4. No menu **Formato**, selecione o quadrado **Cor da Tela de Fundo** > **Laranja**.
5. Selecione **OK** para aplicar o formato.

   ![Definir cor da tela de fundo como laranja](media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")

## <a name="add-the-grand-total-to-the-report"></a>Adicionar o total geral ao relatório

1. Clique com botão direito do mouse na célula de expressão `[Date]` e selecione **Adicionar Total** > **Após**. O Designer de Relatórios adiciona uma nova linha contendo as somas dos valores `[Qty]` e `[LineTotal]` do relatório inteiro e a cadeia de caracteres "Total" na parte inferior da coluna de expressão `[Date]`.
2. Digite a palavra "Geral" depois da palavra "Total" na mesma célula para que apareça "Total Geral".
3. Selecione a célula "Total Geral", as duas células `Sum()` e as células vazias entre elas.
4. No menu **Formato**, selecione o quadrado **Cor da Tela de Fundo** > **Azul Claro**.
5. Selecione **OK** para aplicar o formato.

    ![Modo de exibição de Design: Total geral em tabela básica](media/rs-basictablesumgrandtotaldesign.gif "Modo de exibição de Design: Total geral em tabela básica")

## <a name="preview-the-report"></a>Visualizar o relatório

Para visualizar as alterações de formato, selecione a guia **Visualização**. Na barra de ferramentas **Visualização**, selecione o botão **Última Página**, que se parece com ![ssrs_ssdt_viewertoolbar_lastpage](media/ssrs-ssdt-viewertoolbar-lastpage.png). Os resultados devem ser exibidos como mostrado a seguir:

   ![Visualização: Tabela básica com total geral](media/rs-basictablesumgrandtotalpreview.gif "Visualização: tabela básica com total geral")

## <a name="publishing-the-report-to-the-report-server-optional"></a>Publicar o relatório no *Servidor de Relatório* (opcional)

Uma etapa opcional é publicar o relatório concluído no Servidor de Relatório para poder exibi-lo no portal da Web.

1. Selecione o menu **Projeto** > **Propriedades do Tutorial...**
2. Em **TargetServerURL**, digite o nome do servidor de relatório, por exemplo:
    - `http:/<servername>/reportserver` ou
    - `https://localhost/reportserver` funcionará se você estiver criando o relatório no servidor de relatório.

3. **TargetReportFolder** é denominado Tutorial devido ao nome do projeto. O Designer de Relatórios implanta o relatório nesta pasta.
4. Selecione **OK**.
5. Selecione o menu **Compilar** > **Implantar Tutorial**.

    Ver uma mensagem semelhante à seguinte na janela **Saída** indica uma implantação com êxito.

    > ------ Build iniciado: Projeto: tutorial, Configuração: Depuração ------  
    > Ignorando 'Sales Orders.rdl'. O item está atualizado.  
    > Compilação concluída – 0 erros, 0 avisos  
    > ------ Implantação iniciada: Projeto: tutorial, Configuração: Depuração ------  
    > Implantando em `https://[server name]/reportserver`  
    > Implantando relatório '/tutorial/Sales Orders'.  
    > Implantação concluída -- 0 erros, 0 avisos  
    > ========== Compilação: 1 com êxito ou atualizados, 0 com falha, 0 ignorados ==========  
    > ========== Implantação: 1 bem-sucedida, 0 com falha, 0 ignoradas ==========  

    Se você vir uma mensagem de erro semelhante à seguinte, verifique se você tem permissões no servidor de relatório e se iniciou o [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] com privilégios de administrador.
    >
    > "As permissões concedidas ao usuário 'XXXXXXXX\\[seu nome de usuário]' não são suficientes para a execução desta operação."

6. Abra um navegador com privilégios de administrador. Por exemplo, clique com botão direito do mouse no ícone do Internet Explorer e selecione **Executar como administrador**.
7. Navegue até a URL do portal da Web.
   - `https://<server name>/reports`.
   - `https://localhost/reports` funcionará se você estiver criando o relatório no servidor de relatório.

8. Selecione a pasta Tutorial e o relatório de "Pedidos de Vendas" para exibi-lo.

    ![ssrs_tutorial_tutorialfolder](media/ssrs-tutorial-tutorialfolder.png)  

Você concluiu com êxito o tutorial **Criando um relatório de tabela básico**.

## <a name="see-also"></a>Confira também

[Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)
