---
title: 'Backup e restauração: interoperabilidade e coexistência (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server], related features
- restoring [SQL Server], files
- restoring files [SQL Server], related features
- backups [SQL Server], files or filegroups
- file backups [SQL Server], related features
ms.assetid: 69f212b8-edcd-4c5d-8a8a-679ced33c128
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7f689fcf2082a6a025fbd41f743ba7bd40225d32
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="backup-and-restore-interoperability-and-coexistence-sql-server"></a>Backup e restauração: interoperabilidade e coexistência (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve considerações de backup e restauração para vários recursos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Estes recursos incluem: restauração de arquivo e inicialização de banco de dados; restauração online e índices desabilitados; espelhamento de banco de dados; restauração por etapas e índices de texto completo.  
  
 **Neste tópico:**  
  
-   [Restauração de arquivo e inicialização de banco de dados](#FileRestoreAndDbStartup)  
  
-   [Restauração online e índices desabilitados](#OnlineRestoreAndDisabledIndexes)  
  
-   [Espelhamento de banco de dados e backup e restauração](#DbMandBnR)  
  
-   [Restauração por etapas e índices de texto completo](#PiecemealAndFTIndexes)  
  
-   [Backup de arquivo, restauração e compactação](#FileBnRandCompression)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="FileRestoreAndDbStartup"></a> Restauração de arquivo e inicialização de banco de dados  
 Esta seção é relevante apenas para bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que têm diversos grupos de arquivos.  
  
> [!NOTE]  
>  Quando um banco de dados é iniciado, somente os grupos de arquivos cujos arquivos estavam online no fechamento do banco de dados são recuperados e colocados online.  
  
 Se um problema for encontrado durante a inicialização do banco de dados, a recuperação falhará, e o banco de dados será marcado como SUSPECT. Se o problema puder ser isolado a um arquivo ou arquivos, o administrador do banco de dados poderá colocar os arquivos offline e tentar reinicializar o banco de dados. Para colocar um arquivo offline, você pode usar a seguinte instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) :  
  
 ALTER DATABASE *database_name* MODIFY FILE (NAME **='***filename***'**, OFFLINE)  
  
 Se a inicialização tiver êxito, qualquer grupo de arquivos que contiver um arquivo offline permanecerá offline.  
  
##  <a name="OnlineRestoreAndDisabledIndexes"></a> Restauração online e índices desabilitados  
 Esta seção é relevante apenas para bancos de dados com vários grupos de arquivos e para o modelo de recuperação simples, pelo menos um grupo de arquivos somente leitura.  
  
 Nesses casos, quando um banco de dados estiver online, o índice poderá ser criado, descartado, habilitado ou desabilitado apenas se todos os grupos de arquivos contendo qualquer parte do índice estiverem online.  
  
 Para obter informações sobre como restaurar grupos de arquivos offline, veja [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
##  <a name="DbMandBnR"></a> Espelhamento de banco de dados e backup e restauração  
 Esta seção é relevante apenas para bancos de dados modelo completo que têm vários grupos de arquivos.  
  
> [!NOTE]  
>  O recurso de espelhamento de banco de dados será removido em uma versão futura do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .  
  
 O espelhamento de banco de dados é uma solução para aumentar a disponibilidade do banco de dados. O espelhamento é implementado por base de banco de dados e só funciona com bancos de dados que usam o modelo de recuperação completa. Para obter mais informações, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
> [!NOTE]  
>  Para distribuir cópias de um subconjunto dos grupos de arquivos em um banco de dados, use a replicação: replique somente os objetos nos grupos de arquivos que você quer copiar em outros servidores. Para obter mais informações sobre a replicação transacional, veja [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).  
  
### <a name="creating-the-mirror-database"></a>Criando o banco de dados espelho  
 O banco de dados espelho é criado pela restauração, WITH NORECOVERY, de backups do banco de dados principal no servidor espelho. A restauração deve manter o mesmo nome do banco de dados. Para obter mais informações, consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
 Você pode criar o banco de dados espelho usando uma sequência de restauração por etapas, onde houver suporte. Porém, você não pode iniciar o espelhamento enquanto não restaurar todos os grupos de arquivos e, normalmente, os backups de log restaurados para trazer o banco de dados espelho o mais próximo possível do banco de dados principal. Para obter mais informações, veja [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).  
  
### <a name="restrictions-on-backup-and-restore-during-mirroring"></a>Restrições de backup e restauração durante o espelhamento  
 Quando a sessão de espelhamento de banco de dados está ativa, as seguintes restrições são aplicadas:  
  
-   Não é permitido restaurar ou fazer backup do banco de dados espelho.  
  
-   É permitido fazer backup do banco de dados principal, mas BACKUP LOG WITH NORECOVERY não é permitido.  
  
-   Não é permitido restaurar o banco de dados principal.  
  
##  <a name="PiecemealAndFTIndexes"></a> Restauração por etapas e índices de texto completo  
 Esta seção só é relevante para bancos de dados contendo vários grupos de arquivos e, nos bancos de dados modelo simples, apenas para grupos de arquivos somente leitura.  
  
 Os índices de texto completo são armazenados em grupos de arquivos de banco de dados e podem ser afetados por uma restauração por etapas. Se o índice de texto completo residir no mesmo grupo de arquivos que quaisquer dados da tabela associada, a restauração por etapas funcionará normalmente.  
  
> [!NOTE]  
>  Para exibir a ID do grupo de arquivos que contém um índice de texto completo, selecione a coluna data_space_id de [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
### <a name="full-text-indexes-and-tables-in-separate-filegroups"></a>Índices de texto completo e tabelas em grupos de arquivos separados  
 Se um índice de texto completo residir em um grupo de arquivos separado de todos os dados da tabela associada, o comportamento da restauração por etapas dependerá de qual dos grupos de arquivos é restaurado e colocado online primeiro:  
  
-   Se o grupo de arquivos que contém o índice de texto completo for restaurado e colocado online antes dos grupos de arquivos que contêm os dados da tabela associada, a pesquisa de texto completo funcionará normalmente assim que o índice de texto completo estiver online.  
  
-   Se o grupo de arquivos que contém os dados da tabela for restaurado e colocado online antes do grupo de arquivos que contém o índice de texto completo, o comportamento do texto completo poderá ser afetado. Isso acontece porque as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que disparam uma população, recriam ou reorganizam o catálogo falham até o índice estar online. Essas instruções incluem CREATE FULLTEXT INDEX, ALTER FULLTEXT INDEX, DROP FULLTEXT INDEX e ALTER FULLTEXT CATALOG.  
  
     Neste caso, os seguintes fatores são significativos:  
  
    -   Se o índice de texto completo tiver controle de alterações, o DML de usuário falhará até que o grupo de arquivos de índice seja colocado online. A operação de exclusão também falhará até que o grupo de arquivos de índice esteja online.  
  
    -   Independentemente do controle de alterações, as consultas de texto completo falham porque o índice não está disponível. Se houver uma tentativa de consulta de texto completo quando o grupo de arquivos que contém o índice de texto completo estiver offline, um erro será retornado.  
  
    -   As funções de status (ex.: FULLTEXTCATALOGPROPERTY) terão êxito somente quando não precisarem acessar o índice de texto completo. Por exemplo, o acesso a quaisquer metadados de texto completo online terá êxito, mas **uniquekeycount, itemcount** falhará.  
  
     Quando o grupo de arquivos de índice de texto completo estiver restaurado e online, os dados do índice e os dados da tabela ficarão consistentes.  
  
 Assim que o grupo de arquivos de tabela base e o grupo de arquivos de índice de texto completo estiverem online, qualquer população de texto completo em pausa será retomada.  
  
##  <a name="FileBnRandCompression"></a> Backup de arquivo, restauração e compactação  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à compactação de dados de sistema de arquivos NTFS de grupos de arquivos e bancos de dados somente leitura.  
  
 Restaurando arquivos em um grupo de arquivo somente leitura há suporte em arquivos NTFS compactados. Backup e restauração destes grupos de arquivo funcionam essencialmente em qualquer grupo de arquivo somente leitura, com as seguintes exceções:  
  
-   Restaurando um arquivo leitura e gravação (inclusive o primário ou arquivos de log de um banco de dados de leitura e gravação) para um volume compactado falho e exibição de erro.  
  
-   Restaurando um banco de dados somente leitura para um volume compactado é permitido.  
  
> [!NOTE]  
>  Arquivos de Log de bancos de dados de leitura e gravação nunca deveriam ser colocados em sistemas de arquivo compactado.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [Fazer backup e restaurar índices e catálogos de texto completo](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e Restauração de bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
[Secundárias ativas: Backup em réplicas secundárias \(Grupos de Disponibilidade AlwaysOn\)](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
  
  
