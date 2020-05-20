---
title: Monitorar SQL Server Backup gerenciado no Azure | Microsoft Docs
description: Este artigo descreve as ferramentas que você pode usar para determinar a integridade geral dos backups usando SQL Server Backup gerenciado para o Azure e identificar erros.
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: cfb9e431-7d4c-457c-b090-6f2528b2f315
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4ed32927e38f67c718031930023bd246048e2db5
ms.sourcegitcommit: 553d5b21bb4bf27e232b3af5cbdb80c3dcf24546
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2020
ms.locfileid: "82849604"
---
# <a name="monitor-sql-server-managed-backup-to-azure"></a>Monitorar o backup gerenciado do SQL Server para Azure
  O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tem medidas internas para identificar problemas e erros durante processos de backup e adotar uma ação corretiva quando possível.  No entanto, há determinadas situações onde a intervenção do usuário é necessária. Este tópico descreve as ferramentas que você pode usar para determinar o estado de integridade geral dos backups e identifica todos os erros que precisam ser resolvidos.  
  
## <a name="overview-of-ss_smartbackup-built-in-debugging"></a>Visão geral de depuração interna do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] examina periodicamente backups agendados e tenta reagendar todos os backups com falha. Ele pesquisa a conta de armazenamento periodicamente para identificar interrupções nas cadeias de logs que afetam a capacidade de recuperação do banco de dados e agenda backups novos apropriadamente. Ele também leva em conta as políticas de limitação do Azure e tem mecanismos em vigor para gerenciar vários backups de banco de dados. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usa eventos estendidos para rastrear toda a atividade. Os canais de Evento Estendido usados pelo agente [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] incluem Administração, Operacional, Analítico e Depuração. Os eventos que entram na categoria Admin geralmente estão relacionados a erros, requerem intervenção do usuário e são habilitados por padrão. Os eventos analíticos são ativados também por padrão, mas geralmente não relacionados aos erros que requerem intervenção do usuário. Os eventos operacionais normalmente são informativos. Por exemplo, os eventos operacionais incluem o agendamento de um backup, uma conclusão bem-sucedida do backup, etc. A depuração é a mais detalhada e é usada internamente pelo [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para determinar problemas e corrigi-los, se necessário.  
  
### <a name="configure-monitoring-parameters-for-ss_smartbackup"></a>Configurar parâmetros de monitoramento para o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 O procedimento armazenado do sistema **smart_admin. sp_set_parameter** permite que você especifique as configurações de monitoramento. As seções a seguir mostram o processo de habilitar Eventos Estendidos e habilitar a notificação por email sobre erros e avisos.  
  
 A função **smart_admin. fn_get_parameter** pode ser usada para obter a configuração atual de um parâmetro específico ou de todos os parâmetros configurados. Se os parâmetros nunca tiverem sido configurados, a função não retornará nenhum valor.  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Isso retornará a configuração atual de Eventos Estendidos e notificações por email.  
  
```sql
Use msdb  
Go  
SELECT * FROM smart_admin.fn_get_parameter (NULL)  
GO  
```  
  
 Para obter mais informações, consulte [smart_admin. fn_get_parameter &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)  
  
### <a name="extended-events-for-monitoring"></a>Eventos Estendidos para monitoramento  
 Por padrão, os eventos Admin, Operacional e Analítico estão ativados. Os eventos Admin são mais críticos, úteis para identificar erros que requerem intervenção manual para resolver o problema. Talvez seja necessário ativar os eventos operacional e de depuração, mas considere que esses eventos são detalhados e podem requerer filtragem. Os procedimentos a seguir descrevem como monitorar eventos registrados em log com Eventos Estendidos.  
  
> [!IMPORTANT]  
>  Diferente dos Eventos Estendidos do SQL engine, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] não oferece suporte a conceitos de sessão de Evento Estendido. As funções e os procedimentos armazenados do sistema são as ferramentas usadas para interagir com eventos estendidos. Você também pode exibir o log de eventos estendidos do diretório de log.  
  
