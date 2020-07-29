---
title: Remover junções
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 5c96529e6b66d61dcee5fff9c6ba69a9d878d578
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008896"
---
# <a name="remove-joins-visual-database-tools"></a>Remover Junções (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Se você não quer unir tabelas por uma junção interna ou uma junção externa, você pode remover a junção entre elas. Por exemplo, você pode remover uma junção que o [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) criou automaticamente entre duas tabelas.  
  
> [!NOTE]  
> Remover uma junção de uma consulta não altera a relação subjacente no banco de dados.  
  
Se duas tabelas unidas fazem parte de sua consulta e você remove todas as condições de junção entre elas, a consulta resultante se torna o produto das duas tabelas – ou seja, se torna uma CROSS JOIN.  
  
### <a name="to-remove-a-join"></a>Para remover uma junção  
  
-   No [painel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md), selecione a linha de junção para a junção a ser removida e pressione a tecla DELETE. Você pode selecionar e excluir várias linhas de junção de uma vez.  
  
O Designer de Consulta e Exibição remove a linha de junção e altera a instrução no [painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
[Unir tabelas automaticamente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)  
[Unir tabelas manualmente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
