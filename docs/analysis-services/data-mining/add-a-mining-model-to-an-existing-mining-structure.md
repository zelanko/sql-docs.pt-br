---
title: "Adicionar um modelo de minera&#231;&#227;o a uma estrutura de minera&#231;&#227;o existente | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modelos de mineração [Analysis Services], adicionando"
  - "estruturas de mineração [Analysis Services], modelos de mineração"
  - "adicionando modelos de mineração"
ms.assetid: fcf72300-0674-4e73-a826-9b8eeffefbb5
caps.latest.revision: 24
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 24
---
# Adicionar um modelo de minera&#231;&#227;o a uma estrutura de minera&#231;&#227;o existente
  É possível adicionar mais modelos de mineração a uma estrutura de mineração, após adicionar o modelo inicial. Cada modelo deve conter colunas que existam na estrutura, mas você pode definir de forma diferente o uso das colunas para cada modelo de mineração. Para obter mais informações sobre como definir colunas de modelos de mineração, consulte [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md).  
  
### Para adicionar um modelo de mineração à estrutura  
  
1.  No item de menu **Modelo de Mineração** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione **Novo Modelo de Mineração**.  
  
     A caixa de diálogo **Novo Modelo de Mineração** é exibida.  
  
2.  Em **Nome do modelo**, digite um nome para o modelo de mineração novo.  
  
3.  Em **Nome do algoritmo**, selecione o algoritmo por meio do qual o modelo de mineração será construído.  
  
4.  Clique em **OK**.  
  
 Um modelo de mineração novo é exibido na guia **Modelos de Mineração**. O modelo usa as colunas padrão que existem na estrutura. Para obter mais informações sobre como modificar as colunas, consulte [Alterar as propriedades de um modelo de mineração](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md).  
  
## Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  