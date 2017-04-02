---
title: "Li&#231;&#227;o 5: Criar rela&#231;&#245;es | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Li&#231;&#227;o 5: Criar rela&#231;&#245;es
Nesta lição, você aprenderá a verificar as relações que foram criadas automaticamente quando os dados foram importados e adicionará novas relações entre tabelas diferentes. Uma relação é uma conexão criada entre duas tabelas que estabelece como os dados dessas tabelas devem ser correlacionados. Por exemplo, as tabelas Product e Product Subcategory têm uma relação baseada no fato de que cada produto pertence a uma subcategoria. Para obter mais informações, consulte [Relações &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 3: Renomear colunas](../analysis-services/lesson-3-rename-columns.md).  
  
## Revisar relações existentes e adicionar novas relações  
Ao importar dados usando o Assistente de Importação de Tabela, você importou sete tabelas do banco de dados AdventureWorksDW. Geralmente, se você importar dados de uma fonte relacional, os banco de dados existentes são importados automaticamente junto com os dados. No entanto, antes de dar continuidade à criação do modelo, você deve verificar se essas relações entre tabelas foram criadas corretamente. Para este tutorial, você adicionará também três novas relações.  
  
#### Para revisar relações existentes  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo**, aponte para **Exibição de Modelo** e clique em **Exibição de Diagrama**.  
  
    Agora, o designer de modelos aparece em Exibição de Diagrama, um formato gráfico que exibe todas as tabelas que você importou com linhas entre elas. As linhas entre tabelas indicam as relações que foram criadas automaticamente quando você importar os dados.  
  
    Use os controles de minimapa no canto inferior direito do designer de modelos para ajustar a exibição para que ela inclua o máximo de tabelas possível. Você também pode clicar e arrastar tabelas para locais diferentes, colocando-as mais próximas umas das outras ou colocando-as em uma ordem específica. A movimentação de tabelas não afeta as relações já existentes entre elas. Para exibir todas as colunas em uma tabela específica, clique e arraste em uma borda de tabela expandi-la ou reduzi-la.  
  
2.  Clique na linha sólida entre as tabelas **Cliente** e **Geografia**. A linha sólida entre essas duas tabelas mostra que essa relação está ativa, ou seja, ela é usada por padrão durante o cálculo das fórmulas DAX.  
  
    Observe que, agora, a coluna **ID da Geografia** da tabela **Cliente** e a coluna **ID da Geografia** da tabela **Geografia** são exibidas cada uma dentro de uma caixa. Isso mostra que elas são as colunas usadas na relação. Agora, as propriedades da relação também são exibidas na janela **Propriedades**.  
  
    > [!TIP]  
    > Além de usar o designer de modelos na exibição de diagrama, você também pode usar a caixa de diálogo **Gerenciar Relações** para mostrar as relações entre todas as tabelas em um formato de tabela. Clique no menu **Tabela** e clique em **Gerenciar Relações**. A caixa de diálogo **Gerenciar Relações** mostra as relações que foram criadas automaticamente quando os dados foram importados.  
  
3.  Use o designer de modelos na exibição de diagrama ou a caixa de diálogo **Gerenciar Relações** para verificar se as seguintes relações foram criadas quando cada uma das tabelas foi importada do banco de dados AdventureWorksDW:  
  
    |Ativa|Table|Tabela de Pesquisa Relacionada|  
    |----------|---------|------------------------|  
    |Sim|**Customer [Geography Id]**|**Geography [Geography Id]**|  
    |Sim|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |Sim|**Product Subcategory [Product Category Id]**|**Product Category [Product Category Id]**|  
    |Sim|**Internet Sales [Customer Id]**|**Customer [Customer Id]**|  
    |Sim|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
Se qualquer uma das relações na tabela acima estiver ausente, verifique se o modelo inclui as tabelas a seguir: Customer, Date, Geography, Product, Product Category, Product Subcategory e Internet Sales. Se as tabelas da mesma conexão de fonte de dados forem importadas em momentos distintos, não será criada nenhuma relação entre essas tabelas; essa relações deverão ser criadas manualmente.  
  
Em alguns casos, talvez seja necessário criar relações adicionais entre tabelas no modelo para oferecer suporte a uma lógica corporativa específica. Para este tutorial, você precisa criar três relações adicionais entre as tabelas Internet Sales e Date.  
  
#### Para adicionar novas relações entre tabelas  
  
1.  No designer de modelos, na tabela **Vendas pela Internet**, clique e mantenha o botão do mouse pressionado na coluna **Data do Pedido**, arraste o cursor até a coluna **Data** da tabela **Data** e solte o botão.  
  
    Uma linha sólida aparece, indicando que você criou uma relação ativa entre a coluna **Data do Pedido** da tabela **Vendas pela Internet** e a coluna **Data** da tabela **Data**.  
  
    > [!NOTE]  
    > Ao criar relações, a ordem entre a tabela primária e a tabela de pesquisa relacionada é colocada automaticamente na ordem correta.  
  
2.  No designer de modelos, na tabela **Vendas pela Internet**, clique e mantenha o botão do mouse pressionado na coluna **Data de Conclusão**, arraste o cursor até a coluna **Data** na tabela **Data** e solte o botão.  
  
    Uma linha pontilhada aparece, indicando que você criou uma relação inativa entre a coluna **Data de Conclusão** na tabela **Vendas pela Internet** e a coluna **Data** na tabela **Data**. Você pode ter várias relações entre tabelas, mas só uma relação pode estar ativa por vez.  
  
3.  Por fim, crie mais uma relação; na tabela **Vendas pela Internet**, clique e mantenha o botão do mouse pressionado na coluna **Data de Remessa**, arraste o cursor até a coluna **Data** na tabela **Data** e solte o botão.  
  
    Uma linha pontilhada aparece, indicando que você criou uma relação inativa entre a coluna **Data de Remessa** na tabela **Vendas pela Internet** e a coluna **Data** na tabela **Data**.  
  
## Próxima etapa  
Para continuar esta lição, vá para a próxima lição: [Lição 6: Criar colunas calculadas](../analysis-services/lesson-6-create-calculated-columns.md).  
  
  
  
