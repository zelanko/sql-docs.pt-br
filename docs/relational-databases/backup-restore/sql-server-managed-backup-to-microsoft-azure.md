---
title: Backup gerenciado do SQL Server no Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c041ee4a56b2df2190eabb0da0ef472f0b8ee49
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63008555"
---
# <a name="sql-server-managed-backup-to-microsoft-azure"></a>Backup gerenciado do SQL Server no Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] gerencia e automatiza os backups do SQL Server no Armazenamento de Blobs do Microsoft Azure. Você pode permitir que o SQL Server determine a agenda de backup com base na carga de trabalho de transação do banco de dados. Ou pode usar as opções avançadas para definir uma agenda. As configurações de retenção determinam por quanto tempo os backups são armazenados no Armazenamento de Blobs do Azure. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] oferece suporte para restauração pontual durante o período de retenção especificado.  
  
 Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], os procedimentos e o comportamento básico de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] foi alterado. Para saber mais, confira [Migrate SQL Server 2014 Managed Backup Settings to SQL Server 2016](../../relational-databases/backup-restore/migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016.md).  
  
> [!TIP]  
>  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] é recomendado para as instâncias do SQL Server em execução em máquinas virtuais do Microsoft Azure.  
  
## <a name="benefits"></a>Benefícios  
 Atualmente, a automatização de backups para vários bancos de dados requer o desenvolvimento de uma estratégia de backup, a gravação de código personalizado e o agendamento de backups. Com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], você pode criar um plano de backup, especificando somente o período de retenção e o local do armazenamento. Embora as configurações avançadas estejam disponíveis, elas não são obrigatórias. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] agenda, executa e mantém os backups.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pode ser configurado no nível do banco de dados ou no nível da instância do SQL Server. Durante a configuração no nível de instância, quaisquer bancos de dados novos também passam por backup automaticamente. As configurações no nível do banco de dados podem ser usadas para substituir os padrões de nível de instância em uma ocorrência individual.  
  
 Você também pode criptografar os backups para obter segurança adicional, e pode configurar um agendamento personalizado para controlar quando os backups são feitos. Para obter mais detalhes sobre os benefícios de usar o armazenamento de Blobs do Microsoft Azure para backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
##  <a name="Prereqs"></a> Pré-requisitos  
 O Armazenamento do Microsoft Azure é usado pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para armazenar os arquivos de backup. Os seguintes pré-requisitos são necessários:  
  
