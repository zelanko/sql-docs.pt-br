---
title: "Excluir uma coluna de um modelo de minera&#231;&#227;o | Microsoft Docs"
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
  - "excluindo colunas do modelo de mineração"
  - "modelos de mineração [Analysis Services], colunas"
  - "colunas [mineração de dados], excluindo"
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 29
---
# Excluir uma coluna de um modelo de minera&#231;&#227;o
  Ao criar um novo modelo de mineração, talvez você não queira usar todas as colunas existentes na estrutura de mineração em que o modelo é baseado. Por exemplo, talvez você tenha adicionado uma coluna de nome de cliente para detalhamento, mas não deseje usá-la para modelagem. Ou você pode decidir criar várias cópias de uma coluna com discretizações diferentes e usar apenas uma das cópias em cada modelo, ignorando as demais. Você também pode adicionar seletivamente colunas de entrada em vários modelos diferentes para ver como a variável adicionada afeta a coluna de saída.  
  
 Você não precisa criar uma nova estrutura de mineração para cada combinação de colunas; basta sinalizar uma coluna como não sendo usado em um modelo específico.  
  
### Para excluir uma coluna de um modelo de mineração  
  
1.  Na guia **Modelos de Mineração** no Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione a célula que corresponde à coluna que deseja excluir no modelo de mineração apropriado.  
  
2.  Selecione **Ignorar** na caixa de listagem suspensa.  
  
## Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  