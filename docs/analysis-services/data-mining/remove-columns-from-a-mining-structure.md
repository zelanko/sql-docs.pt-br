---
title: "Remover colunas de uma estrutura de minera&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "estruturas de mineração [Analysis Services], colunas"
  - "removendo colunas"
  - "excluindo colunas"
  - "colunas [mineração de dados], colunas de estrutura de mineração"
ms.assetid: 41073ffe-9351-416b-9f0c-62634bc213f9
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 27
---
# Remover colunas de uma estrutura de minera&#231;&#227;o
  Você pode usar o Designer de Mineração de Dados para remover colunas de uma estrutura de mineração após a criação da estrutura. Alguns motivos para remover uma coluna da estrutura de mineração:  
  
-   A estrutura de mineração contém várias cópias de uma coluna e você deseja evitar o uso de dados duplicados em um modelo.  
  
-   Os dados devem ser protegidos, mas o detalhamento foi habilitado.  
  
-   Os dados não são usados na modelagem e não devem ser processados.  
  
 A exclusão de uma coluna da estrutura de mineração não altera a coluna na exibição da fonte de dados nem nos dados externos; apenas os metadados são excluídos. Entretanto, quando você altera as colunas usadas em uma estrutura de mineração, precisa reprocessar a estrutura e quaisquer modelos com base nela.  
  
### Para remover colunas de uma estrutura de mineração  
  
1.  Selecione a guia **Estrutura de Mineração** no Designer de Mineração de Dados.  
  
2.  Expanda a árvore da estrutura de mineração para que mostre todas as colunas.  
  
3.  Clique com o botão direito do mouse na coluna que você quer excluir e selecione **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objetos** , clique em **OK**.  
  
## Consulte também  
 [Tarefas e instruções da estrutura de mineração](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  