|Pré-requisito|Descrição|  
|------------------|-----------------|  
|**Conta do Microsoft Azure**|Você pode começar a usar o Azure com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/) antes de explorar as [opções de compra](https://azure.microsoft.com/pricing/purchase-options/).|  
|**Conta de Armazenamento do Azure**|Os backups são armazenados no Armazenamento de Blobs do Azure associado a uma conta de armazenamento do Azure. Para obter instruções passo a passo para criar uma conta de armazenamento, confira [Sobre as contas de armazenamento do Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/).|  
|**Contêiner de Blob**|Os blobs são organizados em contêineres. Especifique o contêiner de destino para os arquivos de backup. Você pode criar um contêiner no [Portal de Gerenciamento do Azure](https://manage.windowsazure.com/) ou usar o comando **New-AzureStorageContainer** do [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).|  
|**SAS (Assinatura de Acesso Compartilhado)**|O acesso ao contêiner de destino é controlado por uma SAS (Assinatura de Acesso Compartilhado). Para ter uma visão geral da SAS, confira [Assinaturas de Acesso Compartilhado, Parte 1: Noções básicas sobre o modelo SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). É possível criar um token SAS no código ou com o comando **New-AzureStorageContainerSASToken** do PowerShell. Para obter um script do PowerShell que simplifica esse processo, confira [Simplifying creation of SQL Credentials with Shared Access Signature (SAS) tokens on Azure Storage with Powershell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)(Simplificando a criação de credenciais do SQL com tokens SAS [Assinatura de Acesso Compartilhado] no Armazenamento do Azure com o Powershell). O token SAS pode ser armazenado em uma **Credencial do SQL** para uso com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|**SQL Server Agent**|O SQL Server Agent deve estar em execução para que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] funcione. Considere a configuração da opção de inicialização como automática.|  
  
## <a name="components"></a>Componentes  
 Transact-SQL é a principal interface para interagir com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Os procedimentos armazenados do sistema são usados para habilitar, configurar e monitorar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. As funções do sistema são usadas para recuperar parâmetros de configuração existentes, valores de parâmetro e informações do arquivo de backup. Os eventos estendidos são usados navegar por erros e avisos. Os mecanismos do alerta são habilitados por meio de trabalhos do SQL Agent e do Gerenciamento Baseado em Política do SQL Server. A seguir é mostrada uma lista dos objetos e uma descrição dessa funcionalidade em relação ao [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 Os cmdlets do PowerShell também estão disponíveis para configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. O SQL Server Management Studio oferece suporte à restauração de backups criados pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usando a tarefa **Restaurar Banco de Dados**  
  
|||  
|-|-|  
|Objeto do Sistema|Descrição|  
|**MSDB**|Armazena os metadados, o histórico de backup de todos os backups criados pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)|Habilita o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)|Define as configurações avançadas para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], como a criptografia.|  
|[managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|Cria uma agenda personalizada para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[managed_backup.sp_ backup_master_switch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql.md)|Pausa e retoma [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[managed_backup.sp_set_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql.md)|Habilita e configura o monitoramento para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Exemplos: habilitação de eventos estendidos, configurações de email para notificações.|  
|[managed_backup.sp_backup_on_demand &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql.md)|Executa um backup ad-hoc para um banco de dados habilitado para usar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] sem interromper a cadeia de logs.|  
|[managed_backup.fn_backup_db_config &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql.md)|Retorna os valores atuais de status e configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados ou para todos os bancos de dados na instância.|  
|[managed_backup.fn_is_master_switch_on &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql.md)|Retorna o status da opção mestra.|  
|[managed_backup.sp_get_backup_diagnostics &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql.md)|Retorna os eventos registrados pelos Eventos Estendidos.|  
|[managed_backup.fn_get_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql.md)|Retorna os valores atuais de configurações do sistema de backup como configurações de monitoramento e de email para alertas.|  
|[managed_backup.fn_available_backups &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md)|Recupera os backups disponíveis para um banco de dados especificado ou para todos os bancos de dados em uma instância.|  
|[managed_backup.fn_get_current_xevent_settings &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql.md)|Retorna as configurações atuais do evento estendido.|  
|[managed_backup.fn_get_health_status &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql.md)|Retorna as contagens agregadas dos erros registrados pelos Eventos Estendidos para um período especificado.|  
  
## <a name="backup-strategy"></a>Estratégia de backup  
  
### <a name="backup-scheduling"></a>Agendamento de backup  
 Você pode especificar um agendamento de backup personalizado usando o procedimento armazenado do sistema [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md). Se você não especificar uma agenda personalizada, o tipo de backups agendados e a frequência de backup serão determinados com base na carga de trabalho do banco de dados. As configurações de período de retenção são usadas para determinar o tempo durante o qual o arquivo de backup deverá ser mantido no armazenamento e a capacidade de recuperar o banco de dados para um determinado momento no período de retenção.  
  
### <a name="backup-file-naming-conventions"></a>Convenções de nomenclatura do arquivo de backup  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa o contêiner que você especificar, para que você tenha controle sobre o nome do contêiner. Os arquivos de backup de bancos de dados não disponíveis são nomeados usando a seguinte convenção: O nome é criado usando os primeiros 40 caracteres do nome do banco de dados, o GUID do banco de dados, sem o '-' e o carimbo de data/hora. O caractere de sublinhado é inserido entre segmentos como separadores. A extensão de arquivo **.bak** é usada no backup completo e a extensão de arquivo **.log** é usada nos backups de log. Para bancos de dados do Grupo de Disponibilidade, além da convenção de nomenclatura de arquivo descrita acima, o GUID do banco de dados do Grupo de Disponibilidade é adicionado após os 40 caracteres do nome do banco de dados. O valor de GUID do banco de dados do Grupo de Disponibilidade é o valor para o group_database_id em sys.databases.  
  
### <a name="full-database-backup"></a>Backup de banco de dados Completo  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] programa um backup completo do banco de dados se qualquer uma das seguintes afirmações for verdadeira.  
  
-   Um banco de dados é habilitado para o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pela primeira vez ou quando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] é habilitado com as configurações padrão no nível da instância.  
  
-   O crescimento do log desde o backup completo do banco de dados mais recente é igual a ou maior que 1 GB.  
  
