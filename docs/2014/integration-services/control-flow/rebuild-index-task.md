---
title: Tarefa recompilar índice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rebuildindextask.f1
helpviewer_keywords:
- rebuilding indexes
- indexes [Integration Services]
- Rebuild Index task
ms.assetid: 021884dd-e72d-47b2-99e8-b741410509c3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9e89c081c1c543c198a827955ab4865709ead391
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392684"
---
# <a name="rebuild-index-task"></a>Tarefa Recriar Índice
  A tarefa Recriar Índice recria índices em tabelas e exibições de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre o gerenciamento de índices, consulte [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Utilizando a tarefa Recriar Índice, um pacote pode reconstruir índices em um único banco de dados ou em vários bancos de dados. Se a tarefa recriar somente os índices em um único banco de dados, você poderá escolher as exibições e as tabelas cujos índices a tarefa recriará.  
  
 Essa tarefa encapsula uma instrução ALTER INDEX REBUILD com as seguintes opções de recriação de índice:  
  
-   Especificar uma porcentagem de FILLFACTOR ou utilizar a quantidade original de FILLFACTOR.  
  
-   Definir PAD_INDEX = ON para alocar o espaço livre especificado pelo FILLFACTOR nas páginas de nível intermediário do índice.  
  
-   Definir SORT_IN_TEMPDB = ON para armazenar o resultado de classificação intermediário utilizado para recriar o índice em tempdb. Quando o resultado de classificação intermediário for definido como OFF, ele será armazenado no mesmo banco de dados do índice.  
  
-   Definir IGNORE_DUP_KEY = ON para permitir uma operação de inserção de várias linhas que inclui registros que violam restrições exclusivas para inserir os registros que não as violam.  
  
-   Definir ONLINE = ON para não manter os bloqueios das tabelas, de forma que se possa prosseguir com consultas ou atualizações na tabela subjacente, durante a reindexação.  
  
> [!NOTE]  
>  As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Para obter mais informações sobre a instrução ALTER INDEX e as opções de recriação de índice, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
> [!IMPORTANT]  
>  O tempo que a tarefa leva para criar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] por ela executada é proporcional ao número de índices recriados pela tarefa. Se a tarefa for configurada para recompilar índices em todas as tabelas e exibições em um banco de dados com um grande número de índices ou em vários bancos de dados, ela poderá levar um tempo considerável para gerar a instrução Transact-SQL.  
  
## <a name="configuration-of-the-rebuild-index-task"></a>Configuração da tarefa Recompilar Índice  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
 [Tarefa Recriar Índice &#40;Plano de manutenção&#41;](../../relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , consulte [Definir as propriedades de uma tarefa ou um contêiner](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](integration-services-tasks.md)   
 [Fluxo de Controle](control-flow.md)  
  
  
