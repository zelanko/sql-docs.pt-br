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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "69493860"
---
# <a name="defining-a-fact-relationship"></a>Definindo uma relação de fatos
  Algumas vezes, os usuários desejam dimensionar medidas por itens de dados que estão na tabela de fatos ou consultar a tabela de fatos em busca de informações relacionadas específicas, como, por exemplo, números de faturas ou de ordens de compra relacionados a determinados fatos de vendas. Ao definir uma dimensão com base em um item da tabela de fatos, a dimensão será chamada *dimensão de fatos*. As dimensões de fatos também são conhecidas como dimensões de degeneração. Elas são úteis para agrupar em conjunto as linhas de tabelas de fatos relacionadas, como, por exemplo, todas as linhas que estiverem relacionadas a um determinado número de fatura. Embora seja possível colocar essas informações em uma tabela de dimensões separada no banco de dados relacional, criar uma tabela de dimensões separada para essas informações não fornecerá benefício algum, pois a tabela de dimensões tende a aumentar na mesma proporção que a tabela de fatos, duplicando dados e tornando maior sua complexidade.  
  
 No [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você pode determinar se deseja duplicar os dados da dimensão de fatos em uma estrutura de dimensão MOLAP para aumentar o desempenho da consulta ou se deseja definir a dimensão de fatos como uma dimensão ROLAP para economizar mais espaço de armazenamento reduzindo o desempenho da consulta. Ao armazenar uma dimensão com o modo de armazenamento MOLAP, todos os membros da dimensão são armazenados na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em uma estrutura MOLAP altamente compactada, além de serem armazenados nas partições do grupo de medidas. Quando você armazena uma dimensão com o modo de armazenamento ROLAP, somente a definição da dimensão é armazenada na estrutura MOLAP – os próprios membros da dimensão são consultados da tabela de fatos relacional subjacente no momento da consulta. O modo de armazenamento apropriado pode ser definido com base na frequência em que a dimensão de fatos é consultada, no número de linhas retornada por uma consulta comum, no desempenho da consulta e no custo de processamento. A definição de uma dimensão como ROLAP não requer que todos os cubos que usam a dimensão também sejam armazenados no modo ROLAP. O modo de armazenamento de cada dimensão pode ser configurado independentemente.  
  
 Quando você define uma dimensão de fatos, é possível definir a relação entre a dimensão de fatos e o grupo de medidas como uma relação de fatos. As restrições a seguir se aplicam às relações de fatos:  
  
-   O atributo de granularidade deve ser a coluna chave da dimensão, que cria uma relação um-para-um entre a dimensão e os fatos na tabela de fatos.  
  
-   Uma dimensão pode ter uma relação de fatos apenas com um único grupo de medidas.  
  
> [!NOTE]  
>  As dimensões de fatos devem ser atualizadas incrementalmente após cada atualização do grupo de medidas referenciada pela relação de fatos.  
  
 Para obter mais informações, consulte [Relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)e [Definir uma relação de fatos e as propriedades da relação fatos](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
 Nas tarefas deste tópico, você adiciona uma nova dimensão de cubo com base na coluna **CustomerPONumber** da tabela de fatos **FactInternetSales** . Em seguida, você define a relação entre essa nova dimensão de cubo e o grupo de medidas **Vendas pela Internet** como uma relação de fatos.  
  
## <a name="defining-the-internet-sales-orders-fact-dimension"></a>Definindo a dimensão de fatos dos pedidos de venda pela Internet  
  
1.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **dimensões**e clique em **nova dimensão**.  
  
2.  Na página **Bem-vindo ao Assistente para Dimensões** , clique em **Avançar**.  
  
3.  Na página **Selecionar Método de Criação** , verifique se a opção **Usar uma tabela existente** está selecionada e clique em **Avançar**.  
  
4.  Na página **Especificar Informações da Fonte** , verifique se a exibição da fonte de dados **Adventure Works DW 2012** está selecionada.  
  
5.  Na lista **Tabela principal** , selecione **InternetSales**.  
  
6.  Na lista **Colunas de chave** , verifique se **SalesOrderNumber** e **SalesOrderLineNumber** estão listados.  
  
7.  Na lista **Coluna de nome** , selecione **SalesOrderLineNumber**.  
  
8.  Clique em **Próximo**.  
  
9. Na página **Selecionar Tabelas Relacionadas** , desmarque as caixas de seleção ao lado de todas as tabelas e clique em **Avançar**.  
  
10. Na página **Selecionar Atributos de Dimensão** , clique duas vezes na caixa de seleção no cabeçalho para desmarcar todas as caixas. O atributo **Número do Pedido de Vendas** permanecerá selecionado porque é o atributo de chave.  
  
11. Selecione o atributo **Número da OC do Cliente** e clique em **Avançar**.  
  
12. Na página **Concluindo o Assistente** , altere o nome para **Detalhes do Pedido de Vendas pela Internet** e clique em **Concluir** para concluir o assistente.  
  
13. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
14. No painel **atributos** do designer de dimensão da dimensão **detalhes do pedido de vendas pela Internet** , selecione **número do pedido de vendas**e altere a propriedade **nome** no janela Propriedades para`Item Description.`  
  
15. Na célula da propriedade **NameColumn** , clique no botão procurar **(...)**. Na caixa de diálogo **coluna de nome** , selecione **produto** na lista **tabela de origem** , selecione **EnglishProductName** para a **coluna origem**e clique em **OK**.  
  
16. Adicione o atributo **Número do Pedido de Vendas** à dimensão arrastando a coluna **SalesOrderNumber** da tabela **InternetSales** no painel **Exibição da Fonte de Dados** até o painel **Atributos** .  
  
17. Altere a propriedade **nome** do atributo número do novo **pedido** de vendas `Order Number`para e altere a propriedade **OrderBy** para **chave**.  
  
18. No painel **hierarquias** , crie uma hierarquia de usuário **pedidos de vendas pela Internet** que `Order Number` contenha os níveis de descrição e de **Item** , nessa ordem.  
  
19. No painel **Atributos** , selecione **Detalhes do Pedido de Vendas pela Internet**e examine o valor da propriedade **StorageMode** na janela Propriedades.  
  
     Observe que, por padrão, essa dimensão é armazenada como uma dimensão MOLAP. Embora a alteração do modo de armazenamento para ROLAP economize tempo de processamento e espaço de armazenamento, ela reduz o desempenho da consulta. Apenas para a finalidade deste tutorial, você usará MOLAP como o modo de armazenamento.  
  
20. Para adicionar uma dimensão criada recentemente ao cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como uma dimensão do cubo, alterne para o **Designer de Cubo**. Na guia **Estrutura do Cubo** , clique com o botão direito do mouse no painel **Dimensões** e selecione **Adicionar Dimensão do Cubo**.  
  
21. Na caixa de diálogo **Adicionar Dimensão do Cubo**, selecione **Detalhes do Pedido de Vendas pela Internet** e clique em **OK**.  
  
## <a name="defining-a-fact-relationship-for-the-fact-dimension"></a>Definindo uma relação de fatos para a dimensão de fatos  
  
1.  No Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , clique na guia **Uso da Dimensão** .  
  
     Observe que a dimensão de cubo **Detalhes do Pedido de Vendas pela Internet** é configurada automaticamente como tendo uma relação de fatos, como mostra o ícone exclusivo.  
  
2.  Clique no botão procurar (**...**) na célula **Descrição do item** , na interseção do grupo de medidas **vendas pela Internet** e na dimensão **detalhes do pedido de vendas pela Internet** , para examinar as propriedades da relação de fatos.  
  
     A caixa de diálogo **Definir Relação** é aberta. Observe que nenhuma das propriedades pode ser configurada.  
  
     A imagem a seguir mostra as propriedades da relação de fatos na caixa de diálogo **Definir Relação** .  
  
     ![Caixa de diálogo Definir relação](../../2014/tutorials/media/l5-factrelationship-2.gif "Caixa de diálogo Definir Relação")  
  
3.  Clique em **Cancelar**.  
  
## <a name="browsing-the-cube-by-using-the-fact-dimension"></a>Navegando pelo cubo usando a dimensão de fatos  
  
1.  No menu **Criar** , clique em **Implantar Tutorial do Analysis Services** para implantar as alterações na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e processar o banco de dados.  
  
2.  Quando a implantação for concluída com êxito, clique na guia **Navegador** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique no botão **Reconectar** .  
  
3.  Desmarque todas as medidas e hierarquias do painel de dados e adicione a medida **Vendas pela Internet/Valor das Vendas** à área de dados do painel de dados.  
  
4.  No painel de metadados, expanda **Cliente**, **Local**, **Geografia do Cliente**, **Membros**, **Todos os Clientes**, **Austrália**, **Queensland**, **Brisbane**, **4000**, clique com o botão direito do mouse em **Adam Powell**e clique em **Adicionar ao Filtro**.  
  
     Usar um filtro para limitar os pedidos de vendas retornados a um único cliente permite ao usuário fazer uma busca detalhada nos detalhes subjacentes em uma ampla tabela de fatos sem sofrer uma perda significativa no desempenho da consulta.  
  
5.  Adicione a hierarquia definida pelo usuário **Pedidos de Vendas pela Internet** da dimensão **Detalhes do Pedido de Vendas pela Internet** à área de linhas do painel de dados.  
  
     Observe que os números do pedido de vendas e os valores correspondentes das vendas pela Internet em nome de Adam Powell aparecem no painel de dados.  
  
     A imagem a seguir mostra o resultado das etapas anteriores.  
  
     ![Dimensionamento de Vendas pela Internet-Valor das Vendas](../../2014/tutorials/media/l5-factrelationship-3.gif "Dimensionamento de Vendas pela Internet-Valor das Vendas")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Definindo uma relação muitos para muitos](lesson-5-3-defining-a-many-to-many-relationship.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Relações de dimensão](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Definir uma relação de fato e propriedades de relação de fato](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
