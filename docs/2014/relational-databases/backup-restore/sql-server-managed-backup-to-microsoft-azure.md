---
title: SQL Server Backup gerenciado para o Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ab44323dfabd389113351e413751b7a230c176e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70175760"
---
# <a name="sql-server-managed--backup-to-azure"></a>SQL Server Backup gerenciado para o Azure
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]gerencia e automatiza backups de SQL Server para o serviço de armazenamento de BLOBs do Azure. A estratégia de backup usada pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] baseia-se no período de retenção e na carga de trabalho da transação no banco de dados. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] oferece suporte para restauração pontual durante o período de retenção especificado.   
O [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pode ser habilitado no nível do banco de dados ou da instância para gerenciar todos os bancos de dados na instância do SQL Server. O SQL Server pode ser executado localmente ou em ambientes hospedados como a máquina virtual do Azure. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]é recomendado para SQL Server em execução em máquinas virtuais do Azure.  
  
## <a name="benefits-of-automating-sql-server-backup-using-includess_smartbackupincludesss-smartbackup-mdmd"></a>Benefícios da automatização do Backup do SQL Server usando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
-   Atualmente, a automatização de backups para vários bancos de dados requer o desenvolvimento de uma estratégia de backup, a gravação de código personalizado e o agendamento de backups. Usando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], você será solicitado a fornecer somente as configurações de período de retenção e o local do armazenamento. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]agenda, executa e mantém os backups.  
  
     O [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pode ser configurado no nível do banco de dados ou definido com as configurações padrão para uma instância do SQL Server. Automatizar o backup [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usando o tem os seguintes benefícios:  
  
    -   Ao definir os padrões no nível da instância, você pode aplicar essas configurações a qualquer banco de dados criado depois disso, removendo assim o risco de novos bancos de dados não serem submetidos a backup e de perda de dados.  
  
    -   A opção de habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] e definir o período de retenção no nível do banco de dados permite que você substitua as configurações padrão definidas no nível da instância. Isso permite que você tenha um controle mais granular da capacidade de recuperação de um banco de dados específico.  
  
-   Com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], você não precisa especificar o tipo ou a frequência dos backups de um banco de dados.  Você especifica o período de retenção e [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] determina o tipo e a frequência dos backups de um banco de dados que armazena os backups no serviço de armazenamento de BLOBs do Azure. Para obter mais detalhes sobre o conjunto de critérios [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] que o usa para criar a estratégia de backup, consulte a seção [componentes e conceitos](#Concepts) neste tópico.  
  
-   Quando configurado para usar a criptografia, você tem a segurança adicional dos dados do backup. Para obter mais informações, consulte [criptografia de backup](backup-encryption.md)  
  
 Para obter mais detalhes sobre os benefícios de usar o armazenamento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOBs do Azure para backups, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
## <a name="terms-and-definitions"></a>Termos e definições  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 Um recurso do SQL Server que automatiza o backup do banco de dados e mantém os backups com base no período de retenção.  
  
 Período de retenção  
 O período de retenção é usado pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para determinar quais arquivos de backup devem ser mantidos no armazenamento para recuperar um banco de dados pontual dentro do período especificado.  Os valores com suporte estão no intervalo de 1-30 dias.  
  
 Cadeia de logs  
 Uma sequência contínua de backups de log é denominada cadeia de logs. Uma cadeia de logs começa com um backup completo do banco de dados.  
  
##  <a name="Concepts"></a>Requisitos, conceitos e componentes  
  
  
###  <a name="Security"></a> Permissões  
 O Transact-SQL é a principal interface usada para configurar e monitorar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Em geral, para executar os procedimentos armazenados de configuração, **db_backupoperator** função de banco de dados com permissões para `EXECUTE` **alterar qualquer credencial** e permissões no procedimento armazenado **sp_delete_backuphistory** é necessária.  Os procedimentos armazenados e as funções usadas para examinar informações normalmente requerem permissões `Execute` no procedimento armazenado e `Select` na função respectivamente.  
  
###  <a name="Prereqs"></a> Pré-requisitos  
 **Pré-requisitos**  
  
 O **serviço de armazenamento do Azure** é usado pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para armazenar os arquivos de backup.    Os conceitos, a estrutura e os requisitos para a criação de uma conta de armazenamento do Azure são explicados em detalhes na seção [introdução aos principais componentes e conceitos](sql-server-backup-to-url.md#intorkeyconcepts) do tópico **SQL Server Backup to URL** .  
  
 A **credencial do SQL** é usada para armazenar as informações necessárias para autenticar a conta de armazenamento do Azure. O objeto de Credencial do SQL armazena o nome da conta e as informações de chave de acesso. Para obter mais informações, consulte a seção [Introduction to Key Components and Concepts](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) no tópico **SQL Server Backup to URL** . Para obter instruções sobre como criar uma credencial do SQL para armazenar informações de autenticação do armazenamento do Azure, consulte [lição 2: criar uma credencial de SQL Server](../../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
###  <a name="Concepts_Components"></a>Conceitos e componentes principais  
 O [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] é um recurso que gerencia as operações de backup. Ele armazena os metadados no banco de dados **msdb** e usa trabalhos do sistema para gravar backups completos de log de transações e bancos de dados.  
  
#### <a name="components"></a>Componentes  
 Transact-SQL é a principal interface para interagir com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Os procedimentos armazenados do sistema são usados para habilitar, configurar e monitorar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. As funções do sistema são usadas para recuperar parâmetros de configuração existentes, valores de parâmetro e informações do arquivo de backup. Os eventos estendidos são usados navegar por erros e avisos. Os mecanismos do alerta são habilitados por meio de trabalhos do SQL Agent e do Gerenciamento Baseado em Política do SQL Server. A seguir é mostrada uma lista dos objetos e uma descrição dessa funcionalidade em relação ao [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 Os cmdlets do PowerShell também estão disponíveis para configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. O SQL Server Management Studio oferece suporte à restauração de backups criados pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usando a tarefa **Restaurar Banco de Dados**  
  
|||  
|-|-|  
|Objeto do Sistema|DESCRIÇÃO|  
|**MSDB**|Armazena os metadados, o histórico de backup de todos os backups criados pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[smart_admin. set_db_backup &#40;&#41;do Transact-SQL](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)|Procedimento armazenado do sistema para habilitar e configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados.|  
|[smart_admin. set_instance_backup &#40;&#41;do Transact-SQL](https://msdn.microsoft.com/library/dn451009(v=sql.120).aspx)|Procedimento armazenado do sistema para habilitar e definir configurações [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] padrão para a instância de SQL Server.|  
|[smart_admin. sp_ backup_master_switch &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)|Procedimento armazenado do sistema para pausar e retomar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[smart_admin. sp_set_parameter &#40;&#41;do Transact-SQL](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)|Procedimento armazenado do sistema para habilitar e configurar o monitoramento para o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Exemplos: habilitação de eventos estendidos, configurações de email para notificações.|  
|[smart_admin. sp_backup_on_demand &#40;&#41;do Transact-SQL](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)|Procedimento armazenado do sistema que é usado para executar um backup ad hoc para um banco de dados que está habilitado [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para uso sem interromper a cadeia de logs.|  
|[smart_admin. fn_backup_db_config &#40;&#41;do Transact-SQL](/sql/relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql)|Função do sistema que retorna o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] status atual e os valores de configuração para um banco de dados ou para todos os bancos de dados na instância.|  
|[smart_admin. fn_is_master_switch_on &#40;&#41;do Transact-SQL](/sql/relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql)|Função do sistema que retorna o status da opção mestra.|  
|[smart_admin. sp_get_backup_diagnostics &#40;&#41;do Transact-SQL](/sql/relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql)|Procedimento armazenado do sistema usado para retornar os eventos registrados pelos Eventos Estendidos.|  
|[smart_admin. fn_get_parameter &#40;&#41;do Transact-SQL](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)|Função do sistema que retorna os valores atuais de configurações do sistema de backup como configurações de monitoramento e de email para alertas.|  
|[smart_admin. fn_available_backups &#40;&#41;do Transact-SQL](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)|Procedimento armazenado usado para recuperar backups disponíveis para um banco de dados especificado ou para todos os bancos de dados em uma instância.|  
|[smart_admin. fn_get_current_xevent_settings &#40;&#41;do Transact-SQL](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)|Função do sistema que retorna as configurações atuais do evento estendido.|  
|[smart_admin. fn_get_health_status &#40;&#41;do Transact-SQL](/sql/relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql)|A função do sistema que retorna as contagens agregadas dos erros registrados pelos Eventos Estendidos por um período especificado.|  
|[Monitorar o backup gerenciado do SQL Server para Azure](sql-server-managed-backup-to-microsoft-azure.md)|Eventos Estendidos para monitoramento, notificação por email dos erros e avisos, gerenciamento baseado em políticas do SQL Server para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
  
#### <a name="backup-strategy"></a>Estratégia de backup  
 **Estratégia de backup usada [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]por:**  
  
 O tipo de backups agendados e a frequência de backup são determinados com base na carga de trabalho do banco de dados. As configurações de período de retenção são usadas para determinar o tempo durante o qual o arquivo de backup deverá ser mantido no armazenamento e a capacidade de recuperar o banco de dados para um determinado momento no período de retenção.  
  
 **Contêiner de backup e convenções de nomenclatura de arquivo:**  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]nomeia o contêiner de armazenamento do Azure usando o SQL Server nome da instância para todos os bancos de dados, exceto bancos de dados de disponibilidade.  Para bancos de dados de disponibilidade, o GUID do grupo de disponibilidade é usado para nomear o contêiner de armazenamento do Azure.  
  
 O arquivo de backup para bancos de dados que não estão em disponibilidade é nomeado usando a seguinte convenção: o nome é criado usando os primeiros 40 caracteres do nome do banco de dados, o GUID do Database sem o '-' e o carimbo de data/hora. O caractere de sublinhado é inserido entre segmentos como separadores. A extensão de arquivo **.bak** é usada no backup completo e a extensão de arquivo **.log** é usada nos backups de log. Para bancos de dados do Grupo de Disponibilidade, além da convenção de nomenclatura de arquivo descrita acima, o GUID do banco de dados do Grupo de Disponibilidade é adicionado após os 40 caracteres do nome do banco de dados. O valor de GUID do banco de dados do Grupo de Disponibilidade é o valor para o group_database_id em sys.databases.  
  
 **Backup completo de banco de dados:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] o Agent agenda um backup de banco de dados completo se qualquer uma das seguintes opções for verdadeira.  
  
-   Um banco de dados é habilitado para o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pela primeira vez ou quando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] é habilitado com as configurações padrão no nível da instância.  
  
-   O crescimento do log desde o backup completo do banco de dados mais recente é igual a ou maior que 1 GB.  
  
-   O intervalo de tempo máximo de uma semana passou desde o último backup completo do banco de dados.  
  
-   A cadeia de log foi interrompida. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] verifica periodicamente se a cadeia de logs está intacta comparando o primeiro e o último LSNs dos arquivos de backup. Se houver uma quebra na cadeia de logs por qualquer motivo, o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] agendará um backup completo do banco de dados. O motivo mais comum para quebras da cadeia de log provavelmente é a emissão de um comando de backup com o uso de Transact-SQL ou por meio da tarefa Backup no SQL Server Management Studio.  Outros cenários comuns incluem a exclusão acidental dos arquivos de log de backup ou substituições acidentais de backup.  
  
 **Backup de log de transações:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] agenda um backup de log se qualquer uma das seguintes opções for verdadeira:  
  
-   Não há nenhum histórico de backup de log que possa ser encontrado. Isso geralmente é verdadeiro quando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] é habilitado pela primeira vez.  
  
-   O espaço de log de transações usado é 5 MB ou mais.  
  
-   O intervalo de tempo máximo de 2 horas desde que o último backup de log foi atingido.  
  
-   Quando o backup de log de transações está atrás de um backup completo de banco de dados. A meta é manter a cadeia de logs à frente do backup completo.  
  
#### <a name="retention-period-settings"></a>Configurações de período de retenção  
 Ao habilitar o backup, você deve definir o período de retenção em dias: o mínimo é 1 dia e o máximo é 30 dias.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] , com base nas configurações de período de retenção, avalia a capacidade de recuperação para um momento específico, a fim de determinar quais arquivos de backup serão mantidos e identificar os arquivos de backup a serem excluídos. A backup_finish_date do backup é usada para determinar e associar o tempo especificado pelas configurações de período de retenção.  
  
#### <a name="important-considerations"></a>Considerações importantes  
 Algumas considerações são importantes para compreender o impacto delas nas operações do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. As situações estão listadas abaixo:  
  
-   No caso de um banco de dados, se houver um trabalho de backup de banco de dados completo existente, o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] aguardará a conclusão do trabalho atual antes da realização de um backup de banco de dados completo no mesmo banco de dados. Da mesma forma, somente um backup de log de transações pode ser executado em um determinado momento. No entanto, um backup completo de banco de dados e um backup de log de transações podem ser executados simultaneamente. As falhas são registradas como Eventos Estendidos.  
  
-   Se mais de 10 backups de bancos de dados completos simultâneos estiverem agendados, um aviso será emitido por meio do canal de depuração de Eventos Estendidos. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] mantém uma fila de prioridade para os bancos de dados restantes que precisam de backup até que todos os backups sejam agendados e concluídos.  
  
###  <a name="support_limits"></a> Limitações de suporte  
 As limitações a seguir são específicas para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   O agente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] oferece suporte para backups de banco de dados somente: Completos e Backups de Log.  Não há suporte para a automação de backups de arquivo.  
  
-   No momento, as operações do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] têm suporte por meio do Transact-SQL. O monitoramento e a solução de problemas podem ser feitos com o uso de Eventos Estendidos. O suporte ao PowerShell e ao SMO está limitado à definição das configurações padrão de período de retenção e armazenamento de uma instância do SQL Server, e ao monitoramento do status de backup e da integridade geral com base nas políticas de Gerenciamento Baseado em Políticas do SQL Server.  
  
-   Não há suporte para os bancos de dados do sistema.  
  
-   O serviço de armazenamento de BLOBs do Azure é a única opção de armazenamento de backup com suporte. Não há suporte para backups em disco ou fita.  
  
-   Atualmente, o tamanho máximo de arquivo permitido para um blob de página no armazenamento do Azure é de 1 TB. Os arquivos de backup superiores a 1 TB apresentarão falha. Para evitar essa situação, é recomendável que, para bancos de dados grandes, você use a compactação e teste o tamanho do arquivo de backup antes de configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Você pode fazer o teste fazendo backup em um disco local ou fazendo backup manualmente no armazenamento do Azure usando `BACKUP TO URL` a instrução TRANSACT-SQL. Para saber mais, confira [SQL Server Backup to URL](sql-server-backup-to-url.md).  
  
-   Modelos de recuperação: somente os bancos de dados definidos como modelo Completo ou Bulk-logged têm suporte.  Os bancos de dados definidos como modelo de recuperação simples não têm suporte.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pode ter algumas limitações quando configurado com outras tecnologias com suporte para backup, alta disponibilidade ou recuperação de desastres. Para obter mais informações, consulte [SQL Server Backup gerenciado para o Azure: interoperabilidade e coexistência](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
|||  
|-|-|  
|**Descrições de tarefas**|**Tópico**|  
|As tarefas básicas, como configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados ou definir as configurações padrão no nível da instância, desabilitando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no nível da instância ou do banco de dados, pausando e reiniciando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Backup gerenciado do SQL Server para Azure – Configurações de retenção e armazenamento](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)|  
|**Tutorial:** Instruções passo a passo para configurar e monitorar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]o.|[Configurar o backup gerenciado do SQL Server para Azure](enable-sql-server-managed-backup-to-microsoft-azure.md)|  
|**Tutorial:** Instruções passo a passo para configurar e monitorar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] bancos de dados no grupo de disponibilidade.|[Configurar o backup gerenciado do SQL Server para Azure para grupos de disponibilidade](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)|  
|Ferramentas e conceitos, e tarefas relacionadas ao monitoramento do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Monitorar o backup gerenciado do SQL Server para Azure](sql-server-managed-backup-to-microsoft-azure.md)|  
|Ferramentas e etapas para a solução de problemas do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Solucionar problemas de backup gerenciado do SQL Server para Azure](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [SQL Server Backup para URL](sql-server-backup-to-url.md)   
 [SQL Server Backup gerenciado para o Azure: interoperabilidade e coexistência](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)   
 [Solucionar problemas de backup gerenciado do SQL Server para Azure](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)  
  
  
