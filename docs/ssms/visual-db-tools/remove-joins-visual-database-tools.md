---
title: Remover junções (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 88b5bc8e83484129cb6d503b2bb1feb226c8cc34
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="remove-joins-visual-database-tools"></a>Remover Junções (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Se você não quer unir tabelas por uma junção interna ou uma junção externa, você pode remover a junção entre elas. Por exemplo, você pode remover uma junção que o [Designer de Consulta e Exibição](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) criou automaticamente entre duas tabelas.  
  
> [!NOTE]  
> Remover uma junção de uma consulta não altera a relação subjacente no banco de dados.  
  
Se duas tabelas unidas fazem parte de sua consulta e você remove todas as condições de junção entre elas, a consulta resultante se torna o produto das duas tabelas — ou seja, se torna uma CROSS JOIN.  
  
### <a name="to-remove-a-join"></a>Para remover uma junção  
  
-   No [painel Diagrama](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md), selecione a linha de junção para a junção a ser removida e pressione a tecla DELETE. Você pode selecionar e excluir várias linhas de junção de uma vez.  
  
O Designer de Consulta e Exibição remove a linha de junção e altera a instrução no [painel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
[Unir tabelas automaticamente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)  
[Unir tabelas manualmente &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)  
[Consultar com junções &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
