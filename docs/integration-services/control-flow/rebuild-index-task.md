---
title: Tarefa recompilar índice | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rebuildindextask.f1
helpviewer_keywords:
- rebuilding indexes
- indexes [Integration Services]
- Rebuild Index task
ms.assetid: 021884dd-e72d-47b2-99e8-b741410509c3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: af10da0db8cff17e6cf06c155a85713a3fae50eb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294016"
---
# <a name="rebuild-index-task"></a>Tarefa Recriar Índice

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa Recriar Índice recria índices em tabelas e exibições de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre o gerenciamento de índices, consulte [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Utilizando a tarefa Recriar Índice, um pacote pode reconstruir índices em um único banco de dados ou em vários bancos de dados. Se a tarefa recriar somente os índices em um único banco de dados, você poderá escolher as exibições e as tabelas cujos índices a tarefa recriará.  
  
 Essa tarefa encapsula uma instrução ALTER INDEX REBUILD com as seguintes opções de recriação de índice:  
  
-   Especificar uma porcentagem de FILLFACTOR ou utilizar a quantidade original de FILLFACTOR.  
  
-   Definir SORT_IN_TEMPDB = ON para armazenar o resultado de classificação intermediário utilizado para recriar o índice em tempdb. Quando o resultado de classificação intermediário for definido como OFF, ele será armazenado no mesmo banco de dados do índice.  
  
-   Definir PAD_INDEX = ON para alocar o espaço livre especificado pelo FILLFACTOR nas páginas de nível intermediário do índice.  
  
-   Definir IGNORE_DUP_KEY = ON para permitir uma operação de inserção de várias linhas que inclui registros que violam restrições exclusivas para inserir os registros que não as violam.  
  
-   Definir ONLINE = ON para não manter os bloqueios das tabelas, de forma que se possa prosseguir com consultas ou atualizações na tabela subjacente, durante a reindexação.  
  
    > [!NOTE]  
    >  As operações de índice online não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   Especifique um valor de MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo.  
  
-   Especifique WAIT_AT_LOW_PRIORITY, MAX_DURATION e ABORT_AFTER_WAIT para controlar quanto tempo a operação de índice aguardará bloqueios de baixa prioridade.  
  
 Para obter mais informações sobre a instrução ALTER INDEX e as opções de recriação de índice, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
> [!IMPORTANT]  
>  O tempo que a tarefa leva para criar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] por ela executada é proporcional ao número de índices recriados pela tarefa. Se a tarefa for configurada para recompilar índices em todas as tabelas e exibições em um banco de dados com um grande número de índices ou em vários bancos de dados, ela poderá levar um tempo considerável para gerar a instrução Transact-SQL.  
  
## <a name="configuration-of-the-rebuild-index-task"></a>Configuração da tarefa Recompilar Índice  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
 [Tarefa Recriar Índice &#40;Plano de manutenção&#41;](../../relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Definir as propriedades de uma tarefa ou um contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