##### <a name="to-configure-and-view-extended-events"></a>Para configurar e exibir Eventos Estendidos  
  
1.  Para exibir os canais de Evento Estendido disponíveis e seu status atual executando a seguinte consulta:  
  
    ```sql
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     A saída desta consulta exibirá o event_name, quer seja configurável ou não, e se estiver habilitado no momento.  Para obter mais informações, consulte [smart_admin. fn_get_current_xevent_settings &#40;&#41;do Transact-SQL ](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql).  
  
2.  Para habilitar eventos de depuração, execute a seguinte consulta:  
  
    ```sql
    --  to enable debug events  
    Use msdb;  
    GO 
    EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
     Para obter mais informações sobre o procedimento armazenado, consulte [smart_admin. sp_set_parameter &#40;&#41;do Transact-SQL ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql).  
  
3.  Para exibir os eventos em log, execute esta consulta:  
  
    ```sql
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;
    ```  
  
    ```sql
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'
    ```  
  
### <a name="aggregated-error-countshealth-status"></a>Contagens de erros agregadas/Status de integridade  
 A função **smart_admin. fn_get_health_status** retorna uma tabela de contagens de erros agregados para cada categoria que pode ser usada para monitorar o status de integridade de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] . Essa mesma função também é usada pelo mecanismo de notificação por email configurado pelo sistema descrito mais adiante neste tópico.   
Essas contagens agregadas podem ser usadas para monitorar a integridade do sistema. Por exemplo, se a coluna number_ of_retention_loops for 0 em 30 minutos, pode ser que o gerenciamento de retenção esteja demorando ou talvez nem esteja funcionando corretamente. As colunas diferentes de zero do erro podem indicar problemas e os logs de Eventos Estendidos devem ser verificados para descobrir o problema. Como alternativa, chame **smart_admin. sp_get_backup_diagnostics** procedimento armazenado para encontrar os detalhes do erro.  
  
### <a name="using-agent-notification-for-assessing-backup-status-and-health"></a>Usando a notificação do agente para avaliar o status e a integridade do backup  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] inclui um mecanismo de notificação baseado nas políticas de gerenciamento baseado em políticas do SQL Server.  
  
 **Pré-requisitos:**  
  
-   O Database Mail é necessário para usar essa funcionalidade. Para obter mais informações, sobre como habilitar o BD mail para a instância do SQL Server, consulte [configurar Database Mail](../relational-databases/database-mail/configure-database-mail.md).  
  
-   As propriedades do Sistema de Alerta do SQL Server Agent devem estar definidas para usar o Database Mail.  
  
 **Arquitetura de notificação:**  
  
