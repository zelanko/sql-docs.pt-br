---
title: Criar um backup completo do banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4c750f4230cc83467cc5993d2a6ab571a06d2f5
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798027"
---
# <a name="create-a-full-database-backup-sql-server"></a>Create a Full Database Backup (SQL Server)
  Este tópico descreve como criar um backup de banco de dados completo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou PowerShell.  
  
> [!NOTE]  
>  Para obter informações sobre SQL Server Backup para o serviço de armazenamento de BLOBs do Azure, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para criar um backup de banco de dados completo usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A instrução BACKUP não é permitida em uma transação explícita ou implícita.  
  
-   Os backups criados por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para obter mais informações, veja [Backup Overview &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   À medida que um banco de dados aumenta, os backups completos de banco de dados levam mais tempo para serem concluídos e exigem mais espaço de armazenamento. Portanto, para um banco de dados grande, convém complementar um backup de banco de dados completo com uma série de *backups de bancos de dados diferenciais*. Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
-   Você pode estimar o tamanho de um backup de banco de dados completo usando o procedimento armazenado do sistema [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql).  
  
-   Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup do log com muita frequência, essas mensagens de êxito se acumularão muito rapidamente, resultando em logs de erros imensos que podem dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
###  <a name="Security"></a> Segurança  
 TRUSTWORTHY é definido como OFF em um backup de banco de dados. Para obter informações sobre como definir TRUSTWORTHY como ON, veja [Opções do ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], as opções `PASSWORD` e `MEDIAPASSWORD` foram descontinuadas para a criação de backups. Você ainda poderá restaurar os backups criados com senhas.  
  
####  <a name="Permissions"></a> Permissões  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
> [!NOTE]  
>  Ao especificar uma tarefa de backup usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) correspondente, clicando no botão **Script** e selecionando um destino para o script.  
  
#### <a name="to-back-up-a-database"></a>Para fazer o backup de um banco de dados  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  
  
4.  Na caixa de listagem `Database`, verifique o nome do banco de dados. Você pode, como opção, selecionar um banco de dados diferente da lista.  
  
5.  Você pode executar um backup de banco de dados para qualquer modelo de recuperação (**FULL**, **BULK_LOGGED** ou **SIMPLE**).  
  
6.  Na caixa de listagem **Tipo de backup** , selecione **Completo**.  
  
     Observe que depois de criar um backup de banco de dados completo, é possível criar um backup de banco de dados diferencial. Para obter mais informações, consulte [Criar um backup de banco de dados diferencial &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md).  
  
7.  Opcionalmente, você pode selecionar **Copiar Somente Backup** para criar um backup somente cópia. Um *backup somente cópia* é um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não depende da sequência de backups convencionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](copy-only-backups-sql-server.md).  
  
    > [!NOTE]  
    >  Quando a opção **Diferencial** está selecionada, você não pode criar um backup somente cópia.  
  
8.  Para **componente de backup**, clique em `Database`.  
  
9. Aceite o nome do conjunto de backup padrão sugerido na caixa de texto **Nome** ou digite um nome diferente para o conjunto de backup.  
  
10. Opcionalmente, na caixa de texto **Descrição** , digite uma descrição do conjunto de backup.  
  
11. Escolha o tipo do destino do backup e clique em **Disco**, **Fita** ou **URL**. Para selecionar os caminhos de até 64 unidades de disco ou fita que contêm um único conjunto de mídia, clique em **Adicionar**. Os caminhos selecionados são exibidos na caixa de listagem **Backup** .  
  
     Para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup, selecione-o e clique em **Conteúdo**.  
  
12. Para exibir ou selecionar as opções de mídia, clique em **Opções de Mídia** no painel **Selecionar uma página** .  
  
