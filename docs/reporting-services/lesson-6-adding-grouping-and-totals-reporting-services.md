---
title: "Lição 6: Adicionando agrupamentos e totais (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
caps.latest.revision: 56
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e20b99d995151c14e6c334a647da14d3ff8f365
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lesson 6: Adding Grouping and Totals (Reporting Services)
Nesta lição do tutorial, você adicionará agrupamentos e totais ao relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para organizar e resumir os dados.  
  
  
## <a name="bkmk_groupdata"></a>Para agrupar dados em um relatório  
  
1.  Clique na guia **Design** .  
  
2.  Se o painel **Grupos de linhas** não estiver visível, clique com o botão direito do mouse na superfície de design, em seguida, clique em **Exibir** e em **Agrupamento**.  
  
3.  No painel **Dados do Relatório** , arraste o campo **Date** para o painel **Grupos de Linhas** . Coloque-o acima da linha chamada **(Detalhes)**.
  
    Observe que a alça de linha agora exibe um colchete para mostrar um grupo. A tabela também tem duas colunas Data – uma em cada lado de uma linha pontilhada vertical.  
  
    ![Data de grupo adicionada](../reporting-services/media/rs-basictablegroups1design.png "data grupo adicionado")  
  
4.  No painel **Dados do Relatório** , arraste o campo **Order** para o painel **Grupos de Linhas** . Coloque-o abaixo de Data e acima de **(Detalhes)**.

![ssrs_ssdt_addorderfield](../reporting-services/media/ssrs-ssdt-addorderfield.png)   
  
    Note that the row handle now has two brackets in it ![ssrs_ssdt_rowgroupdoublehandles](../reporting-services/media/ssrs-ssdt-rowgroupdoublehandles.png), to show two groups. The table now has two **Order** columns, too.  
  
5.  Exclua as colunas **Data** e **Pedido** originais à **direita** da linha dupla. Isso removerá os valores do registro individual para que apenas o valor do grupo seja exibido. Selecione as alças de coluna das duas colunas, clique com o botão direito do mouse e clique em **Excluir Colunas**.  
  
    ![Selecione as colunas para excluir](../reporting-services/media/rs-basictablegroupsdeletecols.gif "selecionar colunas para exclusão")  
  
6.  Para formatar a nova coluna de data, clique com o botão direito do mouse na célula com a expressão de campo `[Date]` e clique em **Propriedades da Caixa de Texto**.  
  
7.  Clique em **Número**e, no campo **Categoria** , clique em **Data**.  
  
8.  Na caixa **Tipo** , selecione **31 de janeiro de 2000**.  
  
9.  [!INCLUDE[clickOK](../includes/clickok-md.md)].  
  
10.  Alterne para a guia **Visualizar** para visualizar o relatório. Sua aparência deve ser similar a esta ilustração:  
    ![rs_BasicTableGroupsPreview](../reporting-services/media/rs-basictablegroupspreview.png) 
  
## <a name="bkmk_addtotals"></a>Para adicionar totais a um relatório  
  
1.  Alterne para o modo Design.  
  
2.  Clique com o botão direito do mouse na célula da região de dados que contém o campo `[LineTotal]`e clique em **Adicionar Total**.  
  
    Isso adicionará uma linha com uma soma do valor monetário de cada pedido.  
  
3.  Clique com o botão direito do mouse na célula que contém o campo `[Qty]`e clique em **Adicionar Total**.  
  
    Isso adicionará uma soma da quantidade de cada pedido à linha de total.  
  
4.  Na célula vazia à esquerda de `Sum[Qty]`, digite o rótulo "**Total de Pedidos"**.  
  
5.  Você pode adicionar uma cor do plano de fundo à linha de total. Selecione as duas células de soma e a célula de rótulo.  
  
6.  No menu **Formatar** , clique em **Cor do Plano de Fundo**, clique em **Cinza Claro**e clique em **OK**.  
  
    ![Exibição de design: tabela básica com total do pedido](../reporting-services/media/rs-basictablesumlinetotaldesign.gif "exibição de Design: tabela básica com total do pedido")  
  
## <a name="bkmk_adddailytotal"></a>Para adicionar um total diário a um relatório  
  
1.  Clique com o botão direito do mouse na célula **Pedido** , aponte para **Adicionar Total**e clique em **Após**.  
  
    Isso adicione uma nova linha contendo as somas de quantidade e valor em dólar de cada dia e o rótulo “**Total**” na parte inferior da coluna Pedido.  
  
2.  Digite o palavra **Diário** depois da palavra **Total** na mesma célula para que apareça **Total Diário**.  
  
3.  Selecione a célula **Total Diário** , as duas células **Soma** e a célula vazia entre eles.  
  
