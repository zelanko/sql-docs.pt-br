---
title: Tarefa Verificar Integridade do Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.checkdatabaseintegritytask.f1
helpviewer_keywords:
- data integrity [Integration Services]
- Check Database Integrity task [Integration Services]
- checking database consistency
- database consistency checks [Integration Services]
- verifying database consistency
- integrity checking [Integration Services]
ms.assetid: 5a82fe99-4503-429f-9337-e6bac7649fe4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a123557bdeb84ed8d36664b6451772b669edbbec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832845"
---
# <a name="check-database-integrity-task"></a>Tarefa Verificar Integridade do Banco de Dados
  A tarefa Verificar Integridade do Banco de Dados verifica a alocação e integridade estrutural de todos os objetos no banco de dados especificado. A tarefa pode verificar um único ou vários bancos de dados, e você também pode optar por verificar os índices de banco de dados.  
  
 A tarefa Verificar Integridade do Banco de Dados encapsula a instrução DBCC CHECKDB. Para obter mais informações, veja [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql).  
  
## <a name="configuration-of-the-check-database-integrity-task"></a>Configuração da tarefa Verificar Integridade do Banco de Dados  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Verificar Integridade do Banco de Dados &#40;Plano de Manutenção&#41;](../../relational-databases/maintenance-plans/check-database-integrity-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
  
