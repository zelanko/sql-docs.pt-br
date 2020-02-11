---
title: 'Lição 5: criar relações | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a80f607c3187e967404ce018b7eed00497d9c01
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078576"
---
# <a name="lesson-5-create-relationships"></a>Lição 5: Criar relações
  Nesta lição, você aprenderá a verificar as relações que foram criadas automaticamente quando os dados foram importados e adicionará novas relações entre tabelas diferentes. Uma relação é uma conexão entre duas tabelas que estabelece como os dados nessas tabelas devem ser correlacionados. Por exemplo, as tabelas Product e Product Subcategory têm uma relação baseada no fato de que cada produto pertence a uma subcategoria. Para obter mais informações, consulte [Relações &#40;SSAS Tabular&#41;](tabular-models/relationships-ssas-tabular.md).  
  
 Tempo estimado para conclusão desta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 3: Renomear colunas](rename-columns.md).  
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Revisar relações existentes e adicionar novas relações  
 Ao importar dados usando o Assistente de Importação de Tabela, você importou sete tabelas do banco de dados AdventureWorksDW. Geralmente, se você importar dados de uma fonte relacional, os banco de dados existentes são importados automaticamente junto com os dados. No entanto, antes de prosseguir com a criação de seu modelo, você deve verificar se essas relações entre tabelas foram criadas corretamente. Para este tutorial, você também adicionará três novas relações.  
  
#### <a name="to-review-existing-relationships"></a>Para examinar relações existentes  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** , aponte para **Exibição de Modelo**e clique em **Exibição de Diagrama**.  
  
     O designer de modelo agora aparece na Exibição de Diagrama, um formato gráfico que exibe todas as tabelas que você importou com linhas entre elas. As linhas entre as tabelas indicam as relações que foram criadas automaticamente quando você importou os dados.  
  
     Use os controles de minimapa no canto superior direito do designer de modelos para ajustar a exibição de modo que ela inclua o máximo de tabelas possível. Também é possível clicar e arrastar tabelas para locais diferentes, aproximando as tabelas ou colocando-as em uma ordem específica. Mover tabelas não afeta as relações já existentes entre elas. Para exibir todas as colunas em uma tabela específica, clique e arraste uma borda de tabela para expandi-la ou diminuí-la.  
  
2.  Clique na linha sólida entre as tabelas **Cliente** e **Geografia** . A linha sólida entre essas duas tabelas mostra que essa relação está ativa, ou seja, ela é usada por padrão ao calcular fórmulas DAX.  
  
     Observe que, agora, a coluna **ID da Geografia** da tabela **Cliente** e a coluna **ID da Geografia** da tabela **Geografia** são exibidas cada uma dentro de uma caixa. Isso mostra que essas são as colunas usadas na relação. As propriedades da relação agora também aparecem na janela **Propriedades** .  
  
    > [!TIP]  
    >  Além de usar o designer de modelos na exibição de diagrama, você também pode usar a caixa de diálogo **gerenciar relações** para mostrar as relações entre todas as tabelas em um formato de tabela. Clique no menu **Tabela** e clique em **Gerenciar Relações**. A caixa de diálogo **Gerenciar Relações** mostra as relações que foram criadas automaticamente quando os dados foram importados.  
  
3.  Use o designer de modelos na exibição de diagrama ou a caixa de diálogo **gerenciar relações** para verificar se as seguintes relações foram criadas quando cada uma das tabelas foi importada do banco de dados AdventureWorksDW:  
  
    |Ativo|Tabela|Tabela de Pesquisa Relacionada|  
    |------------|-----------|--------------------------|  
    |Sim|**Customer [Geography Id]**|**Geography [Geography Id]**|  
    |Sim|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |Sim|**Product Subcategory [Product Category Id]**|**Product Category [Product Category Id]**|  
    |Sim|**Internet Sales [Customer Id]**|**Customer [Customer Id]**|  
    |Sim|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
 Se qualquer uma das relações na tabela acima estiver ausente, verifique se o modelo inclui as tabelas a seguir: Customer, Date, Geography, Product, Product Category, Product Subcategory e Internet Sales. Se as tabelas da mesma conexão de fonte de dados forem importadas em momentos distintos, eventuais relações entre essas tabelas não serão criadas e deverão ser criadas manualmente.  
  
 Em alguns casos, talvez seja necessário criar relações adicionais entre tabelas no modelo para dar suporte a determinadas lógicas de negócios. Para este tutorial, você precisa criar três relações adicionais entre as tabelas Internet Sales e Date.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Para adicionar novas relações entre tabelas  
  
1.  No designer de modelos, na tabela **Vendas pela Internet** , clique e mantenha o botão do mouse pressionado na coluna **Data do Pedido** , arraste o cursor até a coluna **Data** da tabela **Data** e solte o botão.  
  
     Uma linha sólida aparece, indicando que você criou uma relação ativa entre a coluna **Data do Pedido** da tabela **Vendas pela Internet** e a coluna **Data** da tabela **Data** .  
  
    > [!NOTE]  
    >  Ao criar relações, a ordem entre a tabela primária e a tabela de pesquisa relacionada é colocada automaticamente na ordem correta.  
  
2.  No designer de modelos, na tabela **Vendas pela Internet** , clique e mantenha o botão do mouse pressionado na coluna **Data de Conclusão** , arraste o cursor até a coluna **Data** na tabela **Data** e solte o botão.  
  
     Uma linha pontilhada aparece, indicando que você criou uma relação inativa entre a coluna **Data de Conclusão** na tabela **Vendas pela Internet** e a coluna **Data** na tabela **Data** . Você pode ter várias relações entre tabelas, mas somente uma relação pode estar ativa por vez.  
  
3.  Por fim, crie mais uma relação; na tabela **Vendas pela Internet** , clique e mantenha o botão do mouse pressionado na coluna **Data de Remessa** , arraste o cursor até a coluna **Data** na tabela **Data** e solte o botão.  
  
     Uma linha pontilhada aparece, indicando que você criou uma relação inativa entre a coluna **Data de Remessa** na tabela **Vendas pela Internet** e a coluna **Data** na tabela **Data** .  
  
## <a name="next-step"></a>Próxima etapa  
 Para continuar esta lição, vá para a próxima lição: [Lição 6: Criar colunas calculadas](lesson-5-create-calculated-columns.md).  
  
  
