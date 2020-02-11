---
title: Solução de problemas SQL Server Backup gerenciado para o Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: a34d35b0-48eb-4ed1-9f19-ea14754650da
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 385fa6f6bd874734207c6fec10ddc687b951825a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76929440"
---
# <a name="troubleshooting-sql-server-managed--backup-to-azure"></a>Solucionar problemas de backup gerenciado do SQL Server para Azure
  Este tópico descreve as tarefas e as ferramentas que você pode usar para solucionar erros que podem ocorrer durante as operações do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
## <a name="overview"></a>Visão geral  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tem verificações internas e soluções de problemas; portanto, em muitos casos, as falhas internas são administradas pelo próprio processo do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
 Um exemplo de tal caso é uma exclusão de um arquivo de backup, resultando em uma interrupção da cadeia de logs que afeta [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] a capacidade de recuperação – identificará a interrupção na cadeia de logs e agendará um backup para ser levado imediatamente. No entanto, recomendamos que você monitore o status e aborde todos os erros que requerem intervenção manual.  
  
 O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] registra eventos e erros usando procedimentos armazenados do sistema, exibições de sistema e eventos estendidos. As exibições do sistema e os procedimentos armazenados fornecem informações de configuração do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], status de backups agendados e os erros capturados pelos Eventos Estendidos. O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usa os Eventos Estendidos para capturar os erros a serem usados na solução de problemas. Além de registrar eventos, as Políticas de Administrador Inteligentes do SQL Server fornecem um status de integridade que é usado por um trabalho de notificação por email para fornecer notificações ou informar sobre erros e problemas. Para obter mais informações, consulte [monitorar SQL Server Backup gerenciado no Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]também usa o mesmo log que é usado ao fazer backup manual do armazenamento do Azure (SQL Server Backup para URL). Para obter mais informações sobre problemas relacionados ao backup em URL, consulte a seção solução de problemas em [SQL Server Backup to URL Best Practices and Troubleshooting](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
### <a name="general-troubleshooting-steps"></a>Etapas gerais da solução de problemas  
  
1.  Habilite a Notificação por Email para começar a receber emails de erros e avisos.  
  
     Se desejar, você também pode executar `smart_admin.fn_get_health_status` periodicamente para verificar os erros e as contagens de agregação. Por exemplo, `number_of_invalid_credential_errors` é o número de vezes em que o backup inteligente tentou um backup mas obteve um erro de credencial inválida. 
  `Number_of_backup_loops` e `number_of_retention_loops` não são erros, mas indicam o número de vezes que o thread de backup e o thread de retenção verificaram a lista de bancos de dados. Normalmente, quando @begin_time e @end_time não são fornecidos, a função está mostrando as informações dos últimos 30 minutos e, normalmente, devemos ver valores diferentes de zero para essas duas colunas. Se eles forem zero, o sistema está sobrecarregado ou não está respondendo. Para obter mais informações, consulte a seção **solução de problemas do sistema** mais adiante neste tópico.  
  
2.  Revise os logs de Eventos Estendidos para obter mais detalhes sobre erros e outros eventos associados.  
  
3.  Use as informações nos logs para resolver o problema.  No caso de um problema ou erro do sistema, talvez seja necessário reiniciar o serviço ou o SQL Server Agent.  
  
### <a name="common-causes-of-errors"></a>Causas comuns de erros  
 Esta é a lista das causas comuns de falhas:  
  
1.  **Alterações na credencial SQL:** Se o nome da credencial usada pelo [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] for alterado ou se for excluído, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] o não poderá fazer backups. A alteração deve ser aplicada aos parâmetros de configuração do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
2.  **Alterações nos valores de chave de acesso de armazenamento:** Se os valores de chave de armazenamento forem alterados para a conta do Azure, mas a credencial do SQL não for [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] atualizada com os novos valores, o falhará ao autenticar no armazenamento e falhará no backup dos bancos de dados configurados para usar essa conta.  
  
