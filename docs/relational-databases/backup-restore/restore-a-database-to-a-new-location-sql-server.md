---
title: Restaurar um banco de dados em um novo local (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restoring databases [SQL Server], moving
- database restores [SQL Server], creating new databases
- restoring [SQL Server], with move
- restoring databases [SQL Server], creating new databases
- database backups [SQL Server], creating new database from
- backing up databases [SQL Server], creating new database from
- restoring databases [SQL Server], renaming
- database creation [SQL Server], restoring with move
ms.assetid: 4da76d61-5e11-4bee-84f5-b305240d9f42
caps.latest.revision: 71
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 23023f6f4d8fe277bfee15c467be88aaa04a5723
ms.lasthandoff: 04/11/2017

---
# <a name="restore-a-database-to-a-new-location-sql-server"></a>Restaurar um banco de dados em um novo local (SQL Server)
  Este tópico descreve como restaurar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um novo local e, opcionalmente, renomear o banco de dados, no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SSMS (SQL Server Management Studio) ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você pode mover um banco de dados para um novo caminho ou criar uma cópia de um banco de dados na mesma instância do servidor ou em uma instância de servidor diferente.  
    
##  <a name="BeforeYouBegin"></a> Antes de começar.  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O administrador do sistema que restaura um backup de banco de dados completo deve ser a única pessoa a usar o banco de dados a ser restaurado.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   No modelo de recuperação completa ou bulk-logged, para que você possa restaurar um banco de dados, faça backup do log de transações ativas. Para obter mais informações, veja [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  

-   Para restaurar um banco de dados criptografado, **você deve ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados**. Sem esse certificado ou essa chave assimétrica, não é possível restaurar o banco de dados. Você deverá manter o certificado usado para criptografar a chave de criptografia do banco de dados durante o tempo em que você precisar do backup! Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Para obter considerações adicionais sobre a movimentação de um banco de dados, consulte [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
-   Se você restaurar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou superior para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados será atualizado automaticamente. Normalmente, o banco de dados se torna disponível imediatamente. No entanto, se um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices, dependendo da configuração da propriedade de servidor  **upgrade_option** . Se a opção de atualização for definida como importar (**upgrade_option** = 2) ou recriar (**upgrade_option** = 0), os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida para importar, os índices de texto completo associados serão recriados se um catálogo de texto completo não estiver disponível. Para alterar a configuração da propriedade de servidor **upgrade_option** , use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
###  <a name="Security"></a> Segurança  
 Por motivos de segurança, é recomendável não anexar ou restaurar bancos de dados de origens desconhecidas ou não confiáveis. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
####  <a name="Permissions"></a> Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE assumirão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** , e o proprietário (**dbo**) do banco de dados.  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
  
## <a name="restore-a-database-to-a-new-location-optionally-rename-the-database-using-ssms"></a>Restaurar um banco de dados em um novo local; opcionalmente, renomeie o banco de dados usando o SSMS 

  
1.  Conecte-se à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e, no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Clique com o botão direito do mouse em **Bancos de Dados**e clique em **Restaurar Banco de Dados**. A caixa de diálogo **Restaurar Banco de Dados** é aberta.  
  
3.  Na página **Geral** , use a seção **Origem** para especificar a origem e o local dos conjuntos de backup a serem restaurados. Selecione uma das opções a seguir:  
  
    -   **Banco de dados**  
  
         Selecione o banco de dados a ser restaurado na lista suspensa. A lista contém apenas os bancos de dados dos quais foi feito um backup de acordo com o histórico de backup do **msdb** .  
  
    > **OBSERVAÇÃO:** se o backup foi feito de um servidor diferente, o servidor de destino não terá as informações de histórico de backup do banco de dados especificado. Nesse caso, selecione **Dispositivo** para especificar manualmente o arquivo ou o dispositivo a ser restaurado.  
  
    1.  **Dispositivo**  
  
         Clique no botão Procurar (**...**) para abrir a caixa de diálogo **Selecione dispositivos de backup** . Na caixa **Tipo de mídia de backup** , selecione um dos tipos de dispositivo listados. Para selecionar um ou mais dispositivos da caixa **Mídia de backup** , clique em **Adicionar**.  
  
         Após adicionar os dispositivos desejados à caixa de listagem **Mídia de backup** , clique em **OK** para voltar à página **Geral** .  
  
         Na caixa de listagem **Origem: Dispositivo: Banco de Dados** , selecione o nome do banco de dados que deve ser restaurado.  
  
         **Observação** Essa lista estará disponível apenas quando **Dispositivo** for selecionado. Apenas os bancos de dados que têm backups no dispositivo selecionado estarão disponíveis.  
  
4.  Na seção **Destino** , a caixa **Banco de Dados** é preenchida automaticamente com o nome do banco de dados a ser restaurado. Para alterar o nome do banco de dados, digite o novo nome na caixa **Banco de Dados** .  
  
5.  Na caixa **Restaurar para** , deixe o padrão como **Para o último backup obtido** ou clique em **Linha do tempo** para acessar a caixa de diálogo **Linha do Tempo de Backup** para selecionar manualmente um momento determinado a fim de interromper a ação de recuperação. Consulte [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md) para obter mais informações sobre como designar um momento determinado.  
  
6.  Na grade **Conjuntos de backup a serem restaurados** , selecione os backups a serem restaurados. Essa grade exibe os backups disponíveis para o local especificado. Por padrão, um plano de recuperação é sugerido. Para substituir o plano de recuperação sugerido, você pode alterar as seleções na grade. Backups que dependem da restauração de um backup anterior têm a seleção automaticamente cancelada quando a seleção do backup anterior é cancelada.  
  
     Para obter informações sobre as colunas da grade **Selecionar os conjuntos de backup a serem restaurados**, veja [Restaurar banco de dados &#40;Página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md).  
  
7.  Para especificar o novo local dos arquivos de banco de dados, selecione a página **Arquivos** e clique em **Realoque todos os arquivos para pasta**. Forneça um novo local para a **Pasta do arquivo de dados** e **Pasta do arquivo de log**. Para obter mais informações sobre essa grade, veja [Restaurar banco de dados &#40;Página Arquivos&#41;](../../relational-databases/backup-restore/restore-database-files-page.md).  
  
8.  Na página **Opções** , ajuste as opções desejadas. Para obter mais informações sobre essas opções, veja [Restaurar banco de dados &#40;Página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).  

 ## <a name="restore-database-to-a-new-location-optionally-rename-the-database-using-t-sql"></a>Restaurar um banco de dados em um novo local; opcionalmente, renomeie o banco de dados usando o T-SQL
 
 
1.  Opcionalmente, determine os nomes lógicos e físicos dos arquivos no conjunto de backup que contém o backup completo de banco de dados que você deseja restaurar. Essa instrução retorna a uma lista de arquivos de banco de dados e de log contidos no conjunto de backup. A sintaxe básica é a seguinte:  
  
     RESTORE FILELISTONLY FROM *<backup_device>* WITH FILE = *backup_set_file_number* 
  
     Aqui, *backup_set_file_number* indica a posição do backup no conjunto de mídias. Você pode obter a posição de um conjunto de backup por meio da instrução [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) . Para obter mais informações, consulte "Especificando um conjunto de backup", em [Argumentos RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
     Essa instrução também dá suporte a uma série de opções WITH. Para obter mais informações, veja [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).  
  
2.  Use a instrução [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) para restaurar o backup completo do banco de dados. Por padrão, os arquivos de dados e de log são restaurados em seus locais originais. Para realocar um banco de dados, use a opção MOVE para realocar cada um dos arquivos do banco de dados e para evitar colisões com arquivos existentes.  
  
     A sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] básica para restaurar o banco de dados em um novo local e com um novo nome é:  
  
     RESTORE DATABASE *new_database_name*  
  
     FROM *backup_device* [ ,...*n* ]  
  
     [ WITH  
  
     {  
  
     [ **RECOVERY** | NORECOVERY ]  
  
     [ , ] [ FILE ={ *backup_set_file_number* | @*backup_set_file_number* } ]  
  
     [ , ] MOVE '*logical_file_name_in_backup*' TO '*operating_system_file_name*' [ ,...*n* ]  
  
     }  
  
     ;  
  
    > **OBSERVAÇÃO:** Ao se preparar para realocar um banco de dados em um disco diferente, você deve verificar se espaço suficiente está disponível e identificar todas as colisões potenciais com arquivos existentes. Isso envolve o uso de uma instrução [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md) que especifica os mesmos parâmetros MOVE que você planeja usar em sua instrução RESTORE DATABASE.  
  
     A tabela a seguir descreve os argumentos dessa instrução RESTORE em termos de restauração de um banco de dados em um novo local. Para obter mais informações sobre esses argumentos, consulte [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
     *new_database_name*  
     O novo nome do banco de dados.  
  
    >**OBSERVAÇÃO:** se você estiver restaurando o banco de dados em uma instância de servidor diferente, poderá usar o nome do banco de dados original em vez de um novo nome.  
  
     *backup_device* [ **,**...*n* ]  
     Especifica uma lista separada por vírgulas de 1 a 64 dispositivos de backup nos quais o backup de banco de dados precisa ser restaurado. Você pode especificar um dispositivo de backup físico ou especificar um dispositivo de backup lógico correspondente, se definido. Para especificar um dispositivo de backup físico, use a opção DISK ou TAPE:  
  
     { DISK | TAPE } **=***physical_backup_device_name*  
  
     Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
     { **RECOVERY** | NORECOVERY }  
     Se o banco de dados usar o modelo de recuperação completa, você poderá precisar aplicar backups de log de transações depois de restaurar o banco de dados. Nesse caso, especifique a opção NORECOVERY.  
  
     Caso contrário, use a opção de RECOVERY que é a padrão.  
  
     FILE = { *backup_set_file_number* | @*backup_set_file_number* }  
     Identifica o conjunto de backup a ser restaurado. Por exemplo, um *backup_set_file_number* de **1** indica o primeiro conjunto de backup na mídia de backup e um *backup_set_file_number* de **2** indica o segundo conjunto de backup. Você pode obter o *backup_set_file_number* de um backup definido usando a instrução [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) .  
  
     Quando esta opção não está especificada, o padrão é usar o primeiro conjunto de backup no dispositivo de backup.  
  
     Para obter mais informações, consulte "Especificando um conjunto de backup", em [Argumentos RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
     MOVE **'***logical_file_name_in_backup***'** TO **'***operating_system_file_name***'** [ **,**...*n* ]  
     Especifica que o arquivo de log ou de dados especificado pelo *logical_file_name_in_backup* deve ser restaurado no local especificado pelo *operating_system_file_name*. Especifique uma instrução MOVE para cada arquivo lógico que você deseja restaurar do conjunto de backup para um novo local.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |*logical_file_name_in_backup*|Especifica o nome lógico de um arquivo de log ou de dados no conjunto de backup. O nome do arquivo lógico de um arquivo de log ou de dados em um conjunto de backup corresponde ao seu nome lógico no banco de dados quando o conjunto de backup foi criado.<br /><br /> <br /><br /> Observação: para obter uma lista dos arquivos lógicos do conjunto de backup, use [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).|  
    |*operating_system_file_name*|Especifica um novo local para o arquivo especificado por *logical_file_name_in_backup*. O arquivo será restaurado neste local.<br /><br /> Opcionalmente, *operating_system_file_name* especifica um novo nome de arquivo para o arquivo restaurado. Isso será necessário se você estiver criando uma cópia de um banco de dados existente na mesma instância de servidor.|  
    |*n*|É um espaço reservado que indica que você pode especificar instruções MOVE adicionais.|  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo cria um novo banco de dados denominado `MyAdvWorks` por meio da restauração de um backup do banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que inclui dois arquivos: [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Data e [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Log. Esse banco de dados usa o modelo de recuperação simples. O banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] já existe na instância do servidor, portanto, os arquivos no backup devem ser restaurados em um novo local. A instrução RESTORE FILELISTONLY é usada para determinar o número e os nomes dos arquivos no banco de dados que está sendo restaurado. O backup do banco de dados é o primeiro conjunto de backup no dispositivo de backup.  
  
> **OBSERVAÇÃO:** os exemplos de como fazer backup e restaurar o log de transações, incluindo restaurações pontuais, usam o banco de dados `MyAdvWorks_FullRM` que é criado no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] exatamente como no exemplo `MyAdvWorks` a seguir. No entanto, o banco de dados `MyAdvWorks_FullRM` resultante deve ser alterado para usar o modelo de recuperação completa por meio da seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]: ALTER DATABASE <database_name> SET RECOVERY FULL.  
  
```tsql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
-- AdventureWorks2012_Backup is the name of the backup device.  
RESTORE FILELISTONLY  
   FROM AdventureWorks2012_Backup;  
-- Restore the files for MyAdvWorks.  
RESTORE DATABASE MyAdvWorks  
   FROM AdventureWorks2012_Backup  
   WITH RECOVERY,  
   MOVE 'AdventureWorks2012_Data' TO 'D:\MyData\MyAdvWorks_Data.mdf',   
   MOVE 'AdventureWorks2012_Log' TO 'F:\MyLog\MyAdvWorks_Log.ldf';  
GO  
  
```  
  
 Para obter um exemplo de como criar um backup de banco de dados completo do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , consulte [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)  
  
  

