---
title: "Li&#231;&#227;o 7: Criar medidas | Microsoft Docs"
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
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Li&#231;&#227;o 7: Criar medidas
Nesta lição, você criará medidas a serem incluída no modelo. Semelhante às colunas calculadas que você criou na lição anterior, uma medida é essencialmente um cálculo criado por meio de uma fórmula DAX. No entanto, diferente das colunas calculadas, são avaliadas medidas com base em um *filtro*selecionado pelo usuário; por exemplo, uma coluna ou uma segmentação de dados adicionada ao campo Rótulos de Linha em um Tabela Dinâmica.   Um valor para cada célula no filtro é calculado pela medida aplicada. As medidas são cálculos avançados e flexíveis que você incluirá em quase todos os modelos de tabela, a fim de executar cálculos dinâmicos em dados numéricos. Para saber mais, consulte [Medidas &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/measures-ssas-tabular.md).  
  
Para criar medidas, você usará a grade de medida. Por padrão, cada tabela tem uma grade de medida vazia; porém, você não criará medidas normalmente para cada tabela. A Grade de Medida aparece abaixo de uma tabela no designer de modelos em Exibição de Dados. Para ocultar ou exibir a grade de medida de uma tabela, clique no menu **Tabela** e em **Mostrar Grade de Medida**.  
  
Você pode criar uma medida clicando em uma célula vazia na grade de medida e digitando uma fórmula DAX na barra de fórmulas. Quando você clicar em ENTER para concluir a fórmula, a medida será exibida na célula. Você também pode criar medidas por meio de uma função de agregação padrão clicando em uma coluna e clicando no botão AutoSoma (**∑**) na barra de ferramentas. As medidas criadas com o recurso AutoSoma serão exibidas diretamente na célula da grade de medida abaixo da coluna, mas podem ser movidas se necessário.  
  
Nesta lição, você criará medidas inserindo uma fórmula DAX na barra de fórmulas e usando o recurso AutoSoma.  
  
Tempo estimado para concluir esta lição: **30 minutos**  
  
## Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 6: Criar colunas calculadas](../analysis-services/lesson-6-create-calculated-columns.md).  
  
## Criar medidas  
  
#### Para criar a medida Trimestre Atual de Dias até Hoje na tabela Data  
  
1.  No designer de modelos, clique na tabela **Data** .  
  
2.  Se uma grade de medida vazia ainda não aparecer abaixo da tabela, clique no menu **Tabela** e, em seguida, clique em **Mostrar Grade de Medida**.  
  
3.  Na grade de medida, clique na célula vazia superior esquerda.  
  
4.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir:  
  
    **=COUNTROWS( DATESQTD( 'Date'[Date]))**  
  
    Ao concluir a criação da fórmula, pressione ENTER.  
  
    Observe que, agora, a célula superior esquerda contém um nome de medida, **Medida 1**, seguido do resultado, **92**. O nome da medida também precede a fórmula na barra de fórmulas.  
  
5.  Para renomear a medida, na barra de fórmulas, realce o nome **Medida 1**, digite **Dias - Trimestre Atual até Hoje**e pressione a ENTER.  
  
    > [!TIP]  
    > Ao digitar uma fórmula na barra de fórmulas, primeiro digite o nome da medida seguido por dois-pontos (:) e pela fórmula. Com esse método, você não precisa renomear a medida.  
  
#### Para criar a medida Dias do Trimestre Atual na tabela Data  
  
1.  Com a tabela **Data** ainda ativa no designer de modelos, na grade de medida, clique na célula vazia abaixo da medida que você acabou de criar.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    **Dias do Trimestre Atual:=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))**  
  
    Observe nesta fórmula que você inclui primeiro o nome da medida seguido por dois-pontos (:).  
  
    Ao concluir a criação da fórmula, pressione ENTER.  
  
Ao criar uma taxa de comparação entre um período incompleto e o período anterior, a fórmula deve levar em conta a proporção do período decorrido e compará-la à mesma proporção do período anterior. Nesse caso, [Dias – Trimestre Atual até Hoje]/[Dias do Trimestre Atual] fornece a proporção decorrida no período atual.  
  