-   O intervalo de tempo máximo de uma semana passou desde o último backup completo do banco de dados.  
  
-   A cadeia de log foi interrompida. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] verifica periodicamente se a cadeia de logs está intacta comparando o primeiro e o último LSNs dos arquivos de backup. Se houver uma quebra na cadeia de logs por qualquer motivo, o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] agendará um backup completo do banco de dados. O motivo mais comum para quebras da cadeia de log provavelmente é a emissão de um comando de backup com o uso de Transact-SQL ou por meio da tarefa Backup no SQL Server Management Studio.  Outros cenários comuns incluem a exclusão acidental dos arquivos de log de backup ou substituições acidentais de backup.  
  
### <a name="transaction-log-backup"></a>Backup do log de transações  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] agenda um backup de log se alguma das seguintes afirmações for verdadeira:  
  
-   Não há nenhum histórico de backup de log que possa ser encontrado. Isso geralmente é verdadeiro quando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] é habilitado pela primeira vez.  
  
-   O espaço de log de transações usado é 5 MB ou mais.  
  
-   O intervalo de tempo máximo de 2 horas desde que o último backup de log foi atingido.  
  
-   Quando o backup de log de transações está atrás de um backup completo de banco de dados. A meta é manter a cadeia de logs à frente do backup completo.  
  
## <a name="retention-period-settings"></a>Configurações de período de retenção  
 Ao habilitar o backup, você deve definir o período de retenção em dias: O valor mínimo é 1 dia e o máximo, 30 dias.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] , com base nas configurações de período de retenção, avalia a capacidade de recuperação para um momento específico, a fim de determinar quais arquivos de backup serão mantidos e identificar os arquivos de backup a serem excluídos. A backup_finish_date do backup é usada para determinar e associar o tempo especificado pelas configurações de período de retenção.  
  
## <a name="important-considerations"></a>Considerações importantes  
 No caso de um banco de dados, se houver um trabalho de backup de banco de dados completo existente, o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] aguardará a conclusão do trabalho atual antes da realização de um backup de banco de dados completo no mesmo banco de dados. Da mesma forma, somente um backup de log de transações pode ser executado em um determinado momento. No entanto, um backup completo de banco de dados e um backup de log de transações podem ser executados simultaneamente. As falhas são registradas como Eventos Estendidos.  
  
 Se mais de 10 backups de bancos de dados completos simultâneos estiverem agendados, um aviso será emitido por meio do canal de depuração de Eventos Estendidos. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] mantém uma fila de prioridade para os bancos de dados restantes que precisam de backup até que todos os backups sejam agendados e concluídos.  

> [!NOTE]
> Não há suporte para backup gerenciado do SQL Server com servidores proxy.
>
  
##  <a name="support_limits"></a> Suporte  
 As seguintes limitações e considerações de suporte são específicas para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   Há suporte para o backup de bancos de dados de sistema **master**, **model**e **msdb** . Não há suporte para o backup de **tempdb** . 
  
-   Para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], há suporte para todos os modelos de recuperação (Completo, Bulk-logged e Simples).  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] oferece suporte apenas para backups de banco de dados completos e de log. Não há suporte para a automação de backups de arquivo.  
  
-   O serviço de Armazenamento de Blobs do Microsoft Azure é a única opção de armazenamento de backup com suporte. Não há suporte para backups em disco ou fita.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa o recurso Backup no Blob de Blocos. O tamanho máximo de um blob de blocos é de 200 GB. Mas, utilizando a distribuição, o tamanho máximo de um backup individual pode ser de até 12 TB. Se seus requisitos de backup ultrapassarem isso, considere o uso da compactação e teste o tamanho do arquivo de backup antes de configurar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Você pode realizar o teste fazendo backup em um disco local ou backup manual do armazenamento do Microsoft Azure usando a instrução Transact-SQL **BACKUP TO URL** . Para saber mais, confira [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pode ter algumas limitações quando configurado com outras tecnologias com suporte para backup, alta disponibilidade ou recuperação de desastres.  
  
## <a name="see-also"></a>Consulte Também  
- [Habilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)   
- [Configurar opções avançadas de backup gerenciado do SQL Server para o Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)   
- [Desabilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/disable-sql-server-managed-backup-to-microsoft-azure.md)
- [Fazer backup e restaurar bancos de dados do sistema](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)
- [Fazer backup dos bancos de dados do SQL Server e restaurá-los](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
  
  
