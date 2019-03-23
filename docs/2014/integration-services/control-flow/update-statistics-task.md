---
title: Tarefa Atualizar Estatísticas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.updatestatisticstask.f1
helpviewer_keywords:
- updating statistics
- Update Statistics task [Integration Services]
ms.assetid: 0247483b-f092-4511-8fa8-3610108bd1bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: be80af34bc2dc8b5d069406bc13a8f8f9b25c42c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379994"
---
# <a name="update-statistics-task"></a>Tarefa Atualizar Estatísticas
  A tarefa Atualizar Estatísticas atualiza informações sobre a distribuição de valores de chaves para um ou mais grupos de estatísticas (coleções) na tabela ou na exibição indexada especificada. Para obter mais informações, consulte [Statistics](../../relational-databases/statistics/statistics.md).  
  
 Utilizando-se a tarefa Atualizar Estatísticas, um pacote pode atualizar as estatísticas de um único banco de dados ou de vários bancos de dados. Se a tarefa atualizar só as estatísticas em um único banco de dados, você poderá escolher as exibições e as tabelas cujas estatísticas a tarefa atualizará. É possível configurar a atualização para atualizar todas as estatísticas, apenas as estatísticas de coluna, ou apenas as estatísticas de índice.  
  
 Esta tarefa encapsula uma instrução UPDATE STATISTICS, inclusive os seguintes argumentos e cláusulas:  
  
-   Os argumentos *table_name* ou *view_name* .  
  
-   Se a atualização se aplicar a todas as estatísticas, a cláusula WITH ALL estará implícita.  
  
-   Se a atualização se aplicar apenas a colunas, a cláusula WITH COLUMN será incluída.  
  
-   Se a atualização se aplicar apenas a índices, a cláusula WITH COLUMN será incluída.  
  
 Se a tarefa Atualizar Estatísticas atualizar estatísticas em vários bancos de dados, a tarefa executará várias instruções UPDATE STATISTICS, uma para cada tabela ou exibição. Todas as instâncias de UPDATE STATISTICS usam a mesma cláusula, mas têm valores diferentes para *table_name* ou *view_name*. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql) e [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql).  
  
> [!IMPORTANT]  
>  O tempo que a tarefa necessita para criar a instrução Transact-SQL que ela executa é proporcional ao número de estatísticas que a tarefa atualiza. Se a tarefa for configurada para atualizar estatísticas em todas as tabelas e exibições em um banco de dados com um grande número de índices ou em vários bancos de dados, ela pode levar um tempo considerável para gerar a instrução Transact-SQL.  
  
## <a name="configuration-of-the-update-statistics-task"></a>Configuração da tarefa Atualizar Estatísticas  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Atualização de Estatísticas &#40;Plano de manutenção&#41;](../../relational-databases/maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](integration-services-tasks.md)   
 [Fluxo de Controle](control-flow.md)  
  
  
