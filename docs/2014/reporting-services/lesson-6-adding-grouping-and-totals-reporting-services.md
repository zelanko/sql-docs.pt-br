---
title: 'Lição 6: Adicionando agrupamentos e totais (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5a372f230cfc2fc63e59787b8f9b674928f72368
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095287"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lesson 6: Adding Grouping and Totals (Reporting Services)
  Adicione agrupamento e totais ao relatório para organizar e resumir os dados.  
  
 Para obter informações sobre como adicionar totais em execução aos relatórios, consulte este artigo do curah.microsoft.com: [adicionar totais aos relatórios do Reporting Services (SSRS)](http://go.microsoft.com/fwlink/p/?LinkId=403698).  
  
 **Neste tópico:**  
  
-   [Para agrupar dados em um relatório](#bkmk_groupdata)  
  
-   [Para adicionar totais a um relatório](#bkmk_addtotals)  
  
-   [Para adicionar um total diário a um relatório](#bkmk_adddailytotal)  
  
-   [Para adicionar um total geral a um relatório](#bkmk_addgrandtotal)  
  
-   [Para publicar o relatório ao servidor de relatório (opcional)](#bkmk_publishreport)  
  
##  <a name="bkmk_groupdata"></a> Para agrupar dados em um relatório  
  
1.  Clique na guia **Design** .  
  
2.  Se você não vir as **grupos de linhas** painel, clique com botão direito na superfície de design e clique em **exibição** e, em seguida, clique em **agrupamento**.  
  
3.  Dos **dados do relatório** painel, arraste o `Date` campo para o **grupos de linhas** painel. Coloque-o acima da linha chamada **(Detalhes)**.  
  
     Observe que a alça de linha agora exibe um colchete para mostrar um grupo. A tabela também tem duas colunas Data – uma em cada lado de uma linha pontilhada vertical.  
  
     ![](../../2014/tutorials/media/rs-basictablegroups1design.gif "rs_BasicTableGroups1Design")  
  
4.  Dos **dados do relatório** painel, arraste o `Order` campo para o **grupos de linhas** painel. Coloque-o abaixo de Data e acima de **(Detalhes)**.  
  
     Observe que a alça de linha agora exibe dois colchetes para mostrar dois grupos. A tabela tem agora duas `Order` colunas, muito.  
  
5.  Exclua as colunas de data e a ordem originais para o **certa** da linha dupla. Isso removerá os valores do registro individual para que apenas o valor do grupo seja exibido. Selecione as alças de coluna das duas colunas, clique com o botão direito do mouse e clique em **Excluir Colunas**.  
  
     ![Selecionar colunas a serem excluídas](../../2014/tutorials/media/rs-basictablegroupsdeletecols.gif "Selecionar colunas a serem excluídas")  
  
     Você pode formatar os cabeçalhos de coluna e a data novamente.  
  
6.  Alterne para a guia **Visualizar** para visualizar o relatório. Sua aparência deve ser similar a esta ilustração:  
  
     ![Tabela agrupada por data e, em seguida, ordem](../../2014/tutorials/media/rs-basictablegroupspreview.gif "Tabela agrupada por data e, em seguida, ordem")  
  
##  <a name="bkmk_addtotals"></a> Para adicionar totais a um relatório  
  
1.  Alterne para o modo Design.  
  
2.  Clique com o botão direito do mouse na célula da região de dados que contém o campo `[LineTotal]`e clique em **Adicionar Total**.  
  
     Isso adicionará uma linha com uma soma do valor monetário de cada pedido.  
  
3.  Clique com o botão direito do mouse na célula que contém o campo `[Qty]`e clique em **Adicionar Total**.  
  
     Isso adicionará uma soma da quantidade de cada pedido à linha de total.  
  
4.  Na célula vazia à esquerda de `Sum[Qty]`, digite o rótulo "**Total de Pedidos"**.  
  
5.  Você pode adicionar uma cor do plano de fundo à linha de total. Selecione as duas células de soma e a célula de rótulo.  
  
6.  No menu **Formatar** , clique em **Cor do Plano de Fundo**, clique em **Cinza Claro**e clique em **OK**.  
  
     ![Modo de exibição de Design: tabela básica com total do pedido](../../2014/tutorials/media/rs-basictablesumlinetotaldesign.gif "Modo de exibição de Design: tabela básica com total do pedido")  
  
##  <a name="bkmk_adddailytotal"></a> Para adicionar um total diário a um relatório  
  
1.  Clique com botão direito na célula pedido, aponte para **Adicionar Total**e clique em **após**.  
  
     Isso adiciona uma nova linha contendo as somas da quantidade e valor monetário de cada dia e o rótulo "**Total**" na coluna pedido.  
  
2.  Digite o palavra **Diário** depois da palavra **Total** na mesma célula para que apareça **Total Diário**.  
  
3.  Selecione a célula **Total Diário** , as duas células **Soma** e a célula vazia entre eles.  
  
4.  No menu **Formatar** , clique em **Cor do Plano de Fundo**, clique em **Laranja**e clique em **OK**.  
  
     ![](../../2014/tutorials/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
##  <a name="bkmk_addgrandtotal"></a> Para adicionar um total geral a um relatório  
  
1.  Clique com o botão direito do mouse na célula Data, aponte para **Adicionar Total**e clique em **Após**.  
  
     Isso adiciona uma nova linha contendo as somas da quantidade e valor monetário de todo o relatório e o **Total** rotular no `Date` coluna.  
  
2.  Digite a palavra **Geral** depois da palavra **Total** na mesma célula para que apareça **Total Geral**.  
  
3.  Selecione a célula **Total Geral** , as duas células **Soma** e as células vazias entre eles.  
  
4.  No menu **Formatar** , clique em **Cor do Plano de Fundo**, clique em **Azul Claro**e clique em **OK**.  
  
     ![Modo de exibição de Design: total geral em tabela básica](../../2014/tutorials/media/rs-basictablesumgrandtotaldesign.gif "Modo de exibição de Design: total geral em tabela básica")  
  
5.  Clique em Visualizar.  
  
     A última página deve ter a seguinte aparência:  
  
     ![Visualização: tabela básica com total geral](../../2014/tutorials/media/rs-basictablesumgrandtotalpreview.gif "Visualização: tabela básica com total geral")  
  
##  <a name="bkmk_publishreport"></a> Para publicar o relatório ao servidor de relatório (opcional)  
  
1.  Uma etapa opcional é publicar o relatório concluído no servidor de relatório de modo nativo para que você possa exibir o relatório no Gerenciador de Relatórios.  
  
2.  Na barra de ferramentas, clique em **Projeto** e, em seguida, em **tutorial Propriedades...**.  
  
3.  No **TargetServerURL** digite o nome do nome do seu servidor de relatório, por exemplo **http://\<servername > / reportserver**  
  
4.  Clique em **OK**.  
  
5.  Na barra de ferramentas, clique em **Compilar** e, em seguida, em **Implantar tutorial**.  
  
     Se você vir uma mensagem semelhante à seguinte na janela de saída, ela indicará uma implantação com êxito.  
  
    > ------ Build started: Project: tutorial, Configuration: Debug ------Skipping 'Sales Orders.rdl'. Item está atualizado. Compilação concluída – 0 erros, 0 avisos---implantação iniciada: projeto: tutorial, configuração: Debug---implantação http://\<nome do servidor > / reportserverDeploying relatar '/ tutorial/Sales Orders'. Implantação concluída-- 0 erros, 0 avisos = = = Build: 1 com êxito ou atualizados, 0 falhou, 0 ignorado = = = Deploy: 1 com êxito, 0 falhou, 0 ignorado = = =  
  
     Se você vir uma mensagem de erro semelhante à seguinte, verifique se você tem permissões no servidor de relatório e se iniciou o [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] com privilégios de administrador.  
  
    > "As permissões concedidas ao usuário ' XXXXXXXX\\< seu nome de usuário\>' são insuficientes para realizar esta operação"  
  
6.  Iniciar o Gerenciador de relatórios com privilégios de administrador, por exemplo, clique com botão direito no ícone do Internet Explorer e clique em **executar como administrador**.  
  
     Navegue até a URL do Gerenciador de Relatórios, por exemplo: `http://<server name>/reports`.  
  
7.  Navegue até a pasta que contém o relatório e clique no nome do relatório `Sales Orders` para exibir o relatório renderizado no navegador.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você concluiu com êxito o tutorial Criando um relatório de tabela básico.  
  
## <a name="see-also"></a>Consulte também  
 [Filtrar, agrupar e classificar dados &#40;relatórios e SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
