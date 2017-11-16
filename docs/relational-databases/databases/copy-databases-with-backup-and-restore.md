---
title: "Copiar bancos de dados com backup e restauração | Microsoft Docs"
ms.custom: 
ms.date: 07/15/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], back up and restore
- restoring databases [SQL Server], previous SQL Server versions
- database restores [SQL Server], copying databases
- restoring databases [SQL Server], onto another server instance
- restoring [SQL Server], onto another server instance
- backing up databases [SQL Server], copying databases
- database backups [SQL Server], copying databases
ms.assetid: b93e9701-72a0-408e-958c-dc196872c040
caps.latest.revision: 61
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aa3c7efcaa066953595525819686c612b5a9aee5
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="copy-databases-with-backup-and-restore"></a>Copiar bancos de dados com backup e restauração
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é possível criar um novo banco de dados por meio da restauração de um backup de um banco de dados do usuário criado por meio do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou de uma versão posterior. No entanto, backups de **master**, **model** e **msdb** que foram criados em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Além disso, backups do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não podem ser restaurados por nenhuma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
>**IMPORTANTE:** O SQL Server 2016 usa um caminho padrão diferente das versões anteriores. Portanto, para restaurar backups de um banco de dados criados no local padrão de versões anteriores, você deve usar a opção MOVE. Para obter informações sobre o novo caminho padrão, veja [Locais de arquivos para instâncias padrão e nomeadas do SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md). Para obter mais informações sobre como mover arquivos de banco de dados, consulte "Movendo arquivos do banco de dados", mais adiante neste tópico.  
  
## <a name="general-steps-for-using-backup-and-restore-to-copy-a-database"></a>Etapas gerais para usar Backup e Restauração para copiar um banco de dados  
 Quando você usa backup e restauração para copiar um banco de dados para outra instância do SQL Server, os computadores de origem e de destino podem ser todas as plataformas na qual o SQL Server é executado.  
  
 As etapas gerais são:  
  
1.  Faça backup do banco de dados de origem que pode residir em uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior. O computador no qual essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada é o **computador de origem**.  
  
2.  No computador no qual você deseja copiar o banco de dados (o **computador de destino**), conecte-se à instância do SQL Server na qual você planeja restaurar o banco de dados. Se necessário, na instância do servidor de **destino** , crie os mesmos dispositivos usados para fazer o backup dos bancos de dados de **origem** .  
  
3.  Restaure o backup do banco de dados de **origem** no computador de **destino** . A restauração do banco de dados cria automaticamente todos os arquivos de banco de dados.  
  
Algumas considerações adicionais que podem afetar esse processo:
  
## <a name="before-you-restore-database-files"></a>Antes de restaurar arquivos do banco de dados  
 A restauração de um banco de dados cria automaticamente os arquivos de banco de dados necessários para o banco de dados de restauração. Por padrão, os arquivos criados pelo SQL Server durante o processo de restauração usam os mesmos nomes e caminhos que os arquivos de backup do banco de dados original no computador de origem.  
  
 Opcionalmente, ao restaurar o banco de dados, é possível especificar o mapeamento de dispositivos, nomes de arquivos ou caminho do banco de dados de restauração. 
 
 Isso pode ser necessário nas seguintes situações:  
  
-   A estrutura do diretório ou o mapeamento da unidade usado pelo banco de dados no computador original não existe no outro computador. Por exemplo, talvez o backup contenha um arquivo que seria restaurado, por padrão, na unidade E, mas o computador de destino não tem uma unidade E.  
  
-   O local de destino talvez não tenha espaço suficiente.  
  
-   Você está reutilizando um nome de banco de dados que existe no destino de restauração e quaisquer de seus arquivos tem o mesmo nome que um arquivo de banco de dados no conjunto de backup. Ocorre uma das seguintes situações:  
  
    -   Se for possível, o arquivo de banco de dados existente será substituído (isso não afeta um arquivo que pertence a um nome de banco de dados diferente).  
  
    -   Se o arquivo existente não puder ser substituído, ocorrerá um erro na restauração.  
  
 Para evitar erros e consequências não intencionais, antes da operação de restauração, você pode usar a tabela de histórico [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) para localizar o banco de dados e os arquivos de log no backup que você planeja restaurar.  
  
## <a name="moving-the-database-files"></a>Movendo os arquivos do banco de dados  
 Se os arquivos que estão no backup do banco de dados não puderem ser restaurados no computador de destino, será necessário mover os arquivos para um novo local enquanto estiverem sendo restaurados. Por exemplo:  
  
