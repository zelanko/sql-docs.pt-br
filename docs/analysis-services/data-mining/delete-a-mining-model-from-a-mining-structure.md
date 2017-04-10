---
title: "Excluir um modelo de minera&#231;&#227;o de uma estrutura de minera&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "estruturas de mineração [Analysis Services], modelos de mineração"
  - "excluindo modelos de mineração"
  - "removendo modelos de mineração"
  - "modelos de mineração [Analysis Services], excluindo"
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 29
---
# Excluir um modelo de minera&#231;&#227;o de uma estrutura de minera&#231;&#227;o
  Você pode excluir modelos de mineração usando o Designer de Mineração de Dados, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou instruções DMX.  
  
### Exclua um modelo de mineração usando as Ferramentas de Dados do SQL Server  
  
1.  Selecione a guia **Modelos de Mineração** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no modelo a ser excluído e selecione **Excluir**.  
  
     A caixa de diálogo **Excluir Objetos** é aberta.  
  
3.  Clique em **OK**.  
  
### Exclua um modelo de mineração usando o SQL Server Management Studio  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém o modelo.  
  
2.  Expanda **Estruturas de Mineração**e, depois, **Modelos de Mineração**.  
  
3.  Clique com o botão direito do mouse no modelo a ser excluído e selecione **Excluir**.  
  
     A exclusão do modelo não leva à exclusão dos dados de treinamento, mas apenas dos metadados e de quaisquer padrões criados durante o treinamento do modelo.  
  
### Excluir um modelo de mineração usando DMX  
  
-   [DROP MINING MODEL &#40;DMX&#41;](../../dmx/drop-mining-model-dmx.md)  
  
## Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  