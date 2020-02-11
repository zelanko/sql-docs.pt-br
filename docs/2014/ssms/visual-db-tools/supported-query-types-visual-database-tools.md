---
title: Tipos de consulta com suporte (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 752467d058a6618ccfa44d7e2f75ac33b632878e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204653"
---
# <a name="supported-query-types-visual-database-tools"></a>Tipos de consulta permitidos (Visual Database Tools)
  Você pode criar os seguintes tipos de consultas nos painéis diagrama e critérios (os painéis gráficos) do [Designer de consulta e exibição](visual-database-tools.md):  
  
-   **Selecionar consulta** Recupera dados de uma ou mais tabelas ou exibições. Esse tipo de consulta cria uma instrução SQL SELECT.  
  
-   **Inserir resultados** Cria novas linhas copiando as linhas existentes de uma tabela em outra, ou na mesma tabela como novas linhas. Esse tipo de consulta cria uma instrução SQL INSERT INTO...SELECT.  
  
-   **Inserir valores** Cria uma nova linha e insere valores em colunas especificadas. Esse tipo de consulta cria uma instrução SQL INSERT INTO...VALUES.  
  
-   **Consulta de atualização** Altera os valores de colunas individuais em uma ou mais linhas existentes em uma tabela. Esse tipo de consulta cria uma instrução SQL UPDATE…SET.  
  
-   **Excluir consulta** Remove uma ou mais linhas de uma tabela. Esse tipo de consulta cria uma instrução SQL DELETE.  
  
    > [!NOTE]  
    >  Uma consulta DELETE remove linhas inteiras de tabelas. Se você quer excluir valores de colunas de dados individuais, use uma consulta UPDATE.  
  
-   **Consulta criar tabela** Cria uma nova tabela e cria linhas nela copiando os resultados de uma consulta nela. Esse tipo de consulta cria uma instrução SQL SELECT....INTO  
  
 Além das consultas, que você pode criar usando os painéis gráficos, pode inserir qualquer instrução SQL no painel de SQL, tais como consultas Union.  
  
 Quando você criar consultas que usam instruções SQL que não podem ser representadas nos painéis gráficos, o Designer de Consulta e Exibição escurece esses painéis para indicar que eles não refletem a consulta que você está criando. Porém, os painéis escurecidos ainda estão ativos e, em muitas casos, você pode fazer alterações na consulta nesses painéis. Se as alterações que você fizer resultarem em uma consulta que pode ser representada nos painéis gráficos, esses painéis não são mais escurecidos.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre como criar consultas e exibições &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Tipos de consultas &#40;Visual Database Tools&#41;](types-of-queries-visual-database-tools.md)  
  
  
