---
title: Adicionar uma ação de expandir ou recolher (Construtor de Relatórios e SSRS) | Microsoft Docs
description: É possível habilitar um usuário para expandir ou recolher itens de maneira interativa em um relatório paginado. Ou para expandir ou recolher linhas e colunas associadas a um grupo para uma tabela ou matriz.
ms.date: 12/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 49f07ad6-242b-4861-8fc1-91ca78c36d6c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 776326093518aa33f8f031e4c4d6675791acf82d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242546"
---
# <a name="add-an-expand-or-collapse-action-to-an-item-report-builder--ssrs"></a>Adicionar uma ação de expandir ou recolher a um item (Construtor de Relatórios e SSRS)
  É possível habilitar um usuário para expandir ou recolher itens de maneira interativa em um relatório paginado. Ou para expandir ou recolher linhas e colunas associadas a um grupo para uma tabela ou matriz. Para permitir que os usuários expandam ou recolham um item, defina as propriedades de visibilidade do item. A definição de trabalhos de visibilidade em um visualizador de relatórios HTML às vezes é chamada de uma ação de *detalhamento* .  
  
 Na exibição de design de relatório, você especifica o nome da caixa de texto no relatório onde deseja exibir os ícones de alternância para expandir e recolher. No relatório renderizado, a caixa de texto exibe um sinal de mais (+) ou de menos (-) além de seu conteúdo. Quando o usuário clica na alternância, a exibição do relatório é atualizada para mostrar ou ocultar o item de relatório nas configurações de visibilidade atuais dos itens do relatório.  
  
 Em geral, as ações de expansão e recolhimento são usadas inicialmente para exibir apenas os dados de resumo e permitir que o usuário clique no sinal de adição para mostrar os dados detalhados. Por exemplo, é possível ocultar inicialmente uma tabela que exibe valores de um gráfico ou grupos filho de uma tabela com grupos de linhas e de colunas aninhados, como em um relatório detalhado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-expand-and-collapse-action-to-a-group"></a>Para adicionar uma ação de expansão e recolhimento a um grupo  
  
1.  Na exibição de design de relatório, clique na tabela ou na matriz para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas.  
  
     ![Painel Agrupamento](../../reporting-services/report-design/media/groupingpane.png "Painel Agrupamento")  
  
     Se o painel Agrupamento não aparecer, clique no menu **Exibir** e clique em **Agrupamento**.  
  
2.  Clique com o botão direito do mouse em qualquer lugar na barra de título do painel Agrupamento e clique em **Avançado**. O modo do painel Agrupamento é alternado para mostrar a estrutura de exibição subjacente de linhas e colunas na superfície de design.  
  
     ![Painel Agrupamento com o menu Modo Avançado](../../reporting-services/report-design/media/groupingpane-advancedmode.png "Painel Agrupamento com o menu Modo Avançado")  
  
3.  No painel de grupo apropriado, clique no nome do grupo de linhas ou de colunas do qual você deseja ocultar as linhas ou colunas associadas. O grupo é selecionado e o painel Propriedades mostra as propriedades do **Membro do Tablix** .  
  
    > [!NOTE]  
    >  Se o painel Propriedades não for exibido, clique em **Exibir** na Faixa de opções e clique em **Propriedades**.  
  
4.  Em **Oculto**, escolha uma das opções a seguir para definir a visibilidade desse item de relatório na primeira vez em que o relatório for executado:  
  
    -   Selecione **False** para exibir o item de relatório.  
  
    -   Selecione **True** para ocultar o item de relatório.  
  
    -   Selecione **\<Expression>** para abrir a caixa de diálogo **Expressão** para criar uma expressão que é avaliada em tempo de execução para determinar a visibilidade.  
  
