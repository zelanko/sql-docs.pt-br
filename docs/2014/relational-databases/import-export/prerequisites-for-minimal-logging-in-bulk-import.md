---
title: Pré-requisitos para registro em log mínimo em importação em massa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- minimal logging [SQL Server]
- logged bulk copy [SQL Server]
- logs [SQL Server], minimal logging
- minimally logged operations [SQL Server]
- bulk importing [SQL Server], minimal logging
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 858789f7954d21c59db3d7221f23d1f429e1c5dd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072216"
---
# <a name="prerequisites-for-minimal-logging-in-bulk-import"></a>Prerequisites for Minimal Logging in Bulk Import
  Para um banco de dados no modelo de recuperação completa, todas as operações de inserção de linha executadas pela importação em massa são registradas completamente no log de transações. Importações de grandes volumes de dados poderão fazer o log de transações ficar cheio rapidamente se o modelo de recuperação completa for usado. Por outro lado, no modelo de recuperação simples ou no modelo de recuperação bulk-logged, o log mínimo de operações de importação em massa reduz a possibilidade de uma operação de importação em massa preencher o espaço do log. O log mínimo também é mais eficiente que o log completo.  
  
> [!NOTE]  
>  O modelo de recuperação bulk-logged foi projetado para substituir temporariamente o modelo de recuperação completa durante operações em massa de grande porte.  
  
## <a name="table-requirements-for-minimally-logging-bulk-import-operations"></a>Requisitos de tabela para operações de importação em massa com log mínimo  
 O log mínimo requer que a tabela de destino atenda às seguintes condições:  
  
-   A tabela não está sendo reproduzida.  
  
-   O bloqueio da tabela é especificado (usando TABLOCK).  
  
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
  
-   Se a tabela tiver um índice clusterizado e estiver vazia, ambas as páginas de dados e de índice terão log mínimo. Por outro lado, se uma tabela tiver um índice clusterizado e não estiver vazia, as páginas de dados e as páginas de índice terão log completo seja qual for o modelo de recuperação.  
  
    > [!NOTE]  
    >  Se você iniciar com uma tabela vazia e importar os dados em massa em vários lotes, as páginas de índice e as páginas de dados terão log mínimo para o primeiro lote, mas a partir do segundo lote, apenas as páginas de dados terão bulk-logged.  
  
> [!NOTE]  
>  Quando a replicação transacional está habilitada, as operações BULK INSERT são completamente registradas mesmo no modelo de recuperação bulk-logged.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  

  
## <a name="see-also"></a>Consulte também  
 [Modelos de recuperação &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
  
