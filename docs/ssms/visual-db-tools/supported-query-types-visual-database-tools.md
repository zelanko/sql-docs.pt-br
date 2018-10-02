---
title: Tipos de consulta com suporte (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d784fca62ffd20e624cc2c103e4657e277012867
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635554"
---
# <a name="supported-query-types-visual-database-tools"></a>Tipos de consulta permitidos (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode criar os seguintes tipos de consultas nos painéis de Diagrama e Critérios (os painéis gráficos) do [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md):  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Tópicos de instruções de como criar consultas e exibições (Ferramentas de Banco de Dados Visual)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Tipos de consultas (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