4.  No menu **Formatar** , clique em **Cor do Plano de Fundo**, clique em **Laranja**e clique em **OK**.  
  
    ![](../reporting-services/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
## <a name="bkmk_addgrandtotal"></a>Para adicionar um total geral a um relatório  
  
1.  Clique com o botão direito do mouse na célula Data, aponte para **Adicionar Total**e clique em **Após**.  
  
    Isso adicionará uma nova linha contendo as somas de quantidade e valor monetário de todo o relatório e o rótulo **Total** na coluna **Data** .  
  
2.  Digite a palavra **Geral** depois da palavra **Total** na mesma célula para que apareça **Total Geral**.  
  
3.  Selecione a célula **Total Geral** , as duas células **Soma** e as células vazias entre eles.  
  
4.  No menu **Formatar** , clique em **Cor do Plano de Fundo**, clique em **Azul Claro**e clique em **OK**.  
  
    ![Exibição de design: total geral em tabela básica](../reporting-services/media/rs-basictablesumgrandtotaldesign.gif "exibição de Design: total geral em tabela básica")  
  
5.  Clique em **Visualizar**.  
  
    A última página deve ser semelhante à imagem a seguir. Na barra de ferramentas, clique em Última Página ![ssrs_ssdt_viewertoolbar_lastpage](../reporting-services/media/ssrs-ssdt-viewertoolbar-lastpage.png).   
  
    ![Visualização: Tabela básica com total geral](../reporting-services/media/rs-basictablesumgrandtotalpreview.gif "visualização: tabela básica com total geral")  
  
## <a name="bkmk_publishreport"></a>Para publicar o relatório no Servidor de Relatório (opcional)  
  
1.  Uma etapa opcional é publicar o relatório concluído no servidor de relatório de modo nativo para que você possa exibir o relatório no Gerenciador de Relatórios.  
  
2.  Clique no menu **Projeto** e em **Propriedades do tutorial...**  
  
3.  Em **TargetServerURL** , digite o nome do servidor de relatório, por exemplo   
- `http:/<servername>/reportserver`  
   
- `http://localhost/reportserver` funcionará se você estiver criando o relatório no servidor de relatório.  
  
  
4. Observe que TargetReportFolder é o tutorial, o nome do projeto.  Esse é o nome da pasta na qual o relatório será implantado nas próximas etapas.  
5. Clique em **OK**.  
  
6.  Clique no menu **Criar** e em **Implantar tutorial**.  
  
    Se você vir uma mensagem semelhante à seguinte na janela de saída, ela indicará uma implantação com êxito.  
  
    > ------ Compilação iniciada: Projeto: tutorial, Configuração: Debug ------  
    > Ignorando 'Sales Orders.rdl'. O item está atualizado.  
    > Compilação concluída – 0 erros, 0 avisos  
    > ------ Implantação iniciada: Projeto: tutorial, Configuração: Debug ------  
    > Implantando em http://[nome do servidor]/reportserver  
    > Implantando relatório '/tutorial/Sales Orders'.  
    > Implantação concluída -- 0 erros, 0 avisos  
    > ========== Compilação: 1 com êxito ou atualizados, 0 com falha, 0 ignorados ==========  
    > ========== Implantação: 1 com êxito, 0 com falha, 0 ignorados ==========  
  
    Se você vir uma mensagem de erro semelhante à seguinte, verifique se você tem permissões no servidor de relatório e se iniciou o [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] com privilégios de administrador.  
  
    > "As permissões concedidas ao usuário 'XXXXXXXX\\[seu nome de usuário]' não são suficientes para a execução desta operação."  
  
7.  Vá para o portal da Web com privilégios de administrador, por exemplo, clique com o botão direito do mouse no ícone do Internet Explorer e clique em **Executar como administrador**.  
  
    Navegue até a URL do portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .   
    **Observação:** a URL do *portal* é "Reports", não a URL do *Servidor* de Relatório "Reportserver".  Por exemplo:   
    - `http://<server name>/reports`.  
     - `http://localhost/reports` funcionará se você estiver criando o relatório no servidor de relatório.  
  
8.  Procure a pasta que contém o relatório. O nome padrão é *tutorial*, o nome do projeto ou o nome digitado no campo TargetReportFolder nas propriedades do projeto.   
Clique no nome do relatório **Pedidos de Venda** para exibir o relatório renderizado no navegador.  
  
    ![ssrs_tutorial_tutorialfolder](../reporting-services/media/ssrs-tutorial-tutorialfolder.png)  
 
* * Você concluiu com êxito o criando um relatório de tabela básico tutorial.* *  
  
## <a name="see-also"></a>Consulte também  
[Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
  


