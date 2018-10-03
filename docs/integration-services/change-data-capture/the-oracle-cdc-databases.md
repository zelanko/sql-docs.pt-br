---
title: Os bancos de dados Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a96486e9-f79b-4b24-bfaf-56203dd0e435
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 28b06c57666f07430a87d8577b7534cf47cf35de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630344"
---
# <a name="the-oracle-cdc-databases"></a>Os bancos de dados Oracle CDC
  Uma Instância do Oracle CDC está associada a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pelo mesmo nome na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. Este banco de dados é chamado de banco de dados Oracle CDC (ou banco de dados CDC).  
  
 O banco de dados CDC é criado e configurado usando o Console de Designer do Oracle CDC e contém os seguintes elementos:  
  
-   Um esquema `cdc` criado habilitando o banco de dados para o SQL Server CDC.  
  
-   Um conjunto de tabelas **cdc.xdbcdc_xxxx** usadas pela Instância do Oracle CDC.  
  
-   Um conjunto de tabelas de espelho vazias com as definições das tabelas capturadas no banco de dados Oracle de origem.  
  
-   Um conjunto de tabelas de alteração e funções de acesso de alteração que são geradas pelo mecanismo SQL Server CDC e são idênticos aos usados no SQL Server CDC habitual e não Oracle.  
  
 O esquema `cdc` só está inicialmente acessível aos membros da função de banco de dados fixa **dbowner** . O acesso às tabelas de alteração e funções de alteração é determinado pelo mesmo modelo de segurança que o SQL Server CDC. Para obter mais informações sobre o modelo de segurança, consulte [Modelo de segurança](http://go.microsoft.com/fwlink/?LinkId=231151).  
  
## <a name="creating-the-cdc-database"></a>Criando o banco de dados CDC  
 Na maioria dos casos, o banco de dados CDC é criado por meio do CDC Designer Console, mas também pode ser criado com um script de implantação CDC que é gerado com o CDC Designer Console. O administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá alterar as configurações de banco de dados se for necessário (por exemplo, para itens de armazenamento, segurança ou disponibilidade).  
  
 Para obter mais informações sobre como usar o CDC Designer Console para criar as tabelas de banco de dados e os scripts necessários, consulte [Usar novo Assistente de Instância](../../integration-services/change-data-capture/use-the-new-instance-wizard.md).  
  
## <a name="cdc-database-user-roles"></a>Funções de usuário de banco de dados CDC  
 Quando um Banco de dados CDC é criado e habilitado para CDC, um usuário de banco de dados chamado **cdc_service** é criado no banco de dados CDC e é associado ao logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o qual o Serviço Oracle CDC foi configurado. Esse usuário é declarado membro das funções de banco de dados **db_datareader**, **db_datawriter**e **db_ddladmin** . Se o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também estiver associado ao usuário `dbo` , o **cdc_service** não será criado.  
  
 Esta atribuição de função permite que o Serviço Oracle CDC atualize as tabelas sob o esquema `cdc` com dados capturados e com informações de controle.  
  
 Quando um banco de dados CDC é criado e as tabelas de origem de CDC são configuradas, o proprietário do banco de dados CDC pode conceder permissão SELECT de tabelas de espelho e pode definir funções associadas do SQL Server CDC para controlar quem acessa os dados de alteração.  
  
## <a name="mirror-tables"></a>Tabelas de espelho  
 Para cada tabela capturada, \<nome-do-esquema>.\<nome-da-tabela>, no banco de dados de origem do Oracle, uma tabela vazia semelhante é criada no Banco de Dados CDC, com o mesmo esquema e nome de tabela. As tabelas de origem do Oracle com o nome de esquema `cdc` (sem diferenciação de maiúsculas e minúsculas) não podem ser capturadas porque o esquema `cdc` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é reservado para o SQL Server CDC.  
  
 As tabelas de espelho estão vazias; não há dados armazenados nelas. Elas são usadas para habilitar a infraestrutura padrão do SQL Server CDC que é usada pela instância do Oracle CDC. Para impedir que os dados sejam inseridos ou atualizados nas tabelas de espelho, todas as operações UPDATE, DELETE e INSERT são negadas para PUBLIC. Isso garante que elas não sejam modificadas.  
  
## <a name="access-to-change-data"></a>Acesso a dados de alteração  
 Como o modelo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obtinha acesso aos dados de alteração que estavam associados a uma instância de captura, o usuário deve ter acesso `select` a todas as colunas capturadas da tabela de espelho associada (as permissões de acesso para as tabelas originais Oracle não fornecem acesso às tabelas de alteração no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Para obter informações sobre o modelo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Modelo de segurança](http://go.microsoft.com/fwlink/?LinkId=231151).  
  
 Além disso, se uma função de acesso for especificada quando a instância de captura for criada, o chamador também deverá ser um membro da função de acesso especificada. Outras funções gerais de captura de dados de alteração para o acesso aos metadados estão acessíveis a todos os usuários de banco de dados por meio da função PUBLIC, embora o acesso aos metadados retornados seja geralmente concedido pelo uso do acesso de seleção às tabelas de origem subjacentes e pela associação em qualquer função associada definida.  
  
 Os dados de alteração poderão ser lidos chamando-se funções especiais baseadas em tabela geradas pelo componente do SQL Server CDC quando uma instância de captura for criada. Para obter mais informações sobre essa função, consulte [Funções do Change Data Capture (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=231152).  
  
 O acesso a dados de CDC pelo componente de origem do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CDC está sujeito às mesmas regras.  
  
## <a name="the-cdc-database-tables"></a>As tabelas do banco de dados CDC  
 Essa seção descreve as seguintes tabelas no banco de dados CDC.  
  
-   [Tabelas de alteração (_CT)](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_Change_Tables_CT)  
  
-   [cdc.lsn_time_mapping](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdclsn_time_mapping)  
  
-   [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config)  
  
-   [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state)  
  
-   [cdc.xdbcdc_trace](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_trace)  
  
-   [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions)  
  
###  <a name="BKMK_Change_Tables_CT"></a> Tabelas de alteração (_CT)  
 As tabelas de alteração são criadas a partir das tabelas de espelho. Elas contêm os dados de alteração que são capturados do banco de dados Oracle. As tabelas são nomeadas de acordo com a convenção a seguir:  
  
 **[cdc].[\<instância-de-captura>_CT]**  
  
 Quando a captura é habilitada inicialmente para tabela `<schema-name>.<table-name>`, o nome de instância de captura padrão é `<schema-name>_<table-name>`. Por exemplo, o nome de instância de captura padrão para a tabela Oracle HR.EMPLOYEES é HR_EMPLOYEES e a tabela de alteração associada é [cdc]. [HR_EMPLOYEES_CT].  
  
 As tabelas de captura são escritas pela Instância do Oracle CDC. Elas são lidas usando funções com valor de tabela especiais geradas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , quando a instância de captura é criada. Por exemplo, `fn_cdc_get_all_changes_HR_EMPLOYEES`. Para obter mais informações sobre essas funções CDC, consulte [Funções do Change Data Capture (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=231152).  
  
###  <a name="BKMK_cdclsn_time_mapping"></a> cdc.lsn_time_mapping  
 A tabela **[cdc].[lsn_time_mapping]** é gerada pelo componente SQL Server CDC. Seu uso no caso do Oracle CDC é diferente que seu uso normal.  
  
 Para o Oracle CDC, os valores de LSN armazenados nesta tabela são baseados no valor SCN (Número de Alteração do Sistema) da Oracle associado com a alteração. Os 6 primeiros bytes do valor LSN são o número SCN original da Oracle.  
  
 Também ao usar o Oracle CDC, as colunas de hora (`tran_begin_time` e `tran_end_time`) armazenam a hora UTC da alteração em vez de a hora local como faz com o SQL Server CDC normal. Isto garante que as alterações do horário de verão não afetem os dados armazenados no lsn_time_mapping.  
  
###  <a name="BKMK_cdcxdbcdc_config"></a> cdc.xdbcdc_config  
 Essa tabela contém os dados de configuração para a Instância do Oracle CDC. Ela é atualizada utilizando o CDC Designer Console. Essa tabela tem somente uma linha.  
  
 A tabela a seguir descreve as colunas da tabela **cdc.xdbcdc_config** .  
  
|Item|Descrição|  
|----------|-----------------|  
|version|Isto mantém o controle da versão da configuração de instância CDC. Ela é atualizada a cada hora que a tabela é atualizada e a cada hora que uma nova instância de captura é adicionada ou uma instância de captura existente é removida.|  
|connect_string|Uma cadeia de conexão da Oracle. Um exemplo básico é:<br /><br /> `<server>:<port>/<instance>` (por exemplo, `erp.contoso.com:1521/orcl`).<br /><br /> A cadeia de conexão também pode especificar um descritor de conexão do Oracle Net, por exemplo, `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`.<br /><br /> Se estiver usando um servidor de diretório ou tnsnames, a cadeia de conexão pode ser o nome da conexão.<br /><br /> Para obter mais informações sobre cadeias de conexão de banco de dados da Oracle, veja [http://go.microsoft.com/fwlink/?LinkId=231153](http://go.microsoft.com/fwlink/?LinkId=231153) para o Oracle Instant Client que é usado pelo Serviço Oracle CDC.|  
|use_windows_authentication|Um valor booliano que pode ser:<br /><br /> **0**: um nome de usuário da Oracle e senha é fornecida para autenticação (o padrão)<br /><br /> **1**: a autenticação do Windows é usada para conectar ao banco de dados da Oracle. Você só poderá usar esta opção se o banco de dados Oracle estiver configurado para funcionar com autenticação do Windows.|  
|username|O nome do usuário do banco de dados de mineração de logs da Oracle. Isso só será obrigatório se **use_windows_authentication = 0**.|  
|password|A senha para o usuário do banco de dados de mineração de logs da Oracle. Isso só será obrigatório se **use_windows_authentication = 0**.|  
|transaction_staging_timeout|O tempo, em segundos, que uma transação do Oracle não confirmada é mantida na memória antes de ser gravada na tabela **cdc.xdbcdc_staged_transactions** . O padrão é 120 segundos.|  
|memory_limit|O limite na quantidade de memória, em Mb que pode ser usado para armazenar dados em cache na memória. Uma configuração inferior faz mais transações serem gravadas na tabela **cdc.xdbcdc_staged_transactions** . O padrão é 50 Mb.|  
|opções|Uma lista de opções na forma de name[=value][; ] - é usada para especificar opções secundárias (por exemplo, rastreamento, ajuste). Consulte a tabela abaixo para obter uma descrição das opções disponíveis.|  
  
 A tabela a seguir descreve as opções disponíveis.  
  
|Nome|Padrão|Mín|Max|Estático|Descrição|  
|----------|-------------|---------|---------|------------|-----------------|  
|rastreamento|Falso|-|-|Falso|Os valores disponíveis são:<br /><br /> True<br /><br /> Falso<br /><br /> on<br /><br /> off|  
|cdc_update_state_interval|10|1|120|Falso|O tamanho (em Kbytes) de partes de memória alocadas para uma transação (uma transação pode alocar mais de uma parte). Consulte a coluna memory_limit na tabela [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config) .|  
|target_max_batched_transactions|100|1|1.000|True|O número máximo de transações do Oracle que podem ser processadas como uma transação na atualização de tabelas do SQL Server CT.|  
|target_idle_lsn_update_interval|10|0|1|Falso|O intervalo (em segundos) para atualizar a tabela **lsn_time_mapping** quando as tabelas capturadas não têm nenhuma atividade.|  
|trace_retention_period|24|1|24*31|Falso|A quantidade de tempo (em horas para manter mensagens na tabela de rastreamento).|  
|sql_reconnect_interval|2|2|3600|Falso|A quantidade de tempo (em segundos) a esperar antes de reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este intervalo é usado além do tempo limite de conexão do cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|sql_reconnect_limit|-1|-1|-1|Falso|O número máximo de reconexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O padrão -1 significa que o processo tenta se reconectar até parar.|  
|cdc_restart_limit|6|-1|3600|Falso|Na maioria dos casos, o serviço CDC reinicia automaticamente uma instância CDC terminada de maneira anormal. Esta propriedade define depois de quantas falhas por hora o serviço para reiniciar a instância. O valor -1 significa que a instância sempre deve ser reiniciada.<br /><br /> O Serviço retorna para reiniciar a instância depois de qualquer atualização da tabela de configuração.|  
|cdc_memory_report|0|0|1.000|Falso|Se o valor do parâmetro foi alterado, a Instância CDC imprimirá seu relatório de memória na tabela de rastreamento.|  
|target_command_timeout|600|1|3600|Falso|O tempo limite de comando ao trabalhar com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|source_character_set|-|-|-|True|Pode ser definido como uma codificação de Oracle específica a ser usada em vez da página de código de banco de dados Oracle. Isto pode ser útil quando a codificação real que os dados de caractere estão usando é diferente de uma expressa pela página de código de banco de dados Oracle.|  
|source_error_retry_interval|30|1|3600|Falso|Usado antes de tentar novamente vários erros como erro de conexão ou falta temporária de sincronização entre tabelas do sistema.|  
|source_prefetch_size|100|1|10.000|True|Tamanho do lote de pré-busca.|  
|source_max_tables_in_query|100|1|10.000|True|Número máximo de tabelas na cláusula WHERE antes de alternar para a leitura do log do Oracle sem filtragem de tabela.|  
|source_read_retry_interval|2|1|3600|Falso|A quantidade de tempo que a origem aguarda antes de tentar ler os logs de transação do Oracle no EOF novamente.|  
|source_reconnect_interval|30|1|3600|Falso|Quanto tempo aguardar (em segundos) antes de tentar reconectar-se ao banco de dados de origem.|  
|source_reconnect_limit|-1|-1||Falso|O número máximo de reconexões do banco de dados de origem. O padrão -1 significa que o processo tenta se reconectar até ser parado.|  
|source_command_timeout|30|1|3600|Falso|O tempo limite de conexão ao trabalhar com Oracle.|  
|source_connection_timeout|30|1|3600|Falso|O tempo limite de conexão ao trabalhar com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|trace_data_errors|True|-|-|Falso|Booliano. **True** indica registro em log de erros de conversão de dados e de truncamento.|  
|CDC_stop_on_breaking_schema_changes|Falso|-|-|Falso|Booliano. **True** indica parada quando a quebra de esquema é detectada.<br /><br /> **False** indica remoção da tabela de espelho e instância de captura.|  
|source_oracle_home||-|-|Falso|Pode ser definido como um caminho específico do Oracle Home ou um Nome do Oracle Home que a instância CDC usará para conectar-se ao Oracle.|  
  
###  <a name="BKMK_cdcxdbcdc_state"></a> cdc.xdbcdc_state  
 Esta tabela contém informações sobre o estado persistido da Instância do Oracle CDC. O estado de captura é usado em cenários de recuperação e failover e para monitoramento de integridade.  
  
 A tabela a seguir descreve as colunas da tabela **cdc.xdbcdc_state** .  
  
|Item|Descrição|  
|----------|-----------------|  
|status|O código do status atual para a Instância do Oracle CDC atual. O status descreve o estado atual para o CDC.|  
|sub_status|Um segundo status de nível que fornece informações adicionais sobre o status atual.|  
|active|Um valor booliano que pode ser:<br /><br /> **0**: o processo de Instância do Oracle CDC não está ativo.<br /><br /> **1**: o processo de Instância do Oracle CDC está ativo.|  
|erro|Um valor booliano que pode ser:<br /><br /> **0**: o processo de Instância do Oracle CDC não está em um estado de erro.<br /><br /> **1**: a Instância do Oracle CDC está em um estado de erro.|  
|status_message|Uma cadeia de caracteres que fornece uma descrição do erro ou status.|  
|timestamp|O carimbo de data/hora com a hora (UTC) da última atualização do estado de captura.|  
|active_capture_node|O nome do host (o host pode ser um nó em um cluster) que está executando o Serviço Oracle CDC no momento e a Instância do Oracle CDC (que está processando os logs de transação do Oracle).|  
|last_transaction_timestamp|Um carimbo de data/hora com a hora (UTC) da última transação que foi gravada nas tabelas de alteração.|  
|last_change_timestamp|Um carimbo de data/hora com a hora (UTC) em que o registro de alteração mais recente foi lido do log de transação do Oracle de origem. Este carimbo de data/hora ajuda a identificar a latência atual do processo de CDC.|  
|transaction_log_head_cn|O número de alteração (CN) mais recente lido do log de transação do Oracle.|  
|transaction_log_tail_cn|O número de alteração (CN) no log de transação do Oracle onde estão as reposições da Instância do Oracle CDC no caso de uma reinicialização ou recuperação.|  
|current_cn|O número de alteração (CN) mais recente conhecido para estar no banco de dados de origem.|  
|software_version|A versão interna do Serviço Oracle CDC.|  
|completed_transactions|O número de transações processadas desde que o CDC foi reiniciado pela última vez.|  
|written_changes|O número de registros de alteração gravados nas tabelas de alteração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|read_changes|O número de registros de alteração lidos do log de transação do Oracle de origem.|  
|staged_transactions|O número de transações ativas no momento que estão preparadas na tabela **cdc.xdbcdc_staged_transactions** .|  
  
###  <a name="BKMK_cdcxdbcdc_trace"></a> cdc.xdbcdc_trace  
 Essa tabela contém informações sobre a operação da instância CDC. As informações armazenadas nesta tabela incluem registros de erro, alterações de status notáveis e registros de rastreamento. As informações de erro também serão gravadas no log de eventos do Windows para garantir que as informações estejam disponíveis se a tabela **cdc.xcbcdc_trace** não estiver disponível.  
  
 A tabela a seguir descreve as colunas da tabela cdc.xdbcdc_trace.  
  
|Item|Descrição|  
|----------|-----------------|  
|timestamp|O carimbo de data/hora UTC exato quando o registro de rastreamento foi gravado.|  
|tipo|Contém um dos seguintes valores.<br /><br /> erro<br /><br /> INFO<br /><br /> rastreamento|  
|nó|O nome do nó no qual o registro foi gravado.|  
|status|O código de status que é usado pela tabela de estado.|  
|sub_status|O código de substatus que é usado pela tabela de estado.|  
|status_message|A mensagem de status que é usada pela tabela de estado.|  
|data|Os dados adicionais para casos em que o erro ou registro de rastreamento contém uma carga (por exemplo, um registro de log corrompido).|  
  
###  <a name="BKMK_cdcxdbcdc_staged_transactions"></a> cdc.xdbcdc_staged_transactions  
 Esta tabela armazena registros de alteração para transações grandes ou longas até a confirmação de transação ou evento de reversão ser capturada. As ordens de Serviço Oracle CDC capturaram registros de log antes de hora de confirmação de transação e, em seguida, por ordem cronológica para cada transação. Os registros de log para a mesma transação são armazenados na memória até que a transação termine e, em seguida, seja gravada na tabela de alteração de destino ou descartada (no caso de uma reversão). Como há uma quantidade limitada de memória disponível, as transações grandes são gravadas na tabela **cdc.xdbcdc_staged_transactions** até que a transação esteja completa. As transações também são gravadas na tabela de preparação quando elas estiverem sendo executadas por muito tempo. Portanto, quando a Instância do Oracle CDC for reiniciada, as alterações antigas não precisarão ser relidas dos logs de transação do Oracle.  
  
 A tabela a seguir descreve as colunas da tabela **cdc.xdbcdc_staged_transactions** .  
  
|Item|Descrição|  
|----------|-----------------|  
|transaction_id|O identificador exclusivo da transação que está sendo preparada.|  
|seq_num|O número de linha **xcbcdc_staged_transactions** para a transação atual (começando com 0).|  
|data_start_cn|O número de alteração (CN) para a primeira alteração nos dados nesta linha.|  
|data_end_cn|O número de alteração (CN) para a última alteração nos dados nesta linha.|  
|data|As alterações preparadas para a transação no formato de um BLOB.|  
  
## <a name="see-also"></a>Consulte Também  
 [Change Data Capture Designer para Oracle da Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)  
  
  
