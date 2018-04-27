---
title: Classificar com ORDER BY (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 804356d4b1099350451a13465eb663e078d4b58a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="sort-with-order-by-visual-database-tools"></a>Classificar com ORDER BY (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode classificar resultados de consulta por uma ou mais das colunas nas linhas retornadas usando uma cláusula ORDER BY. Você pode definir uma cláusula ORDER BY escolhendo opções no painel Detalhes de Critérios.  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>Para classificar uma consulta usando uma cláusula ORDER BY  
  
1.  Abra uma consulta ou crie uma nova.  
  
2.  No [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), clique na coluna **Tipo de Classificação** da linha que corresponde à coluna a ser usada para classificar seus resultados de consulta.  
  
3.  Escolha *Crescente* ou *Decrescente* na lista suspensa.  
  
> [!NOTE]  
> Desmarcar a entrada **Tipo de Classificação** de uma coluna remove essa coluna da cláusula ORDER BY.  
  
Note que conforme você trabalha no painel de critérios, a cláusula UNION de sua consulta é alterada para corresponder a suas ações mais recentes.  
  
> [!NOTE]  
> Ao classificar resultados em mais de uma coluna, especifique a ordem de pesquisa das colunas em relação umas às outras usando a coluna **Ordem de Classificação** . Para obter mais informações, consulte **Como classificar várias colunas em consultas**.  
  
## <a name="see-also"></a>Consulte Também  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
