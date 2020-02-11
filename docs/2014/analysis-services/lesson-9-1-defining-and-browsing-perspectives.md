---
title: Definindo e procurando perspectivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 766004b9-6578-4914-a445-6f44843a5fb0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7889bb81d9bb1f1e3fefa229c0a6a0ee0dc1f1dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "69493772"
---
# <a name="defining-and-browsing-perspectives"></a>Definindo e procurando perspectivas
  Uma perspectiva pode simplificar a exibição de um cubo para propósitos específicos. Por padrão, os usuários podem ver todos os elementos em um cubo para o qual têm permissões. O quê os usuários visualizam ao exibir um cubo completo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é a perspectiva padrão para o cubo. Uma exibição de todo o cubo pode ser muito complexa para os usuários pesquisarem, principalmente para usuários que precisam apenas interagir com uma pequena parte do cubo para satisfazer seus requisitos de inteligência empresarial e geração de relatórios.  
  
 Para reduzir a aparente complexidade de um cubo, você pode criar subconjuntos visíveis do cubo, chamados *perspectivas*, que mostram aos usuários somente uma parte dos grupos de medidas, medidas, dimensões, atributos, hierarquias, KPIs (Indicadores Chave de Desempenho), ações e membros calculados no cubo. Isso pode ser particularmente útil para trabalhar com aplicativos cliente que foram escritos em uma versão anterior do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Esses clientes não têm conceito de exibição de pastas ou perspectivas, por exemplo, mas uma perspectiva é exibida para clientes antigos como se fosse um cubo. Para obter mais informações, consulte [Perspectivas](multidimensional-models-olap-logical-cube-objects/perspectives.md)e [Perspectivas em modelos multidimensionais](multidimensional-models/perspectives-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Uma perspectiva não é um mecanismo de segurança; é na verdade uma ferramenta que fornece uma experiência melhor ao usuário. Toda a segurança de uma perspectiva é herdada do cubo subjacente.  
  
 Nas tarefas deste tópico, você definirá várias perspectivas diferentes e depois navegará no cubo usando essas novas perspectivas.  
  
## <a name="defining-an-internet-sales-perspective"></a>Definindo uma perspectiva Vendas pela Internet  
  
1.  Abra o Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique na guia **Perspectivas** .  
  
     Todos os objetos e seus tipos de objeto são exibidos no painel **Perspectivas** , como mostra a imagem a seguir.  
  
     ![Painel Perspectivas do Designer de Cubo](../../2014/tutorials/media/l9-perspectives-1.gif "Painel Perspectivas do Designer de Cubo")  
  
2.  Na barra de ferramentas da guia **Perspectivas** , clique no botão **Nova Perspectiva** .  
  
     Uma nova perspectiva é exibida na coluna **Nome da Perspectiva** com o nome padrão **Perspectiva**, como mostra a imagem a seguir. Observe que a caixa de seleção de cada objeto está selecionada. Até que você desmarque a caixa de seleção de um objeto, essa perspectiva é idêntica à perspectiva padrão deste cubo.  
  
     ![Nova perspectiva na coluna Nome da Perspectiva](../../2014/tutorials/media/l9-perspectives-2.gif "Nova perspectiva na coluna Nome da Perspectiva")  
  
3.  Altere o nome da perspectiva `Internet Sales`para.  
  
4.  Na próxima linha, defina DefaultMeasure como **Vendas pela Internet/Valor das Vendas**.  
  
     Quando os usuários procurarem no cubo usando essa perspectiva, esta será a medida que eles verão, a menos que especifiquem alguma outra medida.  
  
    > [!NOTE]  
    >  Também é possível definir a medida padrão para todo o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na guia **Estrutura do Cubo** na janela Propriedades do cubo.  
  
5.  Desmarque a caixa de seleção dos seguintes objetos:  
  
    -   `Reseller Sales`grupo de medidas  
  
    -   Grupo de medidas **cotas de vendas**  
  
    -   Grupo de medidas **cotas de vendas 1**  
  
    -   Dimensão do cubo do **revendedor**  
  
    -   Dimensão do cubo de **Geografia do revendedor**  
  
    -   Dimensão do cubo de **região de vendas**  
  
    -   Dimensão do cubo do **funcionário**  
  
    -   Dimensão do cubo de **promoção**  
  
    -   **Receita do revendedor** KPI  
  
    -   Conjunto nomeado de **revendedores grandes**  
  
    -   Membro calculado do **valor total de vendas**  
  
    -   Membro calculado **custo total do produto**  
  
    -   Membro calculado do **GPM do revendedor**  
  
    -   Membro calculado do **GPM total**  
  
    -   Membro calculado **taxa de vendas do revendedor para todos os produtos**  
  
    -   Membro calculado da **taxa de vendas total para todos os produtos**  
  
     Esses objetos não estão relacionados às vendas pela Internet.  
  
    > [!NOTE]  
    >  Dentro de cada dimensão, você também pode selecionar individualmente as hierarquias e atributos definidos pelos usuários que você quer que apareçam na perspectiva.  
  
## <a name="defining-a-reseller-sales-perspective"></a>Definindo a perspectiva Vendas do Revendedor  
  
1.  Na barra de ferramentas da guia **Perspectivas** , clique no botão **Nova Perspectiva** .  
  
2.  Altere o nome da nova perspectiva para `Reseller Sales`.  
  
3.  Defina **Vendas do Revendedor/Valor das Vendas** como a medida padrão.  
  
     Quando os usuários navegarem pelo cubo usando essa perspectiva, essa será a medida que eles verão, a menos que especifiquem alguma outra medida.  
  
4.  Desmarque a caixa de seleção dos seguintes objetos:  
  
    -   `Internet Sales`grupo de medidas  
  
    -   Grupo de medidas **motivo de vendas pela Internet**  
  
    -   Dimensão do cubo do **cliente**  
  
    -   Dimensão do cubo **detalhes do pedido de vendas pela Internet**  
  
    -   Dimensão do cubo **motivo de vendas**  
  
    -   Ação de detalhamento da ação de detalhamento de **vendas pela Internet**  
  
    -   Membro calculado do **valor total de vendas**  
  
    -   Membro calculado **custo total do produto**  
  
    -   Membro calculado do **GPM de Internet**  
  
    -   Membro calculado do **GPM total**  
  
    -   Membro calculado **taxa de vendas pela Internet para todos os produtos**  
  
    -   Membro calculado da **taxa de vendas total para todos os produtos**  
  
     Esses objetos não estão relacionados às vendas do revendedor.  
  
## <a name="defining-a-sales-summary-perspective"></a>Definindo uma perspectiva Resumo das Vendas  
  
1.  Na barra de ferramentas da guia **Perspectivas** , clique no botão **Nova Perspectiva** .  
  
2.  Altere o nome da nova perspectiva para `Sales Summary`.  
  
    > [!NOTE]  
    >  Você não pode especificar uma medida calculada como a medida padrão.  
  
3.  Desmarque a caixa de seleção dos seguintes objetos:  
  
    -   `Internet Sales`grupo de medidas  
  
    -   `Reseller Sales`grupo de medidas  
  
    -   Grupo de medidas **motivo de vendas pela Internet**  
  
    -   Grupo de medidas **cotas de vendas**  
  
    -   Grupo de medidas **Sales Quotas1**  
  
    -   Dimensão do cubo **detalhes do pedido de vendas pela Internet**  
  
    -   Dimensão do cubo **motivo de vendas**  
  
    -   Ação de detalhamento da ação de detalhamento de **vendas pela Internet**  
  
4.  Selecione a caixa de seleção dos seguintes objetos:  
  
    -   Medida de **contagem de vendas pela Internet**  
  
    -   Medida de **contagem de vendas do revendedor**  
  
## <a name="browsing-the-cube-through-each-perspective"></a>Navegando no cubo usando cada perspectiva  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação for concluída com êxito, mude para a guia **Navegador** e clique no botão **Reconectar** .  
  
3.  Inicie o Excel.  
  
4.  A análise no Excel avisa para você escolher quais perspectivas devem ser usadas ao procurar o modelo no Excel, conforme mostrado na imagem a seguir.  
  
     ![Objetos para a perspectiva Vendas pela Internet](../../2014/tutorials/media/l9-perspectives-3.gif "Objetos para a perspectiva Vendas pela Internet")  
  
5.  Como alternativa, você pode iniciar o Excel no menu Iniciar do Windows, definir uma conexão com o banco de dados de tutorial do Analysis Services no localhost, e pode escolher uma perspectiva no assistente de Conexão de Dados, como mostrado na imagem a seguir.  
  
     ![Assistente de Conexão de Dados no Excel](../../2014/tutorials/media/l9-perspectives-3b.gif "Assistente de Conexão de Dados no Excel")  
  
6.  Selecione `Internet Sales` na lista **perspectiva** e, em seguida, examine as medidas e dimensões no painel metadados.  
  
     Observe que somente aqueles objetos especificados na perspectiva Vendas pela Internet são exibidos.  
  
7.  No painel de metadados, expanda **Medidas**.  
  
     Observe que apenas o `Internet Sales` grupo de medidas aparece, junto com o **GPM da Internet** e a taxa de **vendas pela Internet para** membros calculados de todos os produtos.  
  
8.  No modelo, selecione Excel novamente. Selecione `Sales Summary`.  
  
     Observe que em cada grupo de medidas, somente uma medida é exibida, como mostra a imagem a seguir:  
  
     ![Medidas Vendas pela Internet e Vendas do Revendedor](../../2014/tutorials/media/l9-perspectives-4.gif "Medidas Vendas pela Internet e Vendas do Revendedor")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Definindo e procurando traduções](lesson-9-2-defining-and-browsing-translations.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Perspectivas](multidimensional-models-olap-logical-cube-objects/perspectives.md)   
 [Perspectivas em modelos multidimensionais](multidimensional-models/perspectives-in-multidimensional-models.md)  
  
  
