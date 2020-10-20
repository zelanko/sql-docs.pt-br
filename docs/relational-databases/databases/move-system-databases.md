---
description: Mover bancos de dados do sistema
title: Mover bancos de dados do sistema | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- moving system databases
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- tempdb database [SQL Server], moving
- system databases [SQL Server], moving
- scheduled disk maintenace [SQL Server]
- moving databases
- msdb database [SQL Server], moving
- moving database files
- relocating database files
- planned database relocations [SQL Server]
- master database [SQL Server], moving
- model database [SQL Server], moving
- Resource database [SQL Server]
- databases [SQL Server], moving
ms.assetid: 72bb62ee-9602-4f71-be51-c466c1670878
author: stevestein
ms.author: sstein
ms.openlocfilehash: c9edfd5b460a6a6b80900e1beced674b80bfce93
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194993"
---
# <a name="move-system-databases"></a>Mover bancos de dados do sistema
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve como mover bancos de dados do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mover bancos de dados do sistema pode ser útil nas seguintes situações:  
  
-   Recuperação de falha. Por exemplo, o banco de dados está em modo de suspeição ou foi desligado devido a uma falha de hardware.  
  
-   Realocação planejada.  
  
-   Realocação para manutenção de disco programada.  
  
 Os procedimentos a seguir se aplicam para mover arquivos de banco de dados dentro da mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para mover um banco de dados para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para outro servidor, use as operações de [backup e restauração](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) .  

 Os procedimentos neste tópico exigem o nome lógico dos arquivos de banco de dados. Para obter o nome, consulte a coluna de nome na exibição de catálogo [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) .  
  
> [!IMPORTANT]  
>  Se você mover um banco de dados do sistema e, posteriormente, recriar o banco de dados mestre, será necessário mover o banco de dados do sistema novamente porque a operação de recriação instala todos os bancos de dados do sistema em seus locais padrão.  

> [!IMPORTANT]  
>  Após a movimentação dos arquivos, a conta de serviço do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] deve ter permissão para acessar os arquivos no novo local de pasta do arquivo.
    
  
##  <a name="planned-relocation-and-scheduled-disk-maintenance-procedure"></a><a name="Planned"></a> Realocação planejada e procedimento de manutenção de disco agendado  
 Para mover um arquivo de dados de um banco de dados do sistema ou arquivo de log como parte de uma realocação planejada ou operação de manutenção, execute as etapas a seguir. Este procedimento se aplica a todos os bancos de dados do sistema exceto os bancos de dados mestre e Recurso.  
  