-   Você deseja restaurar um banco de dados de backups criado no local padrão da versão anterior.  
  
-   Pode ser necessário restaurar alguns dos arquivos de banco de dados no backup para uma unidade diferente, devido a questões de capacidade. É uma ocorrência comum, porque a maioria dos computadores de uma organização não tem o mesmo número e tamanho de unidades de disco ou configurações de software idênticas.  
  
-   Pode ser necessário criar uma cópia de um banco de dados existente no mesmo computador para fins de teste. Nesse caso, os arquivos de banco de dados para o banco de dados original já existem e, portanto, é necessário especificar nomes de arquivo diferentes quando a cópia de banco de dados for criada durante a operação de restauração.  
  
 Para obter mais informações, consulte “Restaurar arquivos e grupos de arquivos para um novo local", mais adiante neste tópico.  
  
## <a name="changing-the-database-name"></a>Alterando o nome do banco de dados  
 O nome do banco de dados pode ser alterado quando for restaurado para o computador de destino, sem a necessidade de restaurar o banco de dados antes, para depois ter que alterá-lo manualmente. Por exemplo, pode ser necessário alterar o nome de banco de dados de **Sales** para **SalesCopy** para indicar que é uma cópia de um banco de dados.  
  
 O nome de banco de dados que é fornecido explicitamente ao restaurar um banco de dados é usado, automaticamente, como o nome do novo banco de dados. Como o nome do banco de dados ainda não existe, é criado um novo usando os arquivos no backup.  
  
## <a name="when-upgrading-a-database-by-using-restore"></a>Ao atualizar um banco de dados usando a restauração  
 Ao restaurar backups de uma versão anterior, é útil saber com antecedência se o caminho (unidade e diretório) de cada catálogo de texto completo em um backup existe no computador de destino. Para listar os nomes lógicos e nomes físicos, caminho e nome de arquivo, de todos os arquivos de um backup, inclusive os arquivos de catálogo, use uma instrução RESTORE FILELISTONLY FROM *<backup_device>*. Para obter mais informações, veja [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).  
  
 Se o mesmo caminho não existir no computador de destino, você terá duas alternativas:  
  
-   Criar o mapeamento equivalente da unidade/diretório no computador de destino.  
  
-   Mover os arquivos de catálogo para um novo local durante a operação de restauração, usando a cláusula WITH MOVE em sua instrução RESTORE DATABASE. Para obter mais informações, veja [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 Para obter informações sobre opções alternativas para atualizar índices de texto completo, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
## <a name="database-ownership"></a>Propriedade de banco de dados  
 Quando um banco de dados é restaurado em outro computador, o logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usuário Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] que inicia a operação de restauração torna-se automaticamente o novo proprietário do banco de dados. Quando o banco de dados é restaurado, o administrador de sistema ou o novo proprietário do banco de dados pode alterar a propriedade do banco de dados. Para prevenir a restauração não autorizada de um banco de dados, use senhas para conjuntos de mídias ou de backup.  
  
## <a name="managing-metadata-when-restoring-to-another-server-instance"></a>Gerenciando metadados ao restaurar em outra instância do servidor  
 Ao restaurar um banco de dados em outra instância do servidor, para oferecer uma experiência consistente aos usuários e aplicativos, talvez seja necessário recriar alguns ou todos os metadados para o banco de dados, como logons e trabalhos, na outra instância de servidor. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
 **Exibir os dados e arquivos de log em um conjunto de backup**  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
 **Restaurar arquivos e grupos de arquivos em um novo local**  
  
-   [Restaurar arquivos em um novo local &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **Restaurar arquivos e grupos de arquivos sobre arquivos existentes**  
  
-   [Restaurar arquivos e grupos de arquivos sobre arquivos existentes &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
 **Para restaurar um banco de dados com um novo nome**  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **Para reinicializar uma operação de restauração interrompida**  
  
-   [Reiniciar uma operação de restauração interrompida &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
 **Alterar o proprietário do banco de dados**  
  
-   [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)  
  
 **Copiar um banco de dados usando o SMO (SQL Server Management Objects)**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadFileList%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.RelocateFiles%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReplaceDatabase%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
## <a name="see-also"></a>Consulte também  
 [Copiar bancos de dados em outros servidores](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [Locais de arquivos para instâncias padrão e nomeadas do SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  

