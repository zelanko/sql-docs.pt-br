---
title: Fazer backup de arquivos e grupos de arquivos (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up filegroups [SQL Server]
- file backups [SQL Server], how-to topics
- backing up files [SQL Server]
- backups [SQL Server], creating
- filegroups [SQL Server], backing up
ms.assetid: a0d3a567-7d8b-4cfe-a505-d197b9a51f70
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 34d2c923e509422ee4a45abe2132b06362efa1ee
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="back-up-files-and-filegroups-sql-server"></a>Fazer backup de arquivos e de grupos de arquivos (SQL Server)
  Este tópico descreve como fazer backup de arquivos e grupos de arquivos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou PowerShell. Quando o tamanho de banco de dados e exigências de desempenho tornarem um backup de banco de dados completo impraticável, então você poderá criar um backup de arquivo. Um *backup de arquivo* contém todos os dados em um ou mais arquivos (ou grupos de arquivos). Para obter mais informações sobre backups de arquivos, veja [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) e [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A instrução BACKUP não é permitida em uma transação explícita ou implícita.  
  
-   No modelo de recuperação simples, o backup deve ser feito em todos os arquivos de leitura/gravação juntos. Isso ajuda a assegurar que o banco de dados possa ser restaurado até um momento determinado consistente. Em vez de especificar cada arquivo ou grupo de arquivos de leitura/gravação individualmente, use a opção de READ_WRITE_FILEGROUPS. Esta opção efetua backup de todos os grupos de arquivos de leitura/gravação no banco de dados. Um backup que é criado especificando READ_WRITE_FILEGROUPS é conhecido como um *backup parcial*. Para obter mais informações, veja [Backups parciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
-   Para obter mais informações sobre limitações e restrições, veja [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup do log com muita frequência, essas mensagens de êxito serão acumuladas muito rapidamente, resultando em logs de erros imensos que podem dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
 
##  <a name="Permissions"></a> Permissões  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
  
## <a name="back-up-files-and-filegroups-using-ssms"></a>Fazer backup de arquivos e grupos de arquivos usando o SSMS   
  
1.  Depois de conectar-se à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objeto, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  
  
4.  Na lista **Banco de Dados** , verifique o nome do banco de dados. Você pode, como opção, selecionar um banco de dados diferente da lista.  
  
5.  Na lista **Tipo de backup** , selecione **Completo** ou **Diferencial**.  
  
6.  Para a opção **Componente de backup** , clique em **Arquivo e Grupos de Arquivo**.  
  
7.  Na caixa de diálogo **Selecionar Arquivos e Grupos de Arquivos** , selecione os arquivos e os grupos de arquivos a serem incluídos no backup. É possível selecionar um ou mais arquivos individuais ou marcar a caixa para um grupo de arquivos para selecionar automaticamente todos os arquivos nesse grupo.  
  
8.  Aceite o nome do conjunto de backup padrão sugerido na caixa de texto **Nome** ou digite um nome diferente para o conjunto de backup.  
  
9. Opcionalmente, na caixa de texto **Descrição** , digite uma descrição do conjunto de backup.  
  
10. Especifique quando o conjunto de backup irá expirar:  
  
    -   Para que o conjunto de backup expire após um número específico de dias, clique em **Após** (a opção padrão). Em seguida, insira o número de dias (a partir da criação do conjunto) após o qual o conjunto irá expirar. Esse valor pode ser de 0 a 99999 dias; 0 dia significa que o conjunto de backup nunca vai expirar.  
  
         O valor padrão é definido na opção **Retenção de mídia de backup padrão (em dias)** da caixa de diálogo **Propriedades do Servidor** (página**Configurações do Banco de Dados** ). Para acessar essa opção, clique com o botão direito do mouse no nome do servidor no Pesquisador de Objetos, selecione propriedades e a página **Configurações do Banco de Dados** .  
  
    -   Para que o conjunto de backup expire em uma data específica, clique no campo **Em**e digite a data de expiração do conjunto.  
  
11. Escolha o tipo do destino de backup clicando em **Disco** ou **Fita**. Para selecionar os caminhos de até 64 unidades de disco ou fita que contêm um único conjunto de mídias, clique em **Adicionar**. Os caminhos selecionados são exibidos na lista **Fazer backup em** .  
  
    >**OBSERVAÇÃO:** para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup, selecione-o e clique em **Conteúdo**.  
  
12. Para exibir ou selecionar as opções avançadas, clique em **Opções** no painel **Selecionar uma página** .  
  
13. Selecione uma opção **Substituir Mídia** , com um clique em uma das opções a seguir:  
  
    -   **Fazer backup no conjunto de mídias existente**  
  
         Para essa opção, clique em **Anexar ao conjunto de backup existente** ou **Substituir todos os conjuntos de backup existentes**. Para obter informações sobre como fazer backup de um conjunto de mídias existente, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, selecione **Verificar nome do conjunto de mídias e validade do conjunto de backup** para que a operação de backup verifique a data e a hora em que o conjunto de mídias e de backup expiram.  
  
         Como opção, digite um nome na caixa de texto **Nome do conjunto de mídias** . Se nenhum nome for especificado, um conjunto de mídias com um nome em branco será criado. Se você especificar um nome do conjunto de mídias, a mídia (fita ou disco) será verificada para conferir se o nome real corresponde ao nome inserido aqui.  
  
         Se você deixar o nome da mídia em branco e marcar a caixa para verificar a mídia, a verificação terá sucesso se o nome da mídia também estiver em branco na mídia.  
  
    -   **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**  
  
         Para essa opção, digite um nome na caixa de texto **Nome do novo conjunto de mídias** e, opcionalmente, descreva o conjunto de mídias na caixa de texto **Descrição do novo conjunto de mídias** . Para obter mais informações sobre como criar um novo conjunto de mídias, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
14. Na seção **Confiabilidade** , como opção, marque:  
  
    -   **Verificar backup quando concluído**  
  
    -   **Executar soma de verificação antes de gravar na mídia**e, como opção, **Continuar com erro da soma de verificação**. Para obter mais informações sobre somas de verificação, veja [Erros de mídia possíveis durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
15. Se o backup estiver sendo feito em uma unidade de fita (conforme especificado na seção **Destino** da página **Geral**), a opção **Descarregar a fita após o backup** estará ativa. O clique nessa opção habilita a opção **Rebobinar a fita antes de descarregar** .  
  
    > **OBSERVAÇÃO:** as opções na seção **Log de transações** estarão inativas exceto se o backup estiver sendo feito em um log de transações (como especificado na seção **Tipo de backup** da página **Geral** ).  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versões posteriores dão suporte à [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Por padrão, a compactação de um backup depende do valor da opção de configuração de servidor **padrão de compactação de backup** . Porém, independentemente do padrão atual do nível do servidor, é possível compactar um backup, marcando a opção **Compactar backup**e evitar a compactação marcando **Não compactar o backup**.  
  
     **Para exibir o padrão de compactação de backup atual**  
  
    -   [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
  
## <a name="back-up-files-and-filegroups-using-t-sql"></a>Fazer backup de arquivos e grupos de arquivos usando o T-SQL
  
1.  Para criar um backup de arquivo ou grupo de arquivos, use a instrução [BACKUP DATABASE <file_or_filegroup>](../../t-sql/statements/backup-transact-sql.md). Minimamente, essa instrução deve especificar o seguinte:  
  
    -   Nome do banco de dados.  
  
    -   Uma cláusula FILE ou FILEGROUP para cada arquivo ou grupo de arquivos, respectivamente.  
  
    -   O dispositivo de backup em que o backup completo será gravado.  
  
     A sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] básica para um backup de arquivo é:  
  
     BACKUP DATABASE *database*  
  
     { FILE **=***logical_file_name* | FILEGROUP **=***logical_filegroup_name* } [ **,**...*f* ]  
  
     TO *backup_device* [ **,**...*n* ]  
  
     [ WITH *com_opções* [ **,**...*o* ] ] ;  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |*database*|É o banco de dados do qual é feito o backup do log de transações, do banco de dados parcial ou do banco de dados completo.|  
    |FILE **=***logical_file_name*|Especifica o nome lógico de um arquivo a ser incluído no backup de arquivos.|  
    |FILEGROUP **=***logical_filegroup_name*|Especifica o nome lógico de um grupo de arquivos que será incluído no backup de arquivos. No modelo de recuperação simples, um backup de grupo de arquivos é permitido apenas para grupos de arquivos somente leitura.|  
    |[ **,**...*f* ]|É um espaço reservado que indica que vários arquivos e grupos de arquivos podem ser especificados. O número de arquivos ou grupos de arquivos é ilimitado.|  
    |*backup_device* [ **,**...*n* ]|Especifica uma lista de 1 a 64 dispositivos de backup a serem usados para a operação de backup. Você pode especificar um dispositivo de backup físico ou pode especificar um dispositivo de backup lógico correspondente, se já definido. Para especificar um dispositivo de backup físico, use a opção DISK ou TAPE:<br /><br /> { DISK &#124; TAPE } **=***physical_backup_device_name*<br /><br /> Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|  
    |WITH *with_options* [ **,**...*o* ]|Opcionalmente, especifica uma ou mais opções adicionais, como DIFFERENTIAL.<br /><br /> Observação: um backup de arquivo diferencial exige um backup de arquivo completo como base. Para obter mais informações, veja [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).|  
  
2.  No modelo de recuperação completa, você deverá também efetuar backup do log de transações. Para usar um conjunto inteiro de backups de arquivo completos para restaurar um banco de dados, você deverá também ter suficientes backups de log para abranger todos os backups de arquivo, desde o início do primeiro backup de arquivo. Para obter mais informações, veja [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Os exemplos seguintes fazem backup de um ou mais arquivos dos grupos de arquivos secundários do banco de dados `Sales` . Esse banco de dados usa o modelo de recuperação completa e contém os seguintes grupos de arquivos secundários:  
  
-   Um grupo de arquivo nomeado `SalesGroup1` que tem os arquivos `SGrp1Fi1` e `SGrp1Fi2`.  
  
-   Um grupo de arquivo nomeado `SalesGroup2` que tem os arquivos `SGrp2Fi1` e `SGrp2Fi2`.  
  
#### <a name="a-create-a-file-backup-of-two-files"></a>A. Criar um backup de arquivo de dois arquivos  
 O exemplo a seguir cria um backup diferencial de arquivo só do arquivo `SGrp1Fi2` do `SalesGroup1` e o arquivo `SGrp2Fi2` do grupo de arquivos `SalesGroup2` .  
  
```tsql  
--Backup the files in the SalesGroup1 secondary filegroup.  
BACKUP DATABASE Sales  
   FILE = 'SGrp1Fi2',   
   FILE = 'SGrp2Fi2'   
   TO DISK = 'G:\SQL Server Backups\Sales\SalesGroup1.bck';  
GO  
```  
  
#### <a name="b-create-a-full-file-backup-of-the-secondary-filegroups"></a>B. Criar um backup completo de arquivos dos grupos de arquivos secundários  
 O exemplo a seguir cria um backup de arquivo completo de todos os arquivos dos dois grupos de arquivos secundários.  
  
```tsql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck';  
GO  
```  
  
#### <a name="c-create-a-differential-file-backup-of-the-secondary-filegroups"></a>C. Criar um backup diferencial de arquivos dos grupos de arquivos secundários  
 O exemplo a seguir cria um backup diferencial de cada arquivo nos dois grupos de arquivos secundários.  
  
```tsql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
  
1.  Use o cmdlet **Backup-SqlDatabase** e especifique **Files** como valor do parâmetro **-BackupAction** . Além disso, especifique um dos seguintes parâmetros:  
  
    -   Para fazer backup de um arquivo específico, especifique o parâmetro **-DatabaseFile***String* , em que *String* contém um ou mais arquivos de banco de dados para fazer backup.  
  
    -   Para fazer backup de todos os arquivos de determinado grupo de arquivos, especifique o parâmetro **-DatabaseFileGroup***String* , em que *String* contém um ou mais grupos de arquivos de banco de dados para fazer backup.  
  
     O exemplo a seguir cria um backup de arquivo completo de todos os arquivos dos grupos de arquivos secundários 'FileGroup1' e 'FileGroup2' no banco de dados `MyDB` . Os backups são criados no local de backup padrão da instância do servidor `Computer\Instance`.  
  
    ```  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Files -DatabaseFileGroup "FileGroup1","FileGroup2"  
    ```  
  
 **Configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Informações de histórico e cabeçalho de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [Fazer backup do banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [Fazer backup do banco de dados &#40;página Opções de Backup&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [Backups completos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
  
  

