---
title: Estados de arquivo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restoring file state [SQL Server]
- verifying file states
- current file states
- verifying filegroup states
- file states [SQL Server]
- online file state
- offline file state [SQL Server]
- viewing filegroup states
- viewing file states
- suspect file state
- recovering file state [SQL Server]
- current filegroup state
- recovery pending file state [SQL Server]
- displaying file states
- states [SQL Server], files
- displaying filegroup states
- defunct file state
ms.assetid: b426474d-8954-4df0-b78b-887becfbe8d6
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1888b2ab14fd40edd57438ea98dde15adc4efb80
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="file-states"></a>Estados de arquivo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o estado de um arquivo de banco de dados é mantido independentemente do estado do banco de dados. Um arquivo sempre está em um estado específico, como ONLINE ou OFFLINE. Para exibir o estado atual de um arquivo, use a exibição de catálogo [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) ou [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) . Se o banco de dados estiver offline, o estado dos arquivos poderá ser exibido da exibição de catálogo [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) .  
  
 O estado dos arquivos em um grupo de arquivos determina a disponibilidade de todo o grupo. Para que um grupo de arquivos fique disponível, todos os seus arquivos devem estar online. Para exibir o estado atual de um grupo de arquivos, use a exibição de catálogo [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) . Se um grupo de arquivos estiver off-line e você tentar acessá-lo por uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] , ele falhará com um erro. Quando o otimizador de consulta cria planos de consulta para instruções SELECT, ele evita índices não clusterizados e exibições indexadas que residam em grupos de arquivos off-line, permitindo que essas instruções sejam bem-sucedidas. Porém, se o grupo de arquivos offline contiver o heap ou índice clusterizado da tabela de destino, as instruções SELECT falharão. Além disso, qualquer instrução INSERT, UPDATE ou DELETE que modifique uma tabela contendo um índice em um grupo de arquivos offline falhará.  
  
## <a name="file-state-definitions"></a>Definições de estado de arquivo  
 A tabela a seguir define os estados de arquivo.  
  
|Estado|Definição|  
|-----------|----------------|  
|ONLINE|O arquivo está disponível para todas as operações. Os arquivos no grupo de arquivos primário sempre estão on-line se o próprio banco de dados estiver on-line. Se um arquivo no grupo de arquivos primário não estiver on-line, o banco de dados não estará on-line e os estados dos arquivos secundários serão indefinidos.|  
|OFFLINE|O arquivo não está disponível para acesso e talvez não esteja presente no disco. Os arquivos se tornam off-line por ação explícita do usuário e permanecem off-line até que uma ação adicional do usuário seja executada.<br /><br /> **\*\* Cuidado \*\*** Um arquivo somente deve ser definido como offline quando está corrompido, mas pode ser restaurado. Um arquivo definido como off-line pode somente ser definido como on-line pela restauração do arquivo do backup. Para obter mais informações sobre como restaurar um único arquivo, veja [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).|  
|RESTORING|O arquivo está sendo restaurado. Os arquivos entram no estado de restauração devido a um comando de restauração que afeta todo o arquivo, não apenas uma restauração de página e permanece nesse estado até que a restauração esteja completa e o arquivo recuperado.|  
|RECOVERY_PENDING|A recuperação do arquivo foi adiada. Um arquivo entra nesse estado automaticamente devido a um processo de restauração em etapas no qual o arquivo não é restaurado e recuperado. Uma ação adicional é exigida do usuário para resolver o erro e permitir que o processo de recuperação seja concluído. Para obter mais informações, veja [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).|  
|SUSPECT|A recuperação do arquivo falhou durante um processo de restauração on-line. Se o arquivo estiver no grupo de arquivos primário, o banco de dados também será marcado como suspeito. Caso contrário, o arquivo será suspeito e o banco de dados ainda estará on-line.<br /><br /> O arquivo permanecerá no estado suspeito até que seja tornado disponível por um dos seguintes métodos:<br /><br /> Restauração e recuperação<br /><br /> DBCC CHECKDB com REPAIR_ALLOW_DATA_LOSS|  
|DEFUNCT|O arquivo foi descartado quando não estava on-line. Todos os arquivos em um grupo de arquivos tornam-se extintos quando um grupo de arquivos off-line é removido.|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [Estados de banco de dados](../../relational-databases/databases/database-states.md)  
  
 [Estados de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
 [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