#### Para criar a medida Pedido de Vendas de Contagem Distinta pela Internet na tabela Internet Sales  
  
1.  No designer de modelos, clique na tabela **Vendas pela Internet** (guia).  
  
    Se a grade de medida ainda não for exibida, clique com o botão direito do mouse na tabela **Internet Sales** (guia) e clique em **Mostrar Grade de Medida**.  
  
2.  Clique no título de coluna **Número do Pedido de Vendas** .  
  
3.  Na barra de ferramentas, clique na seta para baixo ao lado do botão AutoSoma (**∑**) e selecione **DistinctCount**.  
  
    O recurso AutoSoma cria automaticamente uma medida para a coluna selecionada por meio da fórmula de agregação padrão DistinctCount.  
  
    Observe que, agora, a célula superior abaixo da coluna na grade de medida contém um nome de medida, **Número do Pedido de Venda de Contagem Distinta**. As medidas criadas por meio do recurso AutoSoma são colocadas automaticamente na célula superior, abaixo da coluna associada.  
  
4.  Na grade de medida, clique na nova medida e, na janela **Propriedades** , em **Nome da Medida**, renomeie a medida para **Pedido de Vendas de Contagem Distinta pela Internet**.  
  
#### Para criar medidas adicionais na tabela Internet Sales  
  
1.  Usando o recurso AutoSoma, crie e nomeie as seguintes medidas:  
  
    |Nome da Medida|Coluna|AutoSoma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |Contagem das Linhas de Pedido pela Internet|Número da Linha do Pedido de Vendas|Count|=COUNT([Número da Linha do Pedido de Vendas])|  
    |Unidades Totais da Internet|Quantidade do Pedido|Sum|=SUM([Quantidade do Pedido])|  
    |Valor do Desconto Total pela Internet|Valor do desconto|Sum|=SUM([Valor do Desconto])|  
    |Custo Total do Produto da Internet|Custo Total do Produto|Sum|=SUM([Custo Total do Produto])|  
    |Vendas Totais pela Internet|Valor das Vendas|Sum|=SUM([Valor das Vendas])|  
    |Margem Total da Internet|Margem|Sum|=SUM([Margem])|  
    |Valor Total dos Imp. da Internet|Valor dos Imp.|Sum|=SUM([Valor dos Imp.])|  
    |Frete Total da Internet|Frete|Sum|=SUM([Frete])|  
  
2.  Clicando em uma célula vazia na grade de medida e usando a fórmula DAX, crie e nomeie as seguintes medidas:  
  
    > [!IMPORTANT]  
    > Você deve criar as seguintes medidas na ordem; as fórmulas nas medidas subsequentes se referem às medidas anteriores.  
  
    |Nome da Medida|Fórmula|  
    |----------------|-----------|  
    |Margem do Trimestre Anterior da Internet|=CALCULATE([Margem Total da Internet],PREVIOUSQUARTER('Date'[Date]))|  
    |Margem do Trimestre Atual da Internet|=TOTALQTD([Margem Total da Internet],'Date'[Date])|  
    |Proporção da Margem do Trimestre Anterior da Internet até QTD|=[Margem do Trimestre Anterior da Internet]*([Dias - Trimestre Atual até Hoje]/[Dias do Trimestre Anterior])|  
    |Vendas do Trimestre Anterior da Internet|=CALCULATE([Vendas Totais pela Internet],PREVIOUSQUARTER('Date'[Date]))|  
    |Vendas do Trimestre Atual da Internet|=TOTALQTD([Vendas Totais pela Internet],'Date'[Date])|  
    |Proporção de Vendas do Trimestre Anterior da Internet até QTD|=[Vendas do Trimestre Anterior da Internet]*([Dias - Trimestre Atual até Hoje]/[Dias do Trimestre Atual])|  
  
As medidas criadas para a tabela Vendas pela Internet podem ser usadas para analisar dados financeiros essenciais, como vendas, custos e margem de lucro para itens definidos pelo filtro selecionado pelo usuário.  
  
## Próxima etapa  
Para continuar este tutorial, vá para a próxima lição: [Lição 8: Criar indicadores chave de desempenho](../analysis-services/lesson-8-create-key-performance-indicators.md).  
  
  
  
