---
title: Pré-requisitos para registro em log mínimo em importação em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- minimal logging [SQL Server]
- logged bulk copy [SQL Server]
- logs [SQL Server], minimal logging
- minimally logged operations [SQL Server]
- bulk importing [SQL Server], minimal logging
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 577f7170bce26241803f757e0eb4b1215b094d54
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-minimal-logging-in-bulk-import"></a>Prerequisites for Minimal Logging in Bulk Import
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Para um banco de dados no modelo de recuperação completa, todas as operações de inserção de linha executadas pela importação em massa são registradas completamente no log de transações. Importações de grandes volumes de dados poderão fazer o log de transações ficar cheio rapidamente se o modelo de recuperação completa for usado. Por outro lado, no modelo de recuperação simples ou no modelo de recuperação bulk-logged, o log mínimo de operações de importação em massa reduz a possibilidade de uma operação de importação em massa preencher o espaço do log. O log mínimo também é mais eficiente que o log completo.  
  
> [!NOTE]  
>  O modelo de recuperação bulk-logged foi projetado para substituir temporariamente o modelo de recuperação completa durante operações em massa de grande porte.  
  
## <a name="table-requirements-for-minimally-logging-bulk-import-operations"></a>Requisitos de tabela para operações de importação em massa com log mínimo  
 O log mínimo requer que a tabela de destino atenda às seguintes condições:  
  
-   A tabela não está sendo reproduzida.  
  
-   O bloqueio da tabela é especificado (usando TABLOCK). Para a tabela com um índice columnstore clusterizado, o TABLOCK não é necessário para o log mínimo.  Além disso, somente o carregamento de dados nos grupos de linhas compactados são minimamente registrados, requerendo um tamanho de lote de 102.400 ou superior.  
  
    > [!NOTE]  
    >  Embora as inserções de dados não sejam registradas no log de transações durante uma operação da importação com log em massa, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] ainda faz o log de alocações de extensão cada vez que uma nova extensão é alocada à tabela.  
  
-   A tabela não é do tipo com otimização de memória.  
  
 A possibilidade de ocorrência de log mínimo em uma tabela também poderá depender se a tabela estiver indexada e, nesse caso, se a tabela estiver vazia:  
  
-   Se a tabela não tiver nenhum índice, as páginas de dados terão log mínimo.  
  
-   Se a tabela não tiver nenhum índice clusterizado, mas tiver um ou mais índices não clusterizados, as páginas de dados sempre terão log mínimo. No entanto, a forma como as páginas de índice são registradas depende da tabela:  
  
    -   Se a tabela estiver vazia, a páginas de índice terão log mínimo.  
  
    -   Se a tabela não estiver vazia, as páginas de índice terão log completo.  
  
        > [!NOTE]  
        >  Se você iniciar com uma tabela vazia e importar os dados em massa em vários lotes, para o primeiro lote as páginas de índice e as páginas de dados terão log mínimo, mas começando com o segundo lote, só as páginas de dados terão log mínimo.  
  
-   Se a tabela tiver um índice clusterizado e estiver vazia, ambas as páginas de dados e de índice terão log mínimo. Por outro lado, se uma tabela tiver um índice clusterizado baseado na árvore b e não estiver vazia, as páginas de dados e as páginas de índice terão um log completo, independentemente do modelo de recuperação. Para as tabelas com índice columnstore clusterizado, o carregamento de dados no grupo de linhas compactado sempre terá um log mínimo, independentemente da tabela estar vazia ou não quando o tamanho do lote for > = 102.400.  
  
    > [!NOTE]  
    >  Se você iniciar com uma tabela rowstore vazia e importar em massa os dados em lotes, as páginas de índice e de dados serão registradas minimamente para o primeiro lote, mas do segundo lote em diante, somente as páginas de dados serão registradas em massa.  
  
> [!NOTE]  
>  Quando a replicação transacional está habilitada, as operações BULK INSERT são completamente registradas mesmo no modelo de recuperação bulk-logged.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
  
## <a name="see-also"></a>Consulte Também  
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
  
  