5.  Em **ToggleItem**, na caixa suspensa, selecione o nome de uma caixa de texto à qual adicionar a imagem de alternância.  
  
     Na imagem a seguir, o grupo de linhas Cor está configurado para permitir que os usuários expandam e recolham linhas associadas.  
  
     ![Como configurar um grupo de linhas a ser expandido](../../reporting-services/report-design/media/expandcollapse-confighiddentoggleitemwithnumbers.png "Como configurar um grupo de linhas a ser expandido")  
  
    > [!NOTE]  
    >  A caixa de texto com a imagem de alternância não pode ser o grupo de linhas ou de colunas do qual você deseja ocultar as linhas ou colunas associadas. Ela deve estar no mesmo grupo que o item que está sendo ocultado ou em um grupo ancestral. Por exemplo, para alternar a visibilidade de linhas associadas a um grupo filho, selecione uma caixa de texto em uma linha associada ao grupo pai.  
  
6.  Para testar a alternância, execute o relatório e clique na caixa de texto com a imagem de alternância. A exibição do relatório é atualizada para mostrar grupos de linhas e de colunas com a visibilidade alternada.  
  
     ![Executar relatório com um grupo de linhas expansível](../../reporting-services/report-design/media/expandcollapse-runreport-rowgroup.png "Executar relatório com um grupo de linhas expansível")  
  
### <a name="to-add-expand-and-collapse-action-to-a-report-item"></a>Para adicionar uma ação de expansão e recolhimento a um item de relatório  
  
1.  No modo de exibição de Design de relatório, clique com o botão direito do mouse no item de relatório para mostrar ou ocultar. Em seguida, clique em *\<item de relatório >* **Propriedades**. A caixa de diálogo *\<item de relatório>* **Propriedades** para o item de relatório abrirá.  
  
2.  Clique em **Visibilidade**.  
  
3.  Em **Quando o relatório for executado inicialmente**, escolha uma das opções a seguir para definir a visibilidade desse item de relatório na primeira vez em que o relatório for executado:  
  
    -   Selecione **Mostrar** para exibir o item de relatório.  
  
    -   Selecione **Ocultar** para ocultar o item de relatório.  
  
    -   Selecione **Mostrar ou ocultar com base em uma expressão** para usar uma expressão avaliada em tempo de execução para determinar a visibilidade. Clique em (**fx**) para abrir a caixa de diálogo **Expressão** para criar uma expressão.  
  
        > [!NOTE]  
        >  Quando você especifica uma expressão para visibilidade, está configurando a propriedade Hidden do item de relatório. A expressão avalia como um valor **Booliano** **True** para ocultar o item e **False** para mostrar o item.  
  
4.  Em **A exibição pode ser alternada por este item de relatório**, na caixa suspensa, digite ou selecione o nome de uma caixa de texto no relatório na qual exibir uma imagem de alternância, por exemplo, Textbox1.  
  
     Na imagem a seguir, a tabela está configurada para permitir que os usuários expandam e recolham-na. A exibição da tabela é alternada pela caixa de texto Tabela de Produtos.  
  
     ![Configure uma tabela de relatório a ser expandida](../../reporting-services/report-design/media/expandcollapse-reporttable.png "Configure uma tabela de relatório a ser expandida")  
  
    > [!NOTE]  
    >  A caixa de texto que você escolher deve estar no escopo atual ou de contenção para esse item de relatório (até e incluindo o corpo do relatório). Por exemplo, para alternar a visibilidade de um gráfico, selecione uma caixa de texto que esteja no mesmo escopo de contenção que o gráfico. Por exemplo, o corpo do relatório ou um retângulo. A caixa de texto deve estar na mesma ou em uma hierarquia de contêiner superior.  
  
5.  Para testar a alternância, execute o relatório e clique na caixa de texto com a imagem de alternância. A exibição do relatório é atualizada para mostrar itens de relatório com a visibilidade alternada.  
  
     ![Executar relatório com uma tabela de expansão](../../reporting-services/report-design/media/expandcollapse-runreport-reporttable.png "Executar relatório com uma tabela de expansão")  
  
## <a name="see-also"></a>Consulte Também  
 [Ação de análise detalhada &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [Ocultar um item &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
