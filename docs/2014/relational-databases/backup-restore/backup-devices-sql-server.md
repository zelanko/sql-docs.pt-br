---
title: Dispositivos de backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- tape backup devices, about tape backup devices
- backup devices [SQL Server]
- disk backup devices [SQL Server]
- database backups [SQL Server], backup devices
- logical devices [SQL Server]
- backup devices [SQL Server], about backup devices
- backing up [SQL Server], backup devices
- removable media [SQL Server]
- network shares [SQL Server]
- backups [SQL Server], backup devices
- tape backup devices
- physical devices [SQL Server]
- backing up databases [SQL Server], backup devices
- devices [SQL Server]
ms.assetid: 35a8e100-3ff2-4844-a5da-dd088c43cba4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7cd01f1a3c98bcf0d67ab0224772538a7a82514d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922176"
---
# <a name="backup-devices-sql-server"></a>Dispositivos de backup (SQL Server)
  Durante uma operação de backup em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os dados submetidos a backup (o *backup*) são gravados em um dispositivo de backup físico. Esse dispositivo de backup físico é inicializado quando o primeiro backup em um conjunto de mídias é gravado nele. Os backups em um conjunto de um ou mais dispositivos de backup compõem um único conjunto de mídias.  
  
 **Neste tópico:**  
  
