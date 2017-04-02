---
title: "Li&#231;&#227;o 6: Criar colunas calculadas | Microsoft Docs"
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
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Li&#231;&#227;o 6: Criar colunas calculadas
Nesta lição, você criará novos dados no modelo adicionando colunas calculadas. Uma coluna calculada se baseia nos dados que já existem no modelo. Para saber mais, consulte [Colunas calculadas &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/calculated-columns-ssas-tabular.md).  
  
Você criará cinco novas colunas calculadas em três tabelas diferentes. As etapas são ligeiramente diferentes para cada tarefa. O objetivo disso é mostrar que há vários modos de criar novas colunas, renomeá-las e colocá-las em vários locais em uma tabela.  
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de realizar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 5: Criar relações](../analysis-services/lesson-5-create-relationships.md).  
  
## Criar colunas calculadas  
  
#### Criar uma coluna calculada Month Calendar na tabela Date  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo**, aponte para **Exibição de Modelo** e clique em **Exibição de Dados**.  
  
    Colunas calculadas só podem ser criadas usando o designer de modelos na exibição de dados.  
  
2.  No designer de modelos, clique na tabela **Data** (guia).  
  
3.  Clique com o botão direito do mouse no cabeçalho de coluna **Calendar Quarter** e clique em **Inserir Coluna**.  
  
    Uma nova coluna nomeada **Calculated Column 1** é inserida à esquerda da coluna **Calendar Quarter**.  
  
4.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir. O recurso Preenchimento Automático ajuda a digitar os nomes totalmente qualificados de colunas e tabelas e lista as funções que estão disponíveis.  
  
    **=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]**  
  
    Ao concluir a criação da fórmula, pressione ENTER.  
  
    Os valores são preenchidos em todas as linhas da coluna calculada. Se você rolar para baixo na tabela, verá que as linhas podem ter valores diferentes para essa coluna baseados nos dados que estão em cada linha.  
  
    > [!NOTE]  
    > Se você receber um erro, verifique se os nomes de coluna na fórmula correspondem aos nomes de coluna alterados na [Lição 3: Renomear colunas](../analysis-services/lesson-3-rename-columns.md).  
  
5.  Renomeie esta coluna como **Month Calendar**.  
  
A coluna calculada Month Calendar fornece um nome classificável para o mês.  
  
#### Criar uma coluna calculada Day of Week na tabela Date  
  
1.  Com a tabela **Date** ainda ativa, clique no menu **Coluna** e em **Adicionar Coluna**.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    **=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]**  
  
    Ao concluir a criação da fórmula, pressione ENTER. A nova coluna será adicionada à extrema direita da tabela.  
  
3.  Renomeie a coluna como **Day of Week**.  
  
4.  Clique no título de coluna e arraste a coluna entre as colunas **Day Name** e **Day of Month**.  
  
    > [!TIP]  
    > A movimentação das colunas na tabela facilita a navegação.  
  
A coluna calculada Day of Week fornece um nome classificável para o dia de semana.  
  
#### Criar uma coluna calculada Product Subcategory Name na tabela Product  
  
1.  No designer de modelos, selecione a tabela **Product**.  
  
2.  Role a tela para a extrema direita da tabela. Observe que a coluna mais à direita é chamada **Adicionar Coluna** (em itálico); clique no título de coluna.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir.  
  
    **=RELATED('Product Subcategory'[Product Subcategory Name])**  
  
    Ao concluir a criação da fórmula, pressione ENTER.  
  
4.  Renomeie a coluna como **Product Subcategory Name**.  
  
A coluna calculada Product Subcategory Name é usada para criar uma hierarquia na tabela Product que inclui dados da coluna Product Subcategory Name na tabela Product Subcategory. As hierarquias não podem ultrapassar mais de uma tabela. Você criará hierarquias posteriormente na lição 7.  
  
#### Criar uma coluna calculada Product Category Name na tabela Product  
  
1.  Com a tabela **Product** ainda ativa, clique no menu **Coluna** e em **Adicionar Coluna**.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    **=RELATED('Product Category'[Product Category Name])**  
  
    Ao concluir a criação da fórmula, pressione ENTER.  
  
3.  Renomeie a coluna como **Product Category Name**.  
  
A coluna calculada Product Category Name é usada para criar uma hierarquia na tabela Product que inclui dados da coluna Product Category Name na tabela Product Category. As hierarquias não podem ultrapassar mais de uma tabela.  
  
#### Criar uma coluna calculada Margin na tabela Internet Sales  
  
1.  No designer de modelos, selecione a tabela **Internet Sales**.  
  
2.  Adicione uma nova coluna.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    **=[Sales Amount]-[Total Product Cost]**  
  
    Ao concluir a criação da fórmula, pressione ENTER.  
  
4.  Renomeie a coluna como **Margin**.  
  
5.  Arraste a coluna entre as colunas **Sales Amount** e **Tax Amt**.  
  
A coluna calculada Margin é usada para analisar margens de lucro para cada linha (produto).  
  
## Próxima etapa  
Para continuar esta lição, vá para a próxima lição: [Lição 7: Criar medidas](../analysis-services/lesson-7-create-measures.md).  
  
  
  
