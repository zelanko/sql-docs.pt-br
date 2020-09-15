---
description: Resumir ou agregar valores usando expressões personalizadas (Visual Database Tools)
title: Resumir ou agregar valores usando expressões personalizadas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- custom expressions to aggregate values [SQL Server]
ms.assetid: 34130ac1-0106-4766-b324-acb0b7bb6f6e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: e71f0ffc06314678becda493f6e45c98060d3a32
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88312542"
---
# <a name="summarize-or-aggregate-values-using-custom-expressions-visual-database-tools"></a>Resumir ou agregar valores usando expressões personalizadas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Além de utilizar funções de agregação para agregar dados, você pode criar expressões personalizadas para produzir valores de agregação. É possível utilizar expressões personalizadas ao invés de funções de agregação em qualquer lugar de uma consulta de agregação.  
  
Por exemplo, na tabela `titles` você poderia querer criar uma consulta que exibisse não só o preço médio, mas qual seria o preço médio se houvesse um desconto.  
  
Você não pode incluir uma expressão baseada em cálculos que envolvem apenas linhas individuais na tabela; a expressão deve se basear em um valor de agregação, pois somente os valores de agregação estão disponíveis no momento em que a expressão é calculada.  
  
### <a name="to-specify-a-custom-expression-for-a-summary-value"></a>Para especificar uma expressão personalizada para um valor resumido  
  
1.  Especifique os grupos para a sua consulta. Para obter detalhes, veja [Agrupar linhas em resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  
  
2.  Vá para uma linha em branco do painel Critérios e digite a expressão na coluna **Colunas**.  
  
    O [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) atribui automaticamente um alias de coluna à expressão para criar um título da coluna útil na saída da consulta. Para obter mais detalhes, veja [Criar aliases de coluna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
3.  Na coluna **Agrupar por** da expressão, selecione **Expressão**.  
  
4.  Executar a consulta.  
  
## <a name="see-also"></a>Consulte Também  
[Classificar e agrupar resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir resultados da consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