-   [Termos e definições](#TermsAndDefinitions)  
  
-   [Usando dispositivos de Backup de disco](#DiskBackups)  
  
-   [Usando dispositivos de fita](#TapeDevices)  
  
-   [Usando um dispositivo de Backup lógico](#LogicalBackupDevice)  
  
-   [Conjuntos de mídias de Backup espelhado](#MirroredMediaSets)  
  
-   [Arquivando Backups do SQL Server](#Archiving)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="TermsAndDefinitions"></a> Termos e definições  
 disco de backup  
 Um disco rígido ou outra mídia de armazenamento em disco que contém um ou mais arquivos de backup. Um arquivo de backup é um arquivo de sistema operacional regular.  
  
 conjunto de mídias  
 Uma coleção ordenada de mídias de backup, fitas ou arquivos de disco, que utiliza um tipo e número fixos de dispositivos de backup. Para obter mais informações sobre conjuntos de mídias, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
 dispositivo de backup físico  
 Uma unidade de fita ou um arquivo de disco é fornecido pelo sistema operacional. Um backup pode ser gravado em 1 a 64 dispositivos de backup. Se um backup exigir vários dispositivos de backup, todos os dispositivos deverão corresponder a um único tipo de dispositivo (disco ou fita).  
  
 Os backups do SQL Server podem ser gravados no serviço de armazenamento Blob do Windows Azure, bem como em disco ou fita.  
  
##  <a name="DiskBackups"></a> Usando dispositivos de Backup de disco  
 **Nesta seção:**  
  
-   [A especificação de um arquivo de Backup usando seu nome físico (Transact-SQL)](#BackupFileUsingPhysicalName)  
  
-   [Especificando o caminho de um arquivo de Backup de disco](#BackupFileDiskPath)  
  
-   [Fazendo backup em um arquivo em um compartilhamento de rede](#NetworkShare)  
  
 Se um arquivo de disco ficar cheio enquanto uma operação de backup estiver anexando um backup ao conjunto de mídias, a operação de backup falhará. O tamanho máximo de um arquivo de backup é determinado pelo espaço livre de disco disponível no dispositivo de disco, portanto o tamanho apropriado de um dispositivo de disco de backup depende do tamanho de seus backups.  
  
 Um dispositivo de backup de disco pode ser um simples dispositivo de disco, como uma unidade ATA. Como alternativa, pode-se usar uma unidade de disco removível que permite a substituição de um disco cheio na unidade por um disco vazio. Um disco de backup pode ser um disco local no servidor ou um disco remoto que é um recurso de rede compartilhado. Para obter informações sobre como usar um disco remoto, consulte [Fazendo backup em um arquivo em um compartilhamento de rede](#NetworkShare), posteriormente neste tópico.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As ferramentas de gerenciamento são muito flexíveis para manusear dispositivos de backup em disco, pois elas geram automaticamente um nome com carimbo de data/hora no arquivo em disco.  
  
> [!IMPORTANT]  
>  Nós recomendamos que um disco de backup seja diferente dos discos de banco de dados e de log. Isso é necessário para garantir que será possível acessar os backups se houver falha no disco de dados ou de log.  
  
###  <a name="BackupFileUsingPhysicalName"></a> A especificação de um arquivo de Backup usando seu nome físico (Transact-SQL)  
 A sintaxe básica [BACKUP](/sql/t-sql/statements/backup-transact-sql) para especificar um arquivo de backup com seu nome de dispositivo físico é:  
  
 BACKUP DATABASE *database_name*  
  
 TO DISK **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 Por exemplo:  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';  
GO  
```  
  
 Para especificar um dispositivo de disco físico em uma instrução [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) , a sintaxe básica é:  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM DISK **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 Por exemplo,  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';   
```  
  
###  <a name="BackupFileDiskPath"></a> Especificando o caminho de um arquivo de Backup de disco  
 Ao especificar um arquivo de backup, você deve digitar seu caminho completo e o nome do arquivo. Se você especificar somente o nome de arquivo ou um caminho relativo ao fazer o backup de um arquivo, o arquivo de backup será armazenado no diretório de backup padrão. O diretório de backup padrão é C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*n*\MSSQL\Backup, em que *n* é o número da instância do servidor. Portanto, para a instância de servidor padrão, o diretório de backup padrão é: C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup.  
  
 Para evitar ambiguidade, especialmente em scripts, é recomendável especificar explicitamente o caminho do diretório de backup em cada cláusula DISK. Porém, isto é menos importante quando você está usando o Editor de Consultas. Nesse caso, se você tiver certeza de que o arquivo de backup reside no diretório de backup padrão, pode-se omitir o caminho da cláusula DISK. Por exemplo, a instrução `BACKUP` a seguir faz o backup do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] no diretório de backup padrão.  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'AdventureWorks2012.bak';  
GO  
```  
  
> [!NOTE]  
>  O local padrão é armazenado na chave do Registro **BackupDirectory** em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.n\MSSQLServer**.  
  
###  <a name="NetworkShare"></a> Fazendo backup em um arquivo em um compartilhamento de rede  
 Para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acesse um arquivo de disco remoto, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter acesso ao compartilhamento de rede. Isso inclui ter as permissões necessárias para que as operações de backup possam gravar no compartilhamento de rede e as operações de restauração possam ler a partir do compartilhamento de rede. A disponibilidade de unidades de rede e permissões depende do contexto no qual o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está executando:  
  
-   Para fazer backup em uma unidade de rede quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está executando em uma conta de usuário de domínio, a unidade compartilhada deve ser mapeada como uma unidade de rede na sessão onde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado. Se você iniciar o Sqlservr.exe da linha de comando, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verá todas as unidades de rede mapeadas em sua sessão de logon.  
  
-   Ao executar o Sqlservr.exe como um serviço, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado em uma sessão separada que não tem nenhuma relação com sua sessão de logon. A sessão na qual um serviço é executado pode ter suas próprias unidades mapeadas, embora normalmente não tenha.  
  
-   Você pode se conectar a conta de serviço de rede usando a conta do computador em vez de um usuário de domínio. Para ativar backups de computadores específicos para uma unidade compartilhada, conceda acesso às contas do computador. Desde que o processo Sqlservr.exe que está gravando o backup tenha acesso, é irrelevante se o usuário que está enviando o comando BACKUP tem acesso.  
  
    > [!IMPORTANT]  
    >  Fazer backup de dados em uma rede pode ocasionar erros de rede e por isso, é recomendável que você, quando estiver usando uma unidade remota, verifique a operação de backup após concluí-lo. Para obter mais informações, consulte [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).  
  
#### <a name="specifying-a-universal-naming-convention-unc-name"></a>Especificando um nome UNC (Convenção de Nomenclatura Universal)  
 Para especificar um compartilhamento de rede em um comando de backup ou de restauração, é necessário usar o nome UNC (convenção de nomenclatura universal) totalmente qualificado do arquivo para o dispositivo de backup. Um nome UNC tem a forma **\\\\** _Systemname_ **\\** _ShareName_ **\\** _Path_ **\\** _FileName_.  
  
 Por exemplo:  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = '\\BackupSystem\BackupDisk1\AW_backups\AdventureWorksData.Bak';  
GO  
```  
  
##  <a name="TapeDevices"></a> Usando dispositivos de fita  
  
> [!NOTE]  
>  O suporte a dispositivos de backup em fita será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 **Nesta seção:**  
  
-   [Especificando uma fita de Backup usando seu nome físico (Transact-SQL)](#BackupTapeUsingPhysicalName)  
  
-   [BACKUP de fita específica e as opções de restauração (Transact-SQL)](#TapeOptions)  
  
-   [Gerenciando fitas abertas](#OpenTapes)  
  
 Para fazer o backup de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em fita, é necessário que haja suporte para a(s) unidade(s) de fita no sistema operacional [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Além disso, para determinada unidade de fita, nós recomendamos que você só utilize as fitas recomendadas pelo fabricante da unidade. Para obter mais informações sobre como instalar uma unidade de fita, consulte a documentação do sistema operacional Windows.  
  
 Quando uma unidade de fita é usada, uma operação de backup pode preencher uma fita e continuar em outra fita. Cada fita contém um cabeçalho de mídia. A primeira mídia usada é chamada *fita inicial*. Cada fita sucessiva é conhecida como uma *fita de continuação* e tem um número de sequência de mídia uma vez superior à fita anterior. Por exemplo, um conjunto de mídias associado a quatro dispositivos de mídia contém pelo menos quatro fitas iniciais (e, se o banco de dados não couber, quatro séries de fitas de continuação). Ao anexar um conjunto de backup, você deve montar a última fita na série. Se a última fita não estiver montada, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] examina até o final da fita e solicita que você troque a fita. Neste ponto, monte a última fita.  
  
 Os dispositivos de backup de fita são usados como dispositivos de disco, com as seguintes exceções:  
  
-   O dispositivo de fita deve estar conectado fisicamente ao computador que está executando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O backup em dispositivos de fita remotos não é suportado.  
  
-   Se um dispositivo de backup em fita for preenchido durante a operação de backup, e mais dados ainda precisarem ser gravados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitará uma nova fita e continuará a operação de backup depois que a nova fita for carregada.  
  
###  <a name="BackupTapeUsingPhysicalName"></a> Especificando uma fita de Backup usando seu nome físico (Transact-SQL)  
 A sintaxe básica de [BACKUP](/sql/t-sql/statements/backup-transact-sql) para especificar uma fita de backup usando o nome do dispositivo físico da unidade de fita é:  
  
 BACKUP { DATABASE | LOG } *database_name*  
  
 TO TAPE **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 Por exemplo:  
  
```  
BACKUP LOG AdventureWorks2012   
   TO TAPE = '\\.\tape0';  
GO  
```  
  
 Para especificar um dispositivo de fita físico em uma instrução [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) , a sintaxe básica é:  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM TAPE **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
###  <a name="TapeOptions"></a> BACKUP de fita específica e as opções de restauração (Transact-SQL)  
 Para facilitar o gerenciamento de fitas, a instrução BACKUP fornece as seguintes opções específicas a fitas:  
  
-   { NOUNLOAD | **UNLOAD** }  
  
     Você pode controlar se uma fita de backup é descarregada automaticamente da unidade de fita após uma operação de backup ou restauração. UNLOAD/NOUNLOAD é uma configuração de sessão que persiste durante a vida útil da sessão ou até que ela seja redefinida especificando a alternativa.  
  
-   { **REWIND** | NOREWIND }  
  
     Você pode controlar se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém a fita aberta após a operação de backup ou restauração ou libera e rebobina a fita após o preenchimento. O comportamento padrão é rebobinar a fita (REWIND).  
  
> [!NOTE]  
>  Para obter mais informações sobre sintaxe e argumentos BACKUP, consulte [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql). Para obter mais informações sobre a sintaxe e os argumentos de RESTORE, consulte [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) e [Argumentos RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql), respectivamente.  
  
###  <a name="OpenTapes"></a> Gerenciando fitas abertas  
 Para exibir uma lista de dispositivos de fitas abertas e o status das solicitações de montagem, consulte a exibição de gerenciamento dinâmico [sys.dm_io_backup_tapes](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql) . Esta exibição mostra todas as fitas abertas. Elas incluem fitas em uso que estão temporariamente inativas enquanto esperam a próxima operação de BACKUP ou RESTAURAÇÃO.  
  
 Se uma fita foi acidentalmente deixada aberta, a maneira mais rápida para liberar a fita é usando o comando a seguir: RESTORE REWINDONLY FROM TAPE **=** _backup_device_name_. Para obter mais informações, consulte [RESTORE REWINDONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-rewindonly-transact-sql).  
  
## <a name="using-the-windows-azure-blob-storage-service"></a>Usando o serviço de armazenamento de Blob do Windows Azure  
 Os backups do SQL Server podem ser gravados no serviço de armazenamento de Blob do Windows Azure.  Para obter mais informações sobre como usar o serviço de armazenamento de Blob do Windows Azure para seus backups, consulte [Backup e restauração do SQL Server com o serviço de armazenamento de Blob do Windows Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
##  <a name="LogicalBackupDevice"></a> Usando um dispositivo de Backup lógico  
 Um *dispositivo de backup lógico* é um nome opcional definido pelo usuário que aponta para um dispositivo de backup físico específico (um arquivo de disco ou uma unidade de fita). Um dispositivo de backup lógico permite que você use nomes indiretos ao fazer referência ao dispositivo de backup físico correspondente.  
  
 Definir um dispositivo de backup lógico envolve a atribuição de um nome lógico a um dispositivo físico. Por exemplo, um dispositivo lógico, AdventureWorksBackups, pode ser definido para apontar para o arquivo Z:\SQLServerBackups\AdventureWorks2012.bak ou a unidade de fita \\\\.\tape0. Os comandos de backup e restauração podem especificar o AdventureWorksBackups como o dispositivo de backup, em vez de DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' ou TAPE = '\\\\.\tape0'.  
  
 O nome de dispositivo lógico deve ser exclusivo entre todos os dispositivos de backup lógicos na instância do servidor. Para exibir os nomes de dispositivo lógicos existentes, consulte a exibição do catálogo [sys.backup_devices](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql) . Essa exibição mostra o nome de cada dispositivo de backup lógico e descreve o tipo e o nome de arquivo físico ou caminho do dispositivo de backup físico correspondente.  
  
 Depois que um dispositivo de backup lógico é definido, em um comando de BACKUP ou RESTAURAÇÃO, é possível especificar o dispositivo de backup lógico em vez do nome físico do dispositivo. Por exemplo, a instrução seguinte faz backup do banco de dados `AdventureWorks2012` no dispositivo de backup lógico `AdventureWorksBackups` .  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups;  
GO  
```  
  
> [!NOTE]  
>  Em uma determinada instrução de BACKUP ou RESTAURAÇÃO, o nome do dispositivo de backup lógico e o nome do dispositivo de backup físico correspondente são intercambiáveis.  
  
 Uma vantagem de usar um dispositivo de backup lógico é que é mais simples do que usar um caminho longo. Usar um dispositivo de backup lógico poderá ajudar se você planeja gravar uma série de backups no mesmo caminho ou em um dispositivo de fita. Os dispositivos de backup lógicos são especialmente úteis para identificar dispositivos de backup em fita.  
  
 Um script de backup pode ser gravado para usar um dispositivo de backup lógico particular. Isso permite que você alterne para novos dispositivos de backup físicos sem atualizar o script. Alternar envolve o seguinte processo:  
  
1.  Descartar o dispositivo de backup lógico original.  
  
2.  Definir um novo dispositivo de backup lógico que usa o nome de dispositivo lógico original, mas mapeia em um dispositivo de backup físico diferente. Os dispositivos de backup lógicos são especialmente úteis para identificar dispositivos de backup em fita.  
  
##  <a name="MirroredMediaSets"></a> Conjuntos de mídias de Backup espelhado  
 O espelhamento de conjuntos de mídias de backup reduz o efeito de maus funcionamentos do dispositivo de backup. Esses maus funcionamentos são especialmente sérios uma vez que os backups são a última linha de defesa contra a perda de dados. À medida que o tamanho dos bancos de dados cresce, aumenta a probabilidade de que uma falha de um dispositivo de backup ou mídia torne impossível a restauração de um backup. O espelhamento de mídias de backup aumenta a confiabilidade de backups fornecendo redundância para o dispositivo de backup físico. Para obter mais informações, veja [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md).  
  
> [!NOTE]  
>  Os conjuntos de mídias de backup espelhados oferecem suporte somente em [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] e versões posteriores.  
  
##  <a name="Archiving"></a> Arquivando Backups do SQL Server  
 Recomendamos que você use um utilitário de backup do sistema de arquivos para arquivar os backups de disco e que armazene os arquivos externamente. Usar um disco tem a vantagem de usar a rede para gravar os backups arquivados em um disco externo. O serviço de armazenamento de Blob do Windows Azure pode ser usado como a opção de arquivamento fora do site.  Você pode carregar seus backups em disco ou gravar diretamente os backups no serviço de armazenamento de BLOB do Windows Azure.  
  
 Outra abordagem de arquivamento comum é gravar os backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um disco de backup local, arquivá-los em uma fita e, em seguida, armazenar as fitas externamente.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para especificar um dispositivo de disco (SQL Server Management Studio)**  
  
-   [Especificar um disco ou fita como destino de backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **Para especificar um dispositivo de fita (SQL Server Management Studio)**  
  
-   [Especificar um disco ou fita como destino de backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **Para definir um dispositivo de backup lógico**  
  
-   [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)  
  
-   [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.BackupDevice> (SMO)  
  
 **Para usar um dispositivo de backup lógico**  
  
-   [Especificar um disco ou fita como destino de backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Restaurar um backup de um dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
 **Para exibir informações sobre dispositivos de backup**  
  
-   [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)  
  
-   [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Exibir o conteúdo de um arquivo ou fita de backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
 **Para excluir um dispositivo de backup lógico**  
  
-   [sp_dropdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)  
  
-   [Excluir um dispositivo de backup &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server, objeto Backup Device](../performance-monitor/sql-server-backup-device-object.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Planos de manutenção](../maintenance-plans/maintenance-plans.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)   
 [sys.backup_devices &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sys.dm_io_backup_tapes &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql)   
 [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)  
  
  
