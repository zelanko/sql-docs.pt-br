---
title: Remover junções (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac2b8ca912f02aecc5e1b3e76d04d84b501db89b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63253492"
---
# <a name="remove-joins-visual-database-tools"></a>Remover Junções (Visual Database Tools)
  Se você não quer unir tabelas por uma junção interna ou uma junção externa, você pode remover a junção entre elas. Por exemplo, você pode remover uma junção que o [Designer de Consulta e Exibição](visual-database-tools.md) criou automaticamente entre duas tabelas.  
  
> [!NOTE]  
>  Remover uma junção de uma consulta não altera a relação subjacente no banco de dados.  
  
 Se duas tabelas unidas fazem parte de sua consulta e você remove todas as condições de junção entre elas, a consulta resultante se torna o produto das duas tabelas – ou seja, se torna uma CROSS JOIN.  
  
### <a name="to-remove-a-join"></a>Para remover uma junção  
  
-   No [painel Diagrama](diagram-pane-visual-database-tools.md), selecione a linha de junção para a junção a ser removida e pressione a tecla DELETE. Você pode selecionar e excluir várias linhas de junção de uma vez.  
  
 O Designer de Consulta e Exibição remove a linha de junção e altera a instrução no [painel SQL](sql-pane-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Unir tabelas automaticamente &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md)   
 [Unir tabelas manualmente &#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md)   
 [Consultar com junções &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