13. Selecione uma opção **Substituir Mídia** , com um clique em uma das opções a seguir:  
  
    -   **Fazer backup no conjunto de mídias existente**  
  
         Para essa opção, clique em **Anexar ao conjunto de backup existente** ou **Substituir todos os conjuntos de backup existentes**. Para obter mais informações, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, selecione **Verificar nome do conjunto de mídias e validade do conjunto de backup** para que a operação de backup verifique a data e a hora em que o conjunto de mídias e de backup expiram.  
  
         Como opção, digite um nome na caixa de texto **Nome do conjunto de mídias** . Se nenhum nome for especificado, um conjunto de mídias com um nome em branco será criado. Se você especificar um nome de conjunto de mídias, a mídia (fita ou disco) é verificada para ver se o nome real corresponde ao nome digitado.  
  
        > [!IMPORTANT]  
        >  Essa opção será desabilitada se a opção **URL** for selecionada como o destino de backup na página **General** . Para saber mais, confira [Fazer backup do banco de dados &#40;página Opções de Mídia&#41;](back-up-database-media-options-page.md)  
        >   
        >  Se você planeja usar criptografia, não selecione essa opção. Se você selecionar esta opção, as opções de criptografia na página **Opções de Backup** serão desabilitadas. A criptografia não tem suporte ao anexar ao conjunto de backup existente.  
  
    -   **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**  
  
         Para essa opção, digite um nome na caixa de texto **Nome do novo conjunto de mídias** e, opcionalmente, descreva o conjunto de mídias na caixa de texto **Descrição do novo conjunto de mídias** .  
  
        > [!IMPORTANT]  
        >  Essa opção será desabilitada se a opção **URL** for selecionada na página **General** . Não há suporte para essas ações durante o backup no armazenamento do Azure.  
  
14. Na seção **Confiabilidade** , como opção, marque:  
  
    -   **Verificar backup quando concluído**  
  
    -   **Executar soma de verificação antes de gravar na mídia**e, como opção, **Continuar com erro da soma de verificação**. Para obter informações sobre somas de verificação, veja [Erros de mídia possíveis durante backup e restauração &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
15. Se o backup estiver sendo feito em uma unidade de fita (conforme especificado na seção **Destino** da página **Geral**), a opção **Descarregar a fita após o backup** estará ativa. Clicar nessa opção ativa a opção **Rebobinar a fita antes de descarregar** .  
  
    > [!NOTE]  
    >  As opções na seção **Log de transações** estarão inativos exceto se o backup estiver sendo feito em um log de transações (como especificado na seção **Tipo de backup** da página **Geral** ).  
  
16. Para exibir ou selecionar as opções de backup, clique em **Opções de Backup** no painel **Selecionar uma página** .  
  
17. Especifique quando o conjunto de backup irá expirar e pode ser substituído sem ignorar explicitamente a verificação dos dados de expiração:  
  
    -   Para que o conjunto de backup expire depois de um número específico de dias, clique em **Depois** (a opção padrão) e digite quantos dias depois da criação do conjunto ele deve expirar. Esse valor pode ser de 0 a 99999 dias; 0 dia significa que o conjunto de backup nunca vai expirar.  
  
         O valor padrão é definido na opção **Retenção de mídia de backup padrão (em dias)** da caixa de diálogo **Propriedades do Servidor** (página Configurações do Banco de Dados). Para acessar, clique com o botão direito do mouse no nome do servidor em Pesquisador de Objetos e selecione propriedades. Depois, selecione a página **Configurações de Banco de Dados** .  
  
    -   Para que o conjunto de backup expire em uma data específica, clique no campo **Em**e digite a data de expiração do conjunto.  
  
         Para obter mais informações sobre datas de validade de backup, consulte [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
18. [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] e posteriores dão suporte para [compactação de backup](backup-compression-sql-server.md). Por padrão, a compactação de um backup depende do valor da opção de configuração de servidor **padrão de compactação de backup** . Porém, independentemente do padrão atual do nível do servidor, é possível compactar um backup, marcando a opção **Compactar backup** e evitar a compactação marcando **Não compactar o backup**.  
  
     **Para exibir ou alterar o padrão de compactação de backup atual**  
  
    -   [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
19. Especifique se a criptografia deve ser usada para o backup. Selecione um algoritmo de criptografia a ser usado na etapa de criptografia e forneça um Certificado ou uma Chave assimétrica de uma lista de certificados ou chaves assimétricas existentes. A criptografia tem suporte no SQL Server 2014 ou posterior. Para obter mais detalhes sobre as opções de criptografia, consulte [Fazer backup do banco de dados &#40;página Opções de Backup&#41;](back-up-database-backup-options-page.md).  
  
> [!NOTE]  
>  Alternativamente, é possível usar o Assistente de Plano de Manutenção para criar backups de bancos de dados.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-create-a-full-database-backup"></a>Para criar um backup de banco de dados completo  
  
1.  Execute a instrução BACKUP DATABASE para criar o backup do banco de dados completo, especificando:  
  
    -   O nome do banco de dados do qual fazer backup.  
  
    -   O dispositivo de backup em que o backup completo do banco de dados será gravado.  
  
     A sintaxe básica [!INCLUDE[tsql](../../includes/tsql-md.md)] para o backup de banco de dados completo é:  
  
     BACKUP DATABASE *database*  
  
     TO *backup_device* [ **,** ...*n* ]  
  
     [ WITH *com_opções* [ **,** ...*o* ] ] ;  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |*database*|É o banco de dados do qual fazer backup.|  
    |*backup_device* [ **,** ...*n* ]|Especifica uma lista de 1 a 64 dispositivos de backup a serem usados para a operação de backup. Você pode especificar um dispositivo de backup físico ou pode especificar um dispositivo de backup lógico correspondente, se já definido. Para especificar um dispositivo de backup físico, use a opção DISK ou TAPE:<br /><br /> { DISK &#124; TAPE } **=** _physical_backup_device_name_<br /><br /> Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md).|  
    |WITH *with_options* [ **,** ...*o* ]|Opcionalmente, especifica uma ou mais opções adicionais, *o*. Para obter informações sobre os fundamentos de opções, consulte a etapa 2.|  
  
2.  Opcionalmente, especifique uma ou mais opções WITH. Algumas opções WITH básicas são descritas aqui. Para obter informações sobre todas as opções WITH, consulte [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
    -   Opções WITH do conjunto de backup básico:  
  
         { COMPRESSION | NO_COMPRESSION }  
         No [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] e versões posteriores somente, especifica se [compressão de backup](backup-compression-sql-server.md) é executada neste backup, substituindo o padrão de nível de servidor.  
  
         ENCRYPTION (ALGORITHM, SERVER CERTIFICATE |ASYMMETRIC KEY)  
         No SQL Server 2014 ou em versões posteriores somente, especifique o algoritmo de criptografia a ser usado, e o certificado ou chave assimétrica usada para proteger a criptografia.  
  
         Descrição **=** { **' *`text`* '**  |  **@** _text_variable_ }  
         Especifica o texto de forma livre que descreve o conjunto de backup. A cadeia de caracteres pode conter um máximo de 255 caracteres.  
  
         NAME **=** { *backup_set_name* |  **@** _backup_set_name_var_ }  
         Especifica o nome do conjunto de backup. Os nomes podem ter no máximo de 128 caracteres. Se NAME não estiver especificado, ele estará em branco.  
  
    -   Opções WITH do conjunto de backup básico:  
  
         Por padrão, BACKUP anexa o backup a um conjunto de mídias existente, preservando conjuntos de backup existentes. Para especificar isso explicitamente, use a opção NOINIT. Para obter informações sobre o acréscimo a conjuntos de backup existentes, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Alternativamente, para formatar a mídia de backup, use a opção FORMAT:  
  
         FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media_name_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text_variable_ } ]  
         Use a cláusula FORMAT quando estiver usando a mídia pela primeira vez ou quando quiser sobrescrever todos os dados existentes Opcionalmente, atribua à nova mídia um nome e uma descrição.  
  
        > [!IMPORTANT]  
        >  Tenha muito cuidado ao usar a cláusula FORMAT ou a instrução BACKUP, pois isso destrói qualquer backup previamente armazenado na mídia de backup.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
  
#### <a name="a-backing-up-to-a-disk-device"></a>A. Fazendo backup para um dispositivo de disco.  
 O exemplo a seguir faz backup de banco de dados completo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] em um disco, usando `FORMAT` para criar um novo conjunto de mídia.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-backing-up-to-a-tape-device"></a>B. Fazendo backup para um dispositivo de fita  
 O exemplo a seguir faz backup do banco de dados completo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]em fita, anexando o backup aos backups anteriores.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-backing-up-to-a-logical-tape-device"></a>C. Fazendo backup em um dispositivo de fita lógico  
 O exemplo a seguir cria um dispositivo de backup lógico para uma unidade de fita. O exemplo faz backup completo do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nesse dispositivo.  
  
```sql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
  
1.  Use o cmdlet `Backup-SqlDatabase`. Para indicar explicitamente que se trata de um backup de banco de dados completo, especifique o parâmetro **-BackupAction** com seu valor padrão, `Database`. Esse parâmetro é opcional para backups completos de banco de dados.  
  
     O exemplo a seguir cria um backup de banco de dados completo do banco de dados `MyDB` para o local de backup padrão da instância de servidor `Computer\Instance`. Como opção, esse exemplo especifica `-BackupAction Database`.  
  
    ```powershell
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
    ```  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Fazer backup de um banco de dados (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Restaurar um backup &#40;de banco de dados SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar um backup de banco de dados no modelo de recuperação simples &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Usar o Assistente de Plano de Manutenção](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Fazer backup do banco de dados &#40;página Geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [Fazer backup do banco de dados &#40;página Opções de Backup&#41;](back-up-database-backup-options-page.md)   
 [Backups diferenciais &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Backups de bancos de dados completos &#40;SQL Server&#41;](full-database-backups-sql-server.md)  