1.  Para cada arquivo a ser movido, execute a seguinte instrução.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
2.  Pare a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou desligue o sistema para realizar a manutenção. Para obter mais informações, consulte [Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  Mova o arquivo ou os arquivos para o novo local.  

4.  Reinicialize a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o servidor. Para obter mais informações, consulte [Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
5.  Execute a consulta a seguir para verificar se houve alteração no arquivo.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
 Se o banco de dados msdb for movido e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para [Database Mail](../../relational-databases/database-mail/database-mail.md), execute estas etapas adicionais.  
  
1.  Verifique se o [!INCLUDE[ssSB](../../includes/sssb-md.md)] está habilitado para o banco de dados msdb executando a consulta a seguir.  
  
    ```  
    SELECT is_broker_enabled   
    FROM sys.databases  
    WHERE name = N'msdb';  
    ```  
  
     Para obter mais informações sobre como habilitar o [!INCLUDE[ssSB](../../includes/sssb-md.md)], veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
2.  Verifique se o Database Mail está funcionando, enviando um email de teste.  
  
##  <a name="failure-recovery-procedure"></a><a name="Failure"></a> Falha no procedimento de recuperação  
 Se um arquivo tiver de ser movido devido à falha de um hardware, siga estas etapas para realocar o arquivo para o novo local. Este procedimento se aplica a todos os bancos de dados do sistema exceto os bancos de dados mestre e Recurso.  
  
> [!IMPORTANT]  
>  Se o banco de dados não puder ser inicializado, significa que ele está em modo de suspeição ou em estado não recuperado, e apenas os membros de função fixa sysadmin podem mover o arquivo.  
  
1.  Interrompa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se tiver sido iniciado.  
  
2.  Inicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo somente recuperação mestre, inserindo um dos seguintes comandos no prompt de comando. Os parâmetros especificados nestes comandos diferenciam maiúsculas e minúsculas. Os comandos falham quando os parâmetros não são especificados como demonstrado.  
  
    -   Para a instância padrão (MSSQLSERVER), execute o seguinte comando:  
  
        ```  
        NET START MSSQLSERVER /f /T3608
        ```  
  
    -   Para uma instância nomeada, execute o seguinte comando:  
  
        ```  
        NET START MSSQL$instancename /f /T3608
        ```  
  
     Para obter mais informações, consulte [Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  Para cada arquivo a ser movido, use comandos **sqlcmd** ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para executar a instrução a seguir.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
     Para obter mais informações sobre como usar o utilitário **sqlcmd** , veja [Usar o Utilitário sqlcmd](../../ssms/scripting/sqlcmd-use-the-utility.md).  
  
4.  Saia do utilitário **sqlcmd** ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
5.  Pare a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, execute `NET STOP MSSQLSERVER`.  
  
6.  Mova o arquivo ou os arquivos para o novo local.  
  
7.  Reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, execute `NET START MSSQLSERVER`.  
  
8.  Execute a consulta a seguir para verificar se houve alteração no arquivo.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
##  <a name="moving-the-master-database"></a><a name="master"></a> Movendo o banco de dados mestre  
 Para mover o banco de dados mestre, siga estas etapas.  
  
1.  Pelo menu **Iniciar** , aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**, aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  No nó **Serviços do SQL Server** , clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, **SQL Server [MSSQLSERVER]** ) e escolha **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server (** _nome_instância_ **)** , clique na guia **Parâmetros de Inicialização** .  
  
4.  Na caixa **Parâmetros existentes**, selecione o parâmetro -d para mover o arquivo de dados mestre. Clique em **Atualizar** para salvar a alteração.  
  
     Na caixa **Especificar um parâmetro de inicialização** , altere o parâmetro para o novo caminho do banco de dados mestre.  
  
5.  Na caixa **Parâmetros existentes**, selecione o parâmetro -l para mover o arquivo de log mestre. Clique em **Atualizar** para salvar a alteração.  
  
     Na caixa **Especificar um parâmetro de inicialização** , altere o parâmetro para o novo caminho do banco de dados mestre.  
  
     O valor do parâmetro para o arquivo de dados deve seguir o parâmetro `-d` e o valor para o arquivo de log deve seguir o parâmetro `-l` . O exemplo a seguir mostra os valores de parâmetro da localização padrão do arquivo de dados mestre.  
  
     `-dC:\Program Files\Microsoft SQL Server\MSSQL<version>.MSSQLSERVER\MSSQL\DATA\master.mdf`  
  
     `-lC:\Program Files\Microsoft SQL Server\MSSQL<version>.MSSQLSERVER\MSSQL\DATA\mastlog.ldf`  
  
     Se a realocação planejada para o arquivo de dados mestre for `E:\SQLData`, os valores de parâmetros serão alterados da seguinte maneira:  
  
     `-dE:\SQLData\master.mdf`  
  
     `-lE:\SQLData\mastlog.ldf`  
  
6.  Interrompa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clicando com o botão direito do mouse no nome da instância e escolhendo **Interromper**.  
  
7.  Mova os arquivos do master.mdf e mastlog.ldf para o local novo.  
  
8.  Reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
9. Verifique a alteração do arquivo para o banco de dados mestre executando a consulta a seguir.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID('master');  
    GO  
    ```  

10. Neste ponto, o SQL Server deverá ser executado normalmente. Porém, a Microsoft também recomenda ajustar a entrada do Registro em `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\instance_ID\Setup`, em que *instance_ID* é como `MSSQL13.MSSQLSERVER`. Neste Hive, altere o valor `SQLDataRoot` para o novo caminho. Uma falha em atualizar o Registro poderá causar falha na atualização e aplicação de patch.

  
##  <a name="moving-the-resource-database"></a><a name="Resource"></a> Movendo o banco de dados de recursos  
 A localização do banco de dados de recursos é \<*drive*>:\Program Files\Microsoft SQL Server\MSSQL\<version>.\<*instance_name*>\MSSQL\Binn\\. O banco de dados não pode ser movido.  
  
##  <a name="follow-up-after-moving-all-system-databases"></a><a name="Follow"></a> Acompanhamento: depois de mover todos os bancos de dados do sistema  
 Se você moveu todos os bancos de dados do sistema para uma nova unidade ou volume ou para outro servidor com uma letra de unidade diferente, faça as atualizações a seguir.  
  
-   Altere o caminho do log do SQL Server Agent. Se você não atualizar este caminho, o SQL Server Agent não iniciará.  
  
-   Altere o local padrão do banco de dados. Criar um novo banco de dados pode falhar se a letra da unidade e do caminho especificados como a localização padrão não existir.  
  
#### <a name="change-the-sql-server-agent-log-path"></a>Altere o caminho do log do SQL Server Agent.  
  
1.  No SQL Server Management Studio, em Pesquisador de Objetos, expanda **SQL Server Agent**.  
  
2.  Clique com o botão direito do mouse em **Logs de Erros** e clique em **Configurar**.  
  
3.  Na caixa de diálogo **Configurar Logs de Erros do SQL Server Agent** , especifique o novo local do arquivo SQLAGENT.OUT. A localização padrão é C:\Program Files\Microsoft SQL Server\MSSQL\<version>.<nome_da_instância>\MSSQL\Log\\.  
  
#### <a name="change-the-database-default-location"></a>Altere o local padrão do banco de dados  
  
1.  No SQL Server Management Studio, em Pesquisador de Objetos, clique com o botão direito do mouse no servidor do SQL Server e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades do Servidor** da caixa de diálogo, selecione **Configurações de Banco de Dados**.  
  
3.  Em **Locais padrão de banco de dados**, navegue até o novo local para os arquivos de dados e log.  
  
4.  Pare e inicie o serviço do SQL Server para concluir a alteração.  
  
##  <a name="examples"></a><a name="Examples"></a> Exemplos  
  
### <a name="a-moving-the-tempdb-database"></a>a. Movendo o banco de dados tempdb  
 O seguinte exemplo move os arquivos de log e de dados `tempdb` para um novo local como parte de uma realocação planejada.  
  
> [!NOTE]  
>  Como o tempdb é recriado a cada vez que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada, você não precisa mover fisicamente os arquivos de log e de dados. Os arquivos são criados no local novo quando o serviço é reiniciado na etapa 3. Até que o serviço seja reiniciado, o tempdb continua usando os arquivos de dados e de log no local existente.  
  
1.  Determine os nomes de arquivo lógicos do banco de dados `tempdb` e o seu local atual no disco.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    GO  
    ```  
  
2.  Altere o local de cada arquivo usando `ALTER DATABASE`.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'F:\SQLLog\templog.ldf');  
    GO  
    ```  
  
3.  Pare e reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Verifique a alteração do arquivo.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    ```  
  
5.  Exclua os arquivos `tempdb.mdf` e `templog.ldf` do local original.  
  
## <a name="see-also"></a>Consulte Também  
 [Banco de dados de recursos](../../relational-databases/databases/resource-database.md)   
 [Banco de dados tempdb](../../relational-databases/databases/tempdb-database.md)   
 [Banco de dados mestre](../../relational-databases/databases/master-database.md)   
 [Banco de dados msdb](../../relational-databases/databases/msdb-database.md)   
 [Banco de dados modelo](../../relational-databases/databases/model-database.md)   
 [Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md)   
 [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)   
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Recompilar bancos de dados do sistema](../../relational-databases/databases/rebuild-system-databases.md)  
  
