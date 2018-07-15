---
title: Solução de problemas do SQL Server Managed Backup to Windows Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a34d35b0-48eb-4ed1-9f19-ea14754650da
caps.latest.revision: 18
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fd751224b24583cf5426194d7b4fc5074349bdfd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306137"
---
# <a name="troubleshooting-sql-server-managed--backup-to-windows-azure"></a>Solução de problemas do SQL Server Managed Backup to Windows Azure
  Este tópico descreve as tarefas e as ferramentas que você pode usar para solucionar erros que podem ocorrer durante as operações do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
## <a name="overview"></a>Visão geral  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tem verificações internas e soluções de problemas; portanto, em muitos casos, as falhas internas são administradas pelo próprio processo do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
 O exemplo desse caso é a exclusão de um arquivo de backup, resultando em uma interrupção da cadeia de logs que afeta a capacidade de recuperação; o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] identificará a interrupção na cadeia de logs e agendará um backup a ser executado imediatamente. No entanto, recomendamos que você monitore o status e aborde todos os erros que requerem intervenção manual.  
  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] registra eventos e erros usando procedimentos armazenados do sistema, exibições de sistema e eventos estendidos. As exibições do sistema e os procedimentos armazenados fornecem informações de configuração do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], status de backups agendados e os erros capturados pelos Eventos Estendidos. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usa os Eventos Estendidos para capturar os erros a serem usados na solução de problemas. Além de registrar eventos, as Políticas de Administrador Inteligentes do SQL Server fornecem um status de integridade que é usado por um trabalho de notificação por email para fornecer notificações ou informar sobre erros e problemas. Para obter mais informações, consulte [Monitor de SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] também usa o mesmo log utilizado ao fazer backup manualmente do armazenamento do Windows Azure (Backup do SQL Server para URL). Para obter mais informações sobre Backup para URL relacionados a problemas, consulte a seção solução de problemas em [SQL Server Backup to URL Best Practices and Troubleshooting](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
### <a name="general-troubleshooting-steps"></a>Etapas gerais da solução de problemas  
  
1.  Habilite a Notificação por Email para começar a receber emails de erros e avisos.  
  
     Se desejar, você também pode executar `smart_admin.fn_get_health_status` periodicamente para verificar os erros e as contagens de agregação. Por exemplo, `number_of_invalid_credential_errors` é o número de vezes em que o backup inteligente tentou um backup mas obteve um erro de credencial inválida. `Number_of_backup_loops` e `number_of_retention_loops` não são erros, mas indicam o número de vezes que o thread de backup e o thread de retenção verificaram a lista de bancos de dados. Normalmente, quando @begin_time e @end_time não forem fornecidos, a função está mostrando as informações dos últimos 30 minutos, então, normalmente veremos valores diferentes de zero para essas duas colunas. Se eles forem zero, o sistema está sobrecarregado ou não está respondendo. Para obter mais informações, consulte **Solucionando problemas do sistema** seção mais adiante neste tópico.  
  
2.  Revise os logs de Eventos Estendidos para obter mais detalhes sobre erros e outros eventos associados.  
  
3.  Use as informações nos logs para resolver o problema.  No caso de um problema ou erro do sistema, talvez seja necessário reiniciar o serviço ou o SQL Server Agent.  
  
### <a name="common-causes-of-errors"></a>Causas comuns de erros  
 Esta é a lista das causas comuns de falhas:  
  
1.  **Alterações na credencial SQL:** se o nome da credencial usada por [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] é alterado ou se ele for excluído, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] não será possível fazer backups. A alteração deve ser aplicada aos parâmetros de configuração do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
2.  **Alterações em valores de chave de acesso de armazenamento:** se os valores de chave de armazenamento são alterados para a conta do Windows Azure, mas a credencial do SQL não é atualizada com os novos valores, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] falhará ao autenticar para o armazenamento e há falha no backup bancos de dados configurados para usar essa conta.  
  
