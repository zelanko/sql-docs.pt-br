---
title: "Criar um relatório de nível (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5933c4f0-c713-4ecb-b521-ff46c9c63fff
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c78e1a3998673851e9860a6e6a6e295cde2d7f3e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-stepped-report-report-builder-and-ssrs"></a>Criar um novo relatório de nível (Construtor de Relatórios e SSRS)
Um relatório de nível é um tipo de relatório paginado do  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que mostra as linhas ou grupos filho de detalhes recuados sob um grupo pai na mesma coluna, conforme ilustrado no seguinte exemplo:  
  
 ![Relatório de nível renderizado](../../reporting-services/report-design/media/steppedreportrendered.gif "Relatório de nível renderizado")  
  
 Os relatórios de tabela tradicionais colocam o grupo pai em uma coluna adjacente no relatório. A nova região de dados tablix permite adicionar um grupo e linhas ou grupos filho de detalhe à mesma coluna. Para diferenciar as linhas de grupo de linhas de detalhes ou de grupos filho, você pode aplicar uma formatação, como cor da fonte, ou recuar as linhas de detalhes.  
  
 Os procedimentos neste tópico mostram como criar manualmente um relatório de nível, mas você também pode usar o Assistente de Nova Tabela e Matriz. Ele fornece o layout para relatórios de nível, tornando fácil criá-los. Depois de concluir o assistente, você poderá aperfeiçoar ainda mais o relatório.  
  
> [!NOTE]  
>  O assistente só está disponível no Construtor de Relatórios.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-stepped-report"></a>Para criar um relatório de nível  
  
1.  Crie um relatório de tabela. Por exemplo, insira uma região de dados tablix e adicione campos à linha Dados.  
  
2.  Adicione um grupo pai ao relatório.  
  
    1.  Clique em qualquer lugar da tabela para selecioná-la. O painel Agrupamento exibe o grupo Detalhes no painel Grupos de Linha.  
  
    2.  No painel Agrupamento, clique com o botão direito do mouse em Grupo de Detalhes, aponte para **Adicionar Grupo**e clique em **Grupo Pai**.  
  
    3.  Na caixa de diálogo **Grupo Tablix** , forneça um nome para o grupo e digite ou selecione uma expressão de grupo na lista suspensa. A lista suspensa exibe as expressões de campo simples que estão disponíveis no painel de Dados do Relatório. Por exemplo, [PostalCode] é uma expressão de campo simples para o campo PostalCode em um conjunto de dados.  
  
    4.  Selecione **Adicionar cabeçalho de grupo**. Esta opção adiciona uma linha estática acima do grupo para o rótulo do grupo e os totais do grupo. Da mesma forma, você pode selecionar **Adicionar rodapé de grupo** para adicionar uma linha estática sob o grupo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Você tem agora, um relatório tabular básico. Quando ele for renderizado, você poderá ver uma coluna com o valor da instância do grupo, e uma ou mais colunas com os dados dos detalhes agrupados. A figura a seguir mostra como pode ser a aparência da região de dados na superfície de design.  
  
     ![Região de dados de tabela com grupo](../../reporting-services/report-design/media/tabledataregionwithgroup.gif "Região de dados de tabela com grupo")  
  
     A figura a seguir mostra como pode ser a aparência da região de dados renderizada quando você visualizar o relatório.  
  
     ![Relatório agrupado renderizado](../../reporting-services/report-design/media/tablereportrendered.gif "Relatório agrupado renderizado")  
  
3.  Em um relatório de nível, você não precisa da primeira coluna que mostra a instância de grupo. Em vez disso, copie o valor na célula de cabeçalho do grupo, exclua a coluna do grupo e cole na primeira caixa de texto na linha de cabeçalho do grupo. Para remover a coluna de grupo, clique com o botão direito do mouse na coluna de grupo ou na célula e clique em **Excluir Colunas**. A figura a seguir mostra como pode ser a aparência da região de dados na superfície de design.  
  
     ![Região de dados com linha de cabeçalho de grupo](../../reporting-services/report-design/media/tabledataregiongroupheader.gif "Região de dados com linha de cabeçalho de grupo")  
  
4.  Para recuar as linhas de detalhes sob a linha de cabeçalho do grupo na mesma coluna, altere o preenchimento da célula de dados de detalhes.  
  
    1.  Selecione a célula com o campo de detalhes que você quer recuar. As propriedades da caixa de texto dessa célula aparecem no painel Propriedades.  
  
    2.  No painel Propriedades, em **Alinhamento**, expanda as propriedades para **Preenchimento**.  
  
    3.  Em **Esquerda**, digite um valor de preenchimento novo, como **.5in**. O preenchimento recua o texto na célula pelo valor que você especificar. O preenchimento padrão é 2 pontos. Os valores válidos para as propriedades de preenchimento são um número de zero ou um número maior, positivo, seguido por um designador de tamanho.  
  
         Os designadores de tamanho são:  
  
        |||  
        |-|-|  
        |**Em**|Polegadas (1 polegada = 2,54 centímetros)|  
        |**cm**|Centímetros|  
        |**mm**|Milímetros|  
        |**pt**|Pontos (1 ponto = 1/72 polegada)|  
        |**pc**|Picas (1 pica = 12 pontos)|  
  
     Sua região de dados será semelhante ao exemplo a seguir.  
  
     ![Região de dados para o relatório de nível](../../reporting-services/report-design/media/steppedreportdataregion.gif "Região de dados para o relatório de nível")  
  
     **Região de dados para layout de relatório de nível**  
  
     Na guia **Página Inicial** , clique em **Executar**. O relatório exibe o grupo com os níveis de recuo para os valores do grupo filho.  
  
## <a name="to-create-a-stepped-report-with-multiple-groups"></a>Para criar um relatório de nível com vários grupos  
  
1.  Crie um relatório conforme descrito no procedimento anterior.  
  
2.  Acrescente grupos adicionais ao seu relatório.  
  
    1.  No painel Grupos de Linha, clique com o botão direito do mouse no grupo, clique em **Adicionar Grupo**e escolha o tipo de grupo que deseja adicionar.  
  
        > [!NOTE]  
        >  Há várias maneiras para acrescentar grupos a uma região de dados. Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
    2.  Na caixa de diálogo **Grupo Tablix** , digite um nome.  
  
    3.  Em **Expressão de grupo**, digite uma expressão ou selecione um campo do conjunto de dados para agrupar. Para criar uma expressão, clique no botão de expressão (**fx**) para abrir a caixa de diálogo **Expressão** .  
  
    4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Altere o preenchimento da célula que exibe os dados do grupo.  
  
## <a name="see-also"></a>Consulte também  
 [Cabeçalhos e rodapés de página &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
