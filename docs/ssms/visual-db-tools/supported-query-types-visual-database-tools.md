---
title: Tipos de consulta com suporte (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Delete query
- queries [SQL Server], types
- Update query
- Query Designer [SQL Server], query types
- Criteria pane
- Insert Values query
- Select query
- Make Table query
- Insert Results query
- Diagram pane [Visual Database Tools]
- View Designer, query types
ms.assetid: 72b9116c-c128-4078-a78d-257a2955a3f6
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1afdcb105f3b9045c4064928ba46407fb43f3ed0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="supported-query-types-visual-database-tools"></a>Tipos de consulta permitidos (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Você pode criar os seguintes tipos de consultas nos painéis de Diagrama e Critérios (os painéis gráficos) do [Designer de Exibição e Consulta](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md):  
  
-   **Consulta de seleção** Recupera dados de uma ou mais tabelas ou exibições. Esse tipo de consulta cria uma instrução SQL SELECT.  
  
-   **Inserir Resultados** Cria linhas novas copiando linhas existentes de uma tabela para outra, ou na mesma tabela como linhas novas. Esse tipo de consulta cria uma instrução SQL INSERT INTO...SELECT.  
  
-   **Inserir Valores** Cria uma linha nova e insere valores em colunas especificadas. Esse tipo de consulta cria uma instrução SQL INSERT INTO...VALUES.  
  
-   **Consulta de atualização** Altera os valores de colunas individuais em uma ou mais linhas existentes em uma tabela. Esse tipo de consulta cria uma instrução SQL UPDATE…SET.  
  
-   **Consulta de exclusão** Remove uma ou mais linhas de uma tabela. Esse tipo de consulta cria uma instrução SQL DELETE.  
  
    > [!NOTE]  
    > Uma consulta DELETE remove linhas inteiras de tabelas. Se você quer excluir valores de colunas de dados individuais, use uma consulta UPDATE.  
  
-   **Consulta Criar Tabela** Cria uma tabela nova e cria linhas na mesma copiando os resultados de uma consulta. Esse tipo de consulta cria uma instrução SQL SELECT....INTO  
  
Além das consultas, que você pode criar usando os painéis gráficos, pode inserir qualquer instrução SQL no painel de SQL, tais como consultas Union.  
  
Quando você criar consultas que usam instruções SQL que não podem ser representadas nos painéis gráficos, o Designer de Consulta e Exibição escurece esses painéis para indicar que eles não refletem a consulta que você está criando. Porém, os painéis escurecidos ainda estão ativos e, em muitas casos, você pode fazer alterações na consulta nesses painéis. Se as alterações que você fizer resultarem em uma consulta que pode ser representada nos painéis gráficos, esses painéis não são mais escurecidos.  
  
## <a name="see-also"></a>Consulte também  
[Tópicos de instruções de como criar consultas e exibições (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Tipos de consultas (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