3.  **Altera a conta de armazenamento do Windows Azure:** excluir ou renomear a conta de armazenamento sem fará com que as alterações correspondentes na credencial SQL [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] falhe e nenhum backup será feito. Se você excluir uma conta de armazenamento, verifique se os bancos de dados foram reconfigurados com informações válidas da conta de armazenamento. Se uma conta de armazenamento for renomeada ou os valores de chave forem alterados, verifique se essas alterações são refletidas na Credencial do SQL usada pelo [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
4.  **Alterações em Propriedades do banco de dados:** alterações aos modelos de recuperação ou alterando o nome pode causar a falha de backup.  
  
5.  **Alterações no modelo de recuperação de:** se o modelo de recuperação do banco de dados é alterado para simples de completa ou bulk-logged, os backups serão interrompidos e os bancos de dados serão ignorados pelo [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para obter mais informações, consulte [SQL Server Managed Backup to Windows Azure: interoperabilidade e coexistência](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>Mensagens de erro e soluções mais comuns  
  
1.  **Erros ao habilitar ou configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:**  
  
     Erro: “Falha ao acessar a URL de armazenamento…. Forneça uma credencial SQL válida..." : Você pode ver esse e outros erros similares em relação às credenciais SQL.  Nesses casos, examine o nome da Credencial do SQL que você forneceu e também as informações armazenadas na Credencial do SQL – o nome da conta de armazenamento e a chave de acesso de armazenamento e verifique se eles estão atualizados e válidos.  
  
     Erro: "... não é possível configurar o banco de dados... porque ele é um banco de dados do sistema": você verá esse erro se você tentar habilitar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados do sistema.  O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] não oferece suporte a backups para bancos de dados do sistema.  Para configurar o backup para um banco de dados do sistema, use outras tecnologias de Backup do SQL Server como planos de manutenção.  
  
     Erro: "... Forneça um período de retenção..." : Você poderá ver erros referentes ao período de retenção se você não estiver especificado um período de retenção para o banco de dados ou instância quando você estiver configurando os valores pela primeira vez. Você também poderá consultar um erro se fornecer um valor diferente de um número entre 1 e 30. O valor permitido para o período de retenção é um número entre 1 e 30.  
  
2.  **Erros de notificação de email:**  
  
     Erro: "Database Mail não está habilitado..." – Você verá esse erro se você habilita notificações por email, mas o Database Mail não está configurado na instância. Você deve configurar o Database Mail na instância para que possa receber a notificação sobre o status de integridade do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para obter informações sobre como habilitar o database mail, consulte [configurar o Database Mail](../relational-databases/database-mail/configure-database-mail.md). Você também deve habilitar o SQL Server Agent para usar o Database Mail para notificações. Para obter mais informações, consulte [antes de começar](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin).  
  
     Esta é uma lista dos números de erro que você possivelmente verá e que estão associados às notificações por email:  
  
    -   ErrorNumber: 45209  
  
    -   ErrorNumber: 45210  
  
    -   ErrorNumber: 45211  
  
3.  **Erros de conectividade:**  
  
    -   **Erros relacionados à conectividade do SQL:** esses erros ocorrem quando há problemas para se conectar à instância do SQL Server. Os eventos estendidos expõem esses tipos de erros pelo canal de administração. Veja a seguir os dois eventos estendidos que você pode consultar em busca de erros relacionados a esse tipo de problemas de conectividade:  
  
         FileRetentionAdminXEvent com event_type = SqlError. Para obter detalhes deste erro, consulte o error_code, error_message e stack_trace desse evento. O error_code é o número de erro do SqlException.  
  
         SmartBackupAdminXevent com as seguintes mensagens/prefixos de mensagem:  
  
         *"Ocorreu um erro interno ao configurar o Backup gerenciado do SQL Server para as configurações padrão de Windows Azure por exemplo. Erro pode ser transitório."*  
  
         *"Provavelmente tendo problemas de conectividade com o SQL Server. Ignorando o banco de dados na iteração atual".*  
  
         *"Consultando as informações sobre o uso do log falhou. A falha pode ser transitória. Ignorando o banco de dados na iteração atual".*  
  
         *"Exceção do SQL ao carregar os metadados do agente de SSMBackup2WA. A falha pode ser transitória. Operação será repetida."*  
  
         *"O SSMBackup2WA encontrou exceção SQL enquanto... "*  
  
    -   **Erros de conexão com a conta de armazenamento:**  
  
         As exceções de armazenamento são relatadas em FileRetentionAdminXEvent com event_type = XstoreError. Para obter detalhes do erro, consulte o error_message e stack_trace desse evento.  
  
         Como o Backup Gerenciado do SQL Server usa a tecnologia subjacente de Backup para URL, os erros relacionados à conectividade de armazenamento aplicam-se a ambos os recursos. Para obter mais informações sobre as etapas de solução de problemas, consulte **seção solução de problemas** da [SQL Server Backup to URL Best Practices and Troubleshooting](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) artigo.  
  
### <a name="troubleshooting-system-issues"></a>Solucionando problemas do sistema  
 Estes são alguns cenários possíveis quando há um problema no sistema (SQL Server, SQL Server Agent) e seus efeitos no [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:  
  
-   **Sqlservr.exe para de responder ou de funcionar quando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está em execução:** se o SQL Server parar de funcionar, SQL Agent será fechado normalmente, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] também será interrompido e os eventos serão registrados no arquivo SQL Agent.  
  
     Se o SQL Server parar de responder, os eventos serão registrados no canal de administração.  Um exemplo do log de eventos:  
  
     *Erro de SQL (mecanismo não está respondendo ou obtém sqlException: SqlException:*   
     *rastreamento de pilha, a mensagem e código de erro serão exibidas em um canal de administração xevent, junto com algumas informações extras, como:*   
    *"Provavelmente tendo problemas de conectividade com o SQL Server. Ignorando o banco de dados na iteração atual"*  
  
-   **SQL Agent para de responder ou parar de funcionar quando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está em execução:**  
  
     Se o SQL Agent para de funcionar, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] também será interrompido e os eventos serão registrados no canal de administração. Isso é semelhante aos cenários em que o SQL Server para de responder.  
  
     Se o SQL Agent parar de responder, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] não poderá continuar as operações de backup, e os eventos serão registrados no canal de administração. Um exemplo do log de eventos:  
  
     *Paradas do trabalho: consulte os xevents do canal de administração*   
    *"Uma atualização em andamento ainda não foi recebida do SQL Server em mais de" + dbbackupinfomsgmaxwaittime + "horas para o backup do banco de dados.   O Backup de nuvem do SSM continuará esperando."*  
  
 Se você tiver habilitado a notificação por email, você receberá uma notificação que inclui **número de Loops de Backup** e **número de Loops de retenção**. Se o valor retornado na notificação para uma ou ambas as colunas for zero, isso pode ser uma indicação de que o sistema não está respondendo.  
  
> [!WARNING]  
>  Os processos internos que geram os resultados para o relatório supõem que os logs de diagnóstico de mecanismo estejam no mesmo local do log de erros do SQL Agent, que, por padrão, está na mesma pasta dos logs de erro da instância do SQL Server. Se os logs de diagnóstico do mecanismo forem movidos para um local diferente do local do log de erros do SQL Agent, o sistema não conseguirá localizar os logs de diagnóstico de backup e, consequentemente o relatório da notificação por email poderá não estar correto. Por exemplo, você verá um valor de **0** em todos os campos relatados incluindo o número de Loops de Backup e o número de Loops de retenção. Neste caso onde os logs de diagnóstico são movidos para um local diferente, isso pode não significar que o sistema não esteja respondendo, mas que o sistema não consegue encontrar os logs. Primeiro, verifique se o local dos logs de diagnóstico e dos logs de erro do SQL Agent estão no mesmo local Para verificar o local atual dos logs de diagnóstico, você pode usar [DM os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations). O `path` coluna retorna o local atual do mecanismo de logs de diagnóstico.  Ele deve estar na mesma pasta que os logs de erros do SQL Agent. Você pode obter o caminho do log de erros do SQL Agent usando o procedimento armazenado `dbo.sp_get_sqlagent_properties`.  
  
 Verifique os logs de eventos estendidos para ver os detalhes dos erros. Corrija os erros ou reinicie o SQL Server Agent para resolver a situação.  
  
  
