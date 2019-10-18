---
title: Definindo uma relação de fatos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4b49a078-6848-4286-bc71-cf4862d29064
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4408e9b884e2cb5a0b47d9e6f95a16dec2bd20f6
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493860"
---
# <a name="defining-a-fact-relationship"></a>Definindo uma relação de fatos
  Às vezes, os usuários desejam ser capazes de dimensionar medidas por itens de dados que estão na tabela de fatos ou consultar a tabela de fatos para obter informações adicionais relacionadas específicas, como números de fatura ou números de pedidos de compra relacionados a fatos de vendas específicos. Quando você define uma dimensão com base em um item de tabela de fatos, a dimensão é chamada de *dimensão de fatos*. As dimensões de fato também são conhecidas como dimensões de degeneração. As dimensões de fato são úteis para agrupar linhas de tabela de fatos relacionadas, como todas as linhas relacionadas a um número de fatura específico. Embora você possa colocar essas informações em uma tabela de dimensões separada no banco de dados relacional, a criação de uma tabela de dimensões separada para as informações não fornece nenhum benefício, pois a tabela de dimensões aumentaria na mesma taxa que a tabela de fatos e simplesmente criaria dados duplicados e complexidade desnecessária.  
  
 Em [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você pode determinar se deseja duplicar os dados da dimensão de fatos em uma estrutura de dimensão MOLAP para aumentar o desempenho da consulta ou se deseja definir a dimensão de fatos como uma dimensão ROLAP para economizar espaço de armazenamento às custas do desempenho da consulta. Quando você armazena uma dimensão com o modo de armazenamento MOLAP, todos os membros da dimensão são armazenados na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em uma estrutura MOLAP altamente compactada, além de serem armazenados nas partições do grupo de medidas. Quando você armazena uma dimensão com o modo de armazenamento ROLAP, somente a definição da dimensão é armazenada na estrutura MOLAP – os próprios membros da dimensão são consultados da tabela de fatos relacional subjacente no momento da consulta. Você decide o modo de armazenamento apropriado com base na frequência com que a dimensão de fatos é consultada, o número de linhas retornadas por uma consulta típica, o desempenho da consulta e o custo de processamento. Definir uma dimensão como ROLAP não requer que todos os cubos que usam a dimensão também sejam armazenados com o modo de armazenamento ROLAP. O modo de armazenamento para cada dimensão pode ser configurado independentemente.  
  
 Ao definir uma dimensão de fatos, você pode definir a relação entre a dimensão de fatos e o grupo de medidas como uma relação de fatos. As seguintes restrições se aplicam a relações de fatos:  
  
-   O atributo de granularidade deve ser a coluna de chave para a dimensão, que cria uma relação um-para-um entre a dimensão e os fatos na tabela de fatos.  
  
-   Uma dimensão pode ter uma relação de fato com apenas um único grupo de medidas.  
  
> [!NOTE]  
>  As dimensões de fato devem ser atualizadas incrementalmente após cada atualização para o grupo de medidas referenciado pela relação de fatos.  
  
 Para obter mais informações, consulte [relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)e [definir uma relação de fato e propriedades de relação de fato](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
 Nas tarefas deste tópico, você adiciona uma nova dimensão de cubo com base na coluna **CustomerPONumber** na tabela de fatos **FactInternetSales** . Em seguida, você define a relação entre essa nova dimensão de cubo e o grupo de medidas **vendas pela Internet** como uma relação de fatos.  
  
## <a name="defining-the-internet-sales-orders-fact-dimension"></a>Definindo a dimensão de fatos de pedidos de vendas pela Internet  
  
1.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **dimensões**e clique em **nova dimensão**.  
  
2.  Na página **Bem-vindo ao Assistente para dimensões** , clique em **Avançar**.  
  
3.  Na página **selecionar método de criação** , verifique se a opção **usar uma tabela existente** está selecionada e clique em **Avançar**.  
  
4.  Na página **especificar informações sobre a origem** , verifique se a exibição da fonte de dados **adventure works DW 2012** está selecionada.  
  
5.  Na lista **tabela principal** , selecione **InternetSales**.  
  
6.  Na lista **colunas de chave** , verifique se **SalesOrderNumber** e **SalesOrderLineNumber** estão listados.  
  
7.  Na lista **coluna de nome** , selecione **SalesOrderLineNumber**.  
  
8.  clique em **Avançar**.  
  
9. Na página **selecionar tabelas relacionadas** , desmarque as caixas de seleção ao lado de todas as tabelas e clique em **Avançar**.  
  
10. Na página **Selecionar atributos de dimensão** , clique duas vezes na caixa de seleção do cabeçalho para desmarcar todas as caixas de seleção. O atributo **número do pedido de vendas** permanecerá selecionado porque é o atributo de chave.  
  
11. Selecione o atributo **número da OC do cliente** e clique em **Avançar**.  
  
12. Na página **concluindo o assistente** , altere o nome para **detalhes do pedido de vendas pela Internet** e clique em **concluir** para concluir o assistente.  
  
13. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
14. No painel **atributos** do designer de dimensão da dimensão **detalhes do pedido de vendas pela Internet** , selecione **número do pedido de vendas**e altere a propriedade **nome** na janela Propriedades para `Item Description.`  
  
15. Na célula da propriedade **NameColumn** , clique no botão procurar **(...)** . Na caixa de diálogo **coluna de nome** , selecione **produto** na lista **tabela de origem** , selecione **EnglishProductName** para a **coluna origem**e clique em **OK**.  
  
16. Adicione o **atributo número do pedido de vendas** à dimensão arrastando a coluna **SalesOrderNumber** da tabela **InternetSales** no painel **exibição da fonte de dados** para o painel **atributos** .  
  
17. Altere a propriedade **nome** do atributo número do novo **pedido de vendas** para `Order Number` e altere a propriedade **OrderBy** para **chave**.  
  
18. No painel **hierarquias** , crie uma hierarquia de usuário **pedidos de vendas pela Internet** que contém os níveis de descrição de `Order Number` e **Item** , nessa ordem.  
  
19. No painel **atributos** , selecione **detalhes do pedido de vendas pela Internet**e examine o valor da propriedade **StorageMode** no janela Propriedades.  
  
     Observe que, por padrão, essa dimensão é armazenada como uma dimensão MOLAP. Embora a alteração do modo de armazenamento para ROLAP Economize tempo de processamento e espaço de armazenamento, ela ocorre às custas do desempenho da consulta. Para os fins deste tutorial, você usará MOLAP como o modo de armazenamento.  
  
20. Para adicionar uma dimensão criada recentemente ao cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como uma dimensão do cubo, alterne para o **Designer de Cubo**. Na guia **estrutura do cubo** , clique com o botão direito do mouse no painel **dimensões** e selecione **Adicionar dimensão do cubo**.  
  
21. Na caixa de diálogo **Adicionar dimensão do cubo**., selecione **detalhes do pedido de vendas pela Internet** e clique em **OK**.  
  
## <a name="defining-a-fact-relationship-for-the-fact-dimension"></a>Definindo uma relação de fatos para a dimensão de fatos  
  
1.  No designer de cubo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo de tutorial, clique na guia **uso da dimensão** .  
  
     Observe que a dimensão de cubo **detalhes do pedido de vendas pela Internet** é configurada automaticamente como tendo uma relação de fato, conforme mostrado pelo ícone exclusivo.  
  
2.  Clique no botão procurar ( **...** ) na célula **Descrição do item** , na interseção do grupo de medidas **vendas pela Internet** e na dimensão **detalhes do pedido de vendas pela Internet** , para examinar as propriedades da relação de fatos.  
  
     A caixa de diálogo **definir relação** é aberta. Observe que você não pode configurar nenhuma das propriedades.  
  
     A imagem a seguir mostra as propriedades da relação de fatos na caixa de diálogo **definir relação** .  
  
     ![Caixa de diálogo Definir relação](../../2014/tutorials/media/l5-factrelationship-2.gif "Caixa de diálogo Definir relação")  
  
3.  Clique em **Cancelar**.  
  
## <a name="browsing-the-cube-by-using-the-fact-dimension"></a>Navegando no cubo usando a dimensão de fatos  
  
1.  No menu **Compilar** , clique em **implantar Analysis Services tutorial** para implantar as alterações na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e processar o banco de dados.  
  
2.  Depois que a implantação for concluída com êxito, clique na guia **navegador** no designer de cubo para o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo de tutorial e clique no botão **reconectar** .  
  
3.  Desmarque todas as medidas e hierarquias do painel dados e, em seguida, adicione a medida **vendas pela Internet/valor das vendas** à área de dados do painel dados.  
  
4.  No painel metadados, expanda **cliente**, **local**, Geografia do **cliente**, **Membros**, **todos os clientes**, **Austrália**, expanda **Queensland**e **Brisbane**, Expanda **4000**, clique com o botão direito do mouse em **Adam Powell**e clique em **Adicionar ao filtro**.  
  
     A filtragem para limitar os pedidos de vendas retornados a um único cliente permite que o usuário faça uma busca detalhada dos detalhes subjacentes em uma tabela de fatos grande sem perder uma perda significativa no desempenho da consulta.  
  
5.  Adicione a hierarquia definida pelo usuário **ordens de vendas** pela Internet da dimensão detalhes do **pedido de vendas pela Internet** à área de linha do painel dados.  
  
     Observe que os números de ordem de venda e os valores de vendas pela Internet correspondentes para Adam Powell aparecem no painel de dados.  
  
     A imagem a seguir mostra o resultado das etapas anteriores.  
  
     ![Dimensão de vendas pela Internet-valor das vendas](../../2014/tutorials/media/l5-factrelationship-3.gif "Dimensão de vendas pela Internet-valor das vendas")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa na lição  
 [Definindo uma relação muitos-para-muitos](lesson-5-3-defining-a-many-to-many-relationship.md)  
  
## <a name="see-also"></a>Consulte também  
 @No__t_1 de [relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
 [Definir uma relação de fatos e as propriedades da relação de fatos](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