3.  **Alterações na conta de armazenamento do Azure:** Excluir ou renomear a conta de armazenamento sem alterações correspondentes à credencial [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] do SQL causará falha e nenhum backup será feito. Se você excluir uma conta de armazenamento, verifique se os bancos de dados foram reconfigurados com informações válidas da conta de armazenamento. Se uma conta de armazenamento for renomeada ou os valores de chave forem alterados, verifique se essas alterações são refletidas na Credencial do SQL usada pelo [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
4.  **Alterações nas propriedades do banco de dados:** As alterações nos modelos de recuperação ou a alteração do nome podem fazer com que os backups falhem.  
  
5.  **Alterações no modelo de recuperação:** Se o modelo de recuperação do banco de dados for alterado para simples de completo ou bulk-logged, os backups serão interrompidos e os bancos de dados serão [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]ignorados pelo. Para obter mais informações, consulte [SQL Server Backup gerenciado para o Azure: interoperabilidade e coexistência](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>Mensagens de erro e soluções mais comuns  
  
1.  **Erros ao habilitar ou configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:**  
  
     Erro: "falha ao acessar a URL de armazenamento.... Forneça uma credencial SQL válida... ": você pode ver que este e outros erros semelhantes referentes a credenciais do SQL.  Nesses casos, examine o nome da credencial do SQL que você forneceu e também as informações armazenadas na credencial do SQL – o nome da conta de armazenamento e a chave de acesso de armazenamento e certifique-se de que elas sejam atuais e válidas.  
  
     Erro: "... Não é possível configurar o banco de dados... como ele é um banco de dados do sistema ": você verá esse erro se tentar habilitar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] o para um banco de dados do sistema.  O [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] não oferece suporte a backups para bancos de dados do sistema.  Para configurar o backup para um banco de dados do sistema, use outras tecnologias de Backup do SQL Server como planos de manutenção.  
  
     Erro: "... Fornecer um período de retenção.... ": você poderá ver erros referentes ao período de retenção se não tiver especificado um período de retenção para o banco de dados ou instância quando estiver configurando esses valores pela primeira vez. Você também poderá consultar um erro se fornecer um valor diferente de um número entre 1 e 30. O valor permitido para o período de retenção é um número entre 1 e 30.  
  
2.  **Erros de notificação por email:**  
  
     Erro: "Database Mail não está habilitado..."-você verá esse erro se habilitar notificações por email, mas Database Mail não estiver configurado na instância. Você deve configurar o Database Mail na instância para que possa receber a notificação sobre o status de integridade do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para obter informações sobre como habilitar o Database Mail, consulte [configurar Database Mail](../relational-databases/database-mail/configure-database-mail.md). Você também deve habilitar o SQL Server Agent para usar o Database Mail para notificações. Para obter mais informações, consulte [antes de começar](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin).  
  
     Esta é uma lista dos números de erro que você possivelmente verá e que estão associados às notificações por email:  
  
    -   ErrorNumber: 45209  
  
    -   ErrorNumber: 45210  
  
    -   ErrorNumber: 45211  
  
3.  **Erros de conectividade:**  
  
    -   **Erros relacionados à conectividade do SQL:** Esses erros ocorrem quando há problemas ao se conectar à instância do SQL Server. Os eventos estendidos expõem esses tipos de erros pelo canal de administração. Veja a seguir os dois eventos estendidos que você pode consultar em busca de erros relacionados a esse tipo de problemas de conectividade:  
  
         FileRetentionAdminXEvent com event_type = SqlError. Para obter detalhes deste erro, consulte o error_code, error_message e stack_trace desse evento. O error_code é o número do erro de SqlException.  
  
         SmartBackupAdminXevent com as seguintes mensagens/prefixos de mensagem:  
  
         *"Ocorreu um erro interno ao configurar SQL Server Backup gerenciado para as configurações padrão do Azure para a instância. Erro pode ser transitório. "*  
  
         *"Provavelmente está tendo problemas de conectividade com SQL Server. Ignorando o banco de dados na iteração atual. "*  
  
         *"Falha ao consultar informações de uso do log. A falha pode ser transitória. Ignorando o banco de dados na iteração atual. "*  
  
         *"Exceção SQL encontrada ao carregar os metadados do agente SSMBackup2WA. A falha pode ser transitória. A operação será repetida. "*  
  
         *"SSMBackup2WA encontrou uma exceção SQL durante... "*  
  
    -   **Erros durante a conexão com a conta de armazenamento:**  
  
         As exceções de armazenamento são relatadas em FileRetentionAdminXEvent com event_type = XstoreError. Para obter detalhes do erro, consulte o error_message e stack_trace desse evento.  
  
         Como o Backup Gerenciado do SQL Server usa a tecnologia subjacente de Backup para URL, os erros relacionados à conectividade de armazenamento aplicam-se a ambos os recursos. Para obter mais informações sobre etapas de solução de problemas, consulte a **seção solução de problemas** do artigo [SQL Server práticas recomendadas de backup to URL e solução de problemas](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) .  
  
### <a name="troubleshooting-system-issues"></a>Solucionando problemas do sistema  
 Estes são alguns cenários possíveis quando há um problema no sistema (SQL Server, SQL Server Agent) e seus efeitos no [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:  
  
-   **O sqlservr. exe para de responder ou para [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] de funcionar quando o está em execução:** se SQL Server parar de funcionar, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] agente do SQL será desligado normalmente, também parará e os eventos serão registrados no arquivo SQL Agent. out.  
  
     Se o SQL Server parar de responder, os eventos serão registrados no canal de administração.  Um exemplo do log de eventos:  
  
     *Erro de SQL (mecanismo não respondendo ou Get sqlException: SqlException:*   
     *código de erro, mensagem e StackTrace serão exibidos em um canal de administrador XEvent, junto com algumas informações adicionais, como:*   
    *"Provavelmente está tendo problemas de conectividade com SQL Server. Ignorando o banco de dados na iteração atual "*  
  
-   **O agente SQL para de responder ou para [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] de funcionar quando o está em execução:**  
  
     Se o SQL Agent para de funcionar, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] também será interrompido e os eventos serão registrados no canal de administração. Isso é semelhante aos cenários em que o SQL Server para de responder.  
  
     Se o SQL Agent parar de responder, o [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] não poderá continuar as operações de backup, e os eventos serão registrados no canal de administração. Um exemplo do log de eventos:  
  
     *Bloqueios de trabalho: consulte canal de administrador XEvents*   
    *"Uma atualização de progresso não foi recebida de SQL Server em mais de" + Constants. DBBackupInfoMsgMaxWaitTime + "horas para backup de banco de dados.   O backup de nuvem SSM continuará aguardando. "*  
  
 Se você tiver habilitado a notificação por email, receberá uma notificação que inclui o **número de loops de backup** e o **número de loops de retenção**. Se o valor retornado na notificação para uma ou ambas as colunas for zero, isso pode ser uma indicação de que o sistema não está respondendo.  
  
> [!WARNING]  
>  Os processos internos que geram os resultados para o relatório supõem que os logs de diagnóstico de mecanismo estejam no mesmo local do log de erros do SQL Agent, que, por padrão, está na mesma pasta dos logs de erro da instância do SQL Server. Se os logs de diagnóstico do mecanismo forem movidos para um local diferente do local do log de erros do SQL Agent, o sistema não conseguirá localizar os logs de diagnóstico de backup e, consequentemente o relatório da notificação por email poderá não estar correto. Por exemplo, você pode ver um valor **0** em todos os campos relatados, incluindo o número de loops de backup e o número de loops de retenção. Neste caso onde os logs de diagnóstico são movidos para um local diferente, isso pode não significar que o sistema não esteja respondendo, mas que o sistema não consegue encontrar os logs. Primeiro, verifique se o local dos logs de diagnóstico e dos logs de erro do SQL Agent estão no mesmo local Para verificar o local atual dos logs de diagnóstico, você pode usar [Sys. dm_os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations). A `path` coluna retorna o local atual dos logs de diagnóstico do mecanismo.  Ele deve estar na mesma pasta que os logs de erros do SQL Agent. Você pode obter o caminho do log de erros do SQL Agent usando o procedimento armazenado `dbo.sp_get_sqlagent_properties`.  
  
 Verifique os logs de eventos estendidos para ver os detalhes dos erros. Corrija os erros ou reinicie o SQL Server Agent para resolver a situação.  
  
  