-   **Gerenciamento baseado em políticas:** Duas políticas são definidas para monitorar a integridade do backup: **política de integridade do sistema de administração inteligente**e **política de integridade da ação do usuário do administrador inteligente**. A Política de Integridade do Sistema do Smart Admin avalia os erros críticos, como a falta de Credenciais do SQL ou credenciais desse tipo inválidas e os erros de conectividade e relata a integridade do sistema. Esses normalmente requerem uma ação manual para corrigir o problema subjacente. A Política de Integridade de Ação do Usuário do Smart Admin avalia os avisos, como backups corrompidos e itens semelhantes.  Talvez eles não exijam nenhuma ação, mas apenas um aviso de um evento. Espera-se que esses problemas sejam resolvidos automaticamente pelo agente [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
-   **SQL Server Agent** Trabalho: a notificação é executada usando um trabalho SQL Server Agent que tem três etapas de trabalho. Na primeira etapa do trabalho, ele detecta se o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está configurado para um banco de dados ou instância. Se ele encontrar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado e configurado, executará a segunda etapa: um cmdlet do PowerShell que avalia o status de integridade examinando as políticas de gerenciamento baseado em políticas do SQL Server. Se ele encontrar um erro ou aviso, ocorrerá uma falha, que disparará a terceira etapa, que é enviar uma notificação por email com o relatório de erro/aviso.  No entanto, esse trabalho do SQL Server Agent não está habilitado por padrão. Para habilitar o trabalho de notificação por email, use o procedimento armazenado do sistema **smart_admin. sp_set_backup_parameter** .  O procedimento a seguir descreve as etapas com mais detalhes:  
  
##### <a name="enabling-email-notification"></a>Habilitando a notificação por email  
  
1.  Se Database Mail ainda não estiver configurado, use as etapas descritas em [configurar Database Mail](../relational-databases/database-mail/configure-database-mail.md).  
  
2.  Definir banco de dados como o sistema de email para SQL Server sistema de alertas: clique com o botão direito do mouse em **SQL Server Agent**, selecione **sistema de alerta**, marque a caixa **habilitar perfil de email** , selecione **Database Mail** como o **sistema de email**e selecione um perfil de email criado anteriormente.  
  
3.  Execute a consulta a seguir em uma janela de consulta e forneça o endereço de email para o qual você deseja que a notificação seja enviada:  
  
    ```sql
    Use msdb  
    Go  
    EXEC smart_admin.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'
    ```  
  
     Isso cria um trabalho do SQL Server Agent que é usado para coletar o status de integridade e enviar notificações quando ocorre um erro ou um problema com os backups.  
  
 A seguir é mostrado um exemplo de script para habilitar o DB Mail e para configurar notificação por email através do Trabalho do SQL Server Agent  
  
```sql
-- Prereq: Make sure that SQL Server service runs in a service account that has  
--  access to SMTP Server   
-- set SQL Server service account as domain account   
  
EXEC sp_configure 'show advanced', 1  
RECONFIGURE  
GO  
  
-- Enable DBMail  
EXEC sp_configure 'Database Mail XPs',1  
GO  
RECONFIGURE  
GO  
  
-- Configure DBMail  
DECLARE @emailid NVARCHAR(255)  
-- Note: change this email to your own email id  
SET @emailid = N'emailalias@mycompany.com'  
  
DECLARE @smtpserver NVARCHAR(255)  
SET @smtpserver = N'smtphost.domainname.com'  
  
DECLARE @mailprofile NVARCHAR(255)  
SET @mailprofile = N'my_profile'  
  
EXEC msdb.dbo.sysmail_add_account_sp @account_name=N'myaccount',  
                @email_address = @emailid,  
                @replyto_address = @emailid,  
                @mailserver_name = @smtpserver,  
                @use_default_credentials = 1  
  
EXEC msdb.dbo.sysmail_add_profile_sp @profile_name=@mailprofile  
EXEC msdb.dbo.sysmail_add_profileaccount_sp @profile_name=@mailprofile, @account_name=N'myaccount', @sequence_number=1  
  
-- Set SQL Agent to use DBMail profile  
EXEC msdb.dbo.sp_set_sqlagent_properties @databasemail_profile = @mailprofile  
  
-- Configure Notifications   
EXEC msdb.smart_admin.sp_set_parameter  
@parameter_name = 'SSMBackup2WANotificationEmailIds',  
@parameter_value = @emailid  
  
-- To test is you are receiving notifications  
-- delete few backup files from your storage container, Wait for 15 minutes & see if you get any email notification
```  
  
### <a name="using-powershell-to-setup-custom-health-monitoring"></a>Usando o PowerShell para configurar o monitoramento de integridade personalizado  
 O cmdlet **Test-SqlSmartAdmin** pode ser usado para criar o monitoramento de integridade personalizado. Por exemplo, a opção de notificação descrita na seção anterior pode ser configurada no nível da instância.  Se você tiver várias instâncias do SQL Server configuradas para usar o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], o cmdlet do PowerShell poderá ser usado para criar scripts ao coletar o status e a integridade dos backups de todas as instâncias.  
  
 O cmdlet **Test-SqlSmartAdmin** avalia os erros e avisos retornados pelo SQL Server políticas de gerenciamento baseado em políticas e relata um status acumulado.  Por padrão, esse cmdlet usa as políticas do sistema. Para incluir qualquer política personalizada, use o parâmetro `-AllowUserPolicies`.  
  
 A seguir é mostrado um exemplo de script PowerShell que retorna um relatório de erros e avisos com base nas políticas do sistema e qualquer política de usuário criada:  
  
