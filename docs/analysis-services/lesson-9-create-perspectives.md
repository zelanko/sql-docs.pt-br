---
title: "Li&#231;&#227;o 9: Criar perspectivas | Microsoft Docs"
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
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Li&#231;&#227;o 9: Criar perspectivas
Nesta lição, você criará uma perspectiva de Vendas pela Internet. Uma perspectiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. Quando um usuário se conecta a um modelo usando uma perspectiva, ele vê apenas os objetos de modelo (tabelas, colunas, medidas e KPIs) como campos definidos nessa perspectiva.  
  
A perspectiva Vendas pela Internet que você criou nesta lição excluirá o objeto de tabela Cliente. Quando você cria uma perspectiva que exclui determinados objetos da exibição, esse objeto ainda existe no modelo; porém, não está visível em uma lista de campo de cliente de relatório. Colunas calculadas e medidas incluídas ou não em uma perspectiva ainda podem ser calculadas de dados de objeto que são excluídos.  
  
A finalidade desta lição é descrever como criar perspectivas e se familiarizar com as ferramentas de criação de modelo de tabela. Se você expandir este modelo posteriormente para incluir tabelas adicionais, poderá criar perspectivas adicionais para definir diferentes pontos de vista do modelo; por exemplo, Inventário e Força de Vendas.  
  
Para saber mais, consulte [Perspectivas &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **5 minutos**  
  
## Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deve ter concluído a lição anterior: [Lição 8: Criar Indicadores Chave de Desempenho](../analysis-services/lesson-8-create-key-performance-indicators.md).  
  
## Criar perspectivas  
  
#### Para criar uma perspectiva Vendas pela Internet  
  
1.  No designer de modelos, clique no menu **Modelo**, em **Perspectivas** e em **Criar e Gerenciar**.  
  
2.  Na caixa de diálogo **Perspectivas**, clique em **Nova Perspectiva**.  
  
3.  Para renomear a perspectiva, clique duas vezes no título de coluna **Nova Perspectiva 1** e digite **Vendas pela Internet**.  
  
4.  Em **Campos**, selecione as tabelas **Date**, **Geography**, **Product**, **Product Category**, **Product Subcategory** e **Internet Sales**.  
  
    Observe que você excluiu a tabela Cliente e todas as suas colunas desta perspectiva. Posteriormente, na Lição 12, você usará o recurso Analisar no Excel para testar esta perspectiva. A Lista de Campos da Tabela Dinâmica do Excel incluirá cada tabela exceto a tabela Cliente.  
  
5.  Verifique as seleções, garantindo que a tabela **Customer** não está marcada e clique em **OK**  
  
## Próximas etapas  
Para continuar este tutorial, vá para a próxima lição: [Lição 10: Criar hierarquias](../analysis-services/lesson-10-create-hierarchies.md).  
  
  
  