```powershell
$policyResults = Get-SqlSmartAdmin | Test-SqlSmartAdmin -AllowUserPolicies  
$policyResults.PolicyEvaluationDetails | Select Name, Category, Expression, Result, Exception | fl
```  
  
 O script a seguir retorna um relatório detalhado dos erros e avisos para a instância padrão ( `\SQL\COMPUTER\DEFAULT` ):  
  
```powershell
(Get-SqlSmartAdmin ).EnumHealthStatus()  
```  
  
### <a name="objects-in-msdb-database"></a>Objetos em um banco de dados MSDB  
 Há objetos que são instalados para implementar a funcionalidade. Esses objetos são reservados para uso interno. Porém, há uma tabela do sistema que pode ser útil para monitorar o status do backup: smart_backup_files. A maioria das informações armazenadas nesta tabela é relevante para o monitoramento como o tipo de backup, nome do banco de dados, primeiro e último LSN, as datas de expiração de backup são expostas por meio da função do sistema [smart_admin. fn_available_backups &#40;&#41;do Transact-SQL ](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql). Embora a coluna de status na tabela smart_backup_files que indica o status do arquivo de backup não esteja disponível por meio da função. O seguinte é um exemplo de consulta que você pode usar para recuperar algumas informações que incluem o status da tabela do sistema:  
  
```sql
USE msdb  
GO  
SELECT  
 database_name AS [Database Name] ,backup_path AS [Backup Destination and File]  
,[Backup Type] =  
CASE backup_type  
WHEN 1 THEN 'FULL'  
WHEN 2 THEN 'LOG'  
END  
,[Backup Status] =  
CASE [status]  
WHEN 'A' THEN 'Available'  
WHEN 'B' THEN 'Copy In Progress'  
WHEN 'C' THEN 'Corrupted'  
WHEN 'D' THEN 'Deleted'  
WHEN 'F' THEN 'Copy Failed'  
WHEN 'U' THEN 'Unknown'  
END  
,first_lsn AS [First LSN]  
,last_lsn AS [Last LSN]  
,backup_start_date AS [Backup Start Time]  
,backup_finish_date AS [Backup Completion Time]  
,expiration_date AS [Backup Expiry Date/Time]  
FROM  
smart_backup_files;
```  
  
 Veja a seguir uma explicação detalhada do status diferente retornado:  
  
-   **Disponível-a:** Este é um arquivo de backup normal. O backup foi concluído e também verificou se ele está disponível no armazenamento do Azure.  
  
-   **Cópia em andamento-B:** Esse status é especificamente para bancos de dados do grupo de disponibilidade. Se o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] detectar uma interrupção na cadeia de logs de backup, ele primeiro tentará identificar o backup que pode ter causado essa interrupção. Ao localizar o arquivo de backup, ele tenta copiar o arquivo para o armazenamento do Azure. Quando o processo de cópia estiver em andamento, ele exibirá esse status.  
  
-   **Falha na cópia-F:** Semelhante à cópia em andamento, esses bancos de dados de grupo de disponibilidade t são específicos. Se o processo de cópia falhar, o status será marcado como F.  
  
-   **Corrompido-C:** Se [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] o não puder verificar o arquivo de backup no armazenamento executando um comando restore HEADER_ONLY, mesmo após várias tentativas, ele marcará esse arquivo como corrompido. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] agendará um backup para garantir que o arquivo corrompido não resulte em uma interrupção da cadeia de backup.  
  
-   **Excluído-D:** O arquivo correspondente não pode ser encontrado no armazenamento do Azure. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] agendará um backup se o arquivo excluído resultar em uma interrupção na cadeia de backup.  
  
-   **Desconhecido-U:** Esse status indicou que [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ainda não foi capaz de verificar a existência do arquivo e suas propriedades no armazenamento do Azure. Na próxima vez que o processo for executado, que é aproximadamente a cada 15 minutos, esse status será atualizado.  
