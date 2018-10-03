---
title: Administrar e monitorar a captura de dados de alteração (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], monitoring
- change data capture [SQL Server], administering
- change data capture [SQL Server], jobs
ms.assetid: 23bda497-67b2-4e7b-8e4d-f1f9a2236685
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 619ec50247a2e3c5189b55f9243bb88d1a2b759b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057326"
---
# <a name="administer-and-monitor-change-data-capture-sql-server"></a>Administrar e monitorar a captura de dados de alteração (SQL Server)
  Este tópico descreve como administrar e monitorar a captura de dados de alterações.  
  
##  <a name="Capture"></a> Trabalho de captura  
 O trabalho de captura é iniciado com a execução do procedimento armazenado sem-parâmetros `sp_MScdc_capture_job`. Esse procedimento armazenado é iniciado com a extração de valores configurados para *maxtrans*, *maxscans*, *continuous*e *pollinginterval* para o trabalho de captura de msdb.dbo.cdc_jobs. Eles configurado valores são passados como parâmetros para o procedimento armazenado `sp_cdc_scan`. Isso é usado para invocar `sp_replcmds` para executar a verificação de log.  
  
### <a name="capture-job-parameters"></a>Capturar parâmetros de trabalho  
 Para entender o comportamento do trabalho de captura, você deve entender como os parâmetros configuráveis são usados pelo `sp_cdc_scan`.  
  
#### <a name="maxtrans-parameter"></a>Parâmetro maxtrans  
 O parâmetro *maxtrans* especifica o número máximo de transações que podem ser processadas em um único ciclo de verificação do log. Se, durante a verificação, o número de transações a serem processadas alcançar esse limite, nenhuma transação adicional será incluída na verificação atual. Após a conclusão de um ciclo de verificação, o número de transações que foram processadas sempre será menor ou igual ao *maxtrans*.  
  
#### <a name="maxscans-parameter"></a>Parâmetro maxscans  
 O parâmetro *maxscans* especifica o número máximo de ciclos de verificação que tentaram esgotar o log antes de retornar (continuous = 0) ou executar waitfor (continuous = 1).  
  
#### <a name="continous-parameter"></a>Parâmetro continous  
 O *contínua* parâmetro controla se `sp_cdc_scan` cede o controle após esgotar o log ou executar o número máximo de ciclos de verificação (modo monoestável). Ele também define se `sp_cdc_scan` continua sendo executado até ser interrompido explicitamente (modo contínuo).  
  
##### <a name="one-shot-mode"></a>Modo mono estável  
 No modo monoestável, o trabalho de captura solicita `sp_cdc_scan` execute até *maxtrans* verificações para tentar esgotar o log e retornar. Qualquer transação além de *maxtrans* presente no log será processada nas verificações posteriores.  
  
 O modo monoestável é usado em testes controlados, nos quais o volume de transações a serem processadas é conhecido e há vantagens no fato de o trabalho fechar automaticamente quando concluído. O modo monoestável não é recomendado para uso de produção. Isso ocorre porque ele depende da agenda de trabalho para gerenciar a frequência com que o ciclo de verificação é executado.  
  
 Ao executar no modo monoestável, você pode calcular uma associação superior na taxa de transferência esperada do trabalho de captura, expressa nas transações por segundo usando o seguinte cálculo:  
  
 `(maxtrans * maxscans) / number of seconds between scans`  
  
 Mesmo que o tempo necessário para verificar o log e preencher as tabelas de alteração não seja significativamente diferente de 0, a taxa de transferência média do trabalho não deve exceder o valor obtido pela divisão do máximo de transações permitidas por uma verificação única multiplicada pelo máximo de transações permitidas pelo número de segundos entre o processamento do log.  
  
 Se o modo monoestável foi usado para verificação de log regular, o número de segundos entre o processamento de log deverá ser regido pela agenda do trabalho. Quando esse tipo de comportamento é desejado, executar o trabalho de captura no modo contínuo é um método melhor de gerenciar a reagenda da verificação de log.  
  
##### <a name="continuous-mode-and-the-polling-interval"></a>Modo contínuo e intervalo de sondagem  
 No modo contínuo, o trabalho de captura solicita `sp_cdc_scan` executado continuamente. Isso permite que o procedimento armazenado gerencie seu próprio loop de espera fornecendo não só maxtrans e maxscans, como também um valor para o número de segundos entre o processamento de log (o intervalo de sondagem). Quando executado nesse modo, o trabalho de captura permanece ativo, executando um `WAITFOR` verificação entre logs.  
  
> [!NOTE]  
>  Quando o valor do intervalo de sondagem é maior que 0, o mesmo limite superior na taxa de transferência do trabalho monoestável recorrente também se aplica à operação do trabalho no modo contínuo. Isto é, (*maxtrans* \* *maxscans*) dividido por um intervalo de sondagem diferente de zero colocará uma associação superior no número médio de transações que podem ser processadas pelo trabalho de captura.  
  
### <a name="capture-job-customization"></a>Personalização do trabalho de captura  
 Para o trabalho de captura, você pode aplicar lógica adicional para determinar se uma nova verificação é iniciada imediatamente ou se um estado suspenso é imposto antes do início de uma nova verificação, em vez de depender de um intervalo de sondagem fixo. A opção pode se basear simplesmente na hora do dia, talvez impondo estados suspensos muito longos durante horários de pico de atividade e até mudando para um intervalo de sondagem de 0 no fechamento do dia quando é importante concluir o processamento dos dias e preparar-se para as execuções noturnas. Também foi possível monitorar o andamento do processo de captura para determinar quando todas as transações confirmadas até meia-noite foram verificadas e depositadas em tabelas de alterações. Isso permite a reinicialização do trabalho de captura por uma reinicialização diária agendada após seu término. Ao substituir a etapa de trabalho entregue chamando `sp_cdc_scan` com uma chamada para um invólucro de usuário gravado para `sp_cdc_scan`, pode obter comportamento altamente personalizado com pouco esforço adicional.  
  
##  <a name="Cleanup"></a> Trabalho de limpeza  
 Esta seção fornece informações sobre como o trabalho de limpeza do Change Data Capture funciona.  
  
### <a name="structure-of-the-cleanup-job"></a>Estrutura do trabalho de limpeza  
 O Change Data Capture usa uma retenção com base na estratégia de limpeza para gerenciar o tamanho da tabela de alterações. O mecanismo de limpeza consiste em um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent [!INCLUDE[tsql](../../includes/tsql-md.md)] criado quando a primeira tabela de banco de dados é habilitada. Um único trabalho de limpeza trata da limpeza de todas as tabelas de alterações de bancos de dados e aplica o mesmo valor de retenção a todas as instâncias de captura definidas.  
  
 O trabalho de limpeza é iniciado com a execução do procedimento armazenado sem-parâmetros `sp_MScdc_cleanup_job`. Esse procedimento armazenado começa extraindo os valores de retenção e o limite configurados para o trabalho de limpeza de `msdb.dbo.cdc_jobs`. O valor de retenção é usado para calcular uma nova marca d'água baixa para as tabelas de alterações. O número especificado de minutos é abstraído do máximo *tran_end_time* o valor do `cdc.lsn_time_mapping` tabela para obter a nova marca d'água expressada como um valor de data e hora. A tabela CDC.lsn_time_mapping é usada para converter esse valor de data e hora em um valor correspondente de `lsn`. Se a mesma hora de confirmação for compartilhada por várias entradas na tabela, o `lsn` que corresponde à entrada com o menor `lsn` é escolhida como a nova marca d'água baixa. Esse valor de `lsn` é passado para `sp_cdc_cleanup_change_tables` para remover entradas da tabela de alterações de tabelas de alterações do banco de dados.  
  
> [!NOTE]  
>  A vantagem de usar a hora de confirmação da transação recente como base do cálculo da nova marca d'água baixa é que isso permite que as alterações permaneçam nas tabelas de alterações pelo tempo especificado. Isto ocorre até mesmo quando o processo de captura está sendo executado em segundo plano. Todas as entradas que têm a mesma hora de confirmação a marca d'água baixa continuam sendo representadas nas tabelas de alterações pela escolha do menor `lsn` que tem a hora de confirmação compartilhada para a marca d'água baixa real.  
  
 Quando uma limpeza é executada, a marca d'água baixa para todas as instâncias de captura é atualizada inicialmente em uma única transação. Ela tenta remover entradas obsoletas das tabelas de alterações e da tabela cdc.lsn_time_mapping. O valor limite configurável restringe a quantidade de entradas excluídas em qualquer instrução única. A não execução da exclusão de qualquer tabela individual não impedirá a tentativa de operação nas tabelas restantes.  
  
### <a name="cleanup-job-customization"></a>Personalização do trabalho de limpeza  
 Para o trabalho de limpeza, a possibilidade personalização está na estratégia usada para determinar quais entradas da tabela de alterações devem ser descartadas. A única estratégia com suporte no trabalho de limpeza entregue baseia-se na hora. Nessa situação, a nova marca d'água baixa é calculada pela subtração do período de retenção permitido da hora de confirmação da última transação processada. Como os procedimentos de limpeza subjacentes se baseiam no `lsn` em vez do tempo, qualquer número de estratégias pode ser usado para determinar o menor `lsn` manter nas tabelas de alteração. Somente alguns deles são estritamente baseados na hora. O conhecimento sobre os clientes, por exemplo, pode ser usado para fornecer um mecanismo seguro se não for possível executar os processos de downstream que requerem acesso às tabelas de alterações. Além disso, embora a estratégia padrão seja aplicável ao mesmo `lsn` para limpar as tabelas de alteração de todas as do banco de dados, o procedimento de limpeza subjacente também pode ser chamado para limpar no nível de instância de captura.  
  
##  <a name="Monitor"></a> Monitorar o processo de captura de dados de alterações  
 O monitoramento do processo de captura de dados de alteração permite determinar se as alterações estão sendo gravadas corretamente e com latência razoável nas tabelas de alteração. O monitoramento também pode ajudar a identificar os erros que podem ocorrer. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém duas exibições de gerenciamento dinâmico para ajudar a monitorar a captura de dados de alterações: [sys.dm_cdc_log_scan_sessions](../native-client-ole-db-data-source-objects/sessions.md) e [sys.dm_cdc_errors](../native-client-ole-db-errors/errors.md).  
  
### <a name="identify-sessions-with-empty-result-sets"></a>Identificar sessões com conjuntos de resultados vazios  
 Cada linha da exibição de gerenciamento sys.dm_cdc_log_scan_sessions representa uma sessão de verificação de log (exceto a linha que tem uma ID 0). Uma sessão de verificação de log é equivalente a uma execução de [sp_cdc_scan](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql). Durante uma sessão, a verificação pode retornar alterações ou um resultado vazio. Se o conjunto de resultados for vazio, a coluna empty_scan_count em sys.dm_cdc_log_scan_sessions será definida como 1. Se houver conjuntos de resultados vazios consecutivos, como se o trabalho de captura estivesse sendo executado continuamente, a coluna empty_scan_count na última linha existente será incrementada. Por exemplo, se sys.dm_cdc_log_scan_sessions já contém 10 linhas para verificações que retornaram alterações e se existem cinco conjuntos de resultados vazios em sequência, a exibição conterá 11 linhas. A última linha tem um valor de 5 na coluna empty_scan_count. Para determinar sessões que tiveram uma verificação vazia, execute a seguinte consulta:  
  
 `SELECT * from sys.dm_cdc_log_scan_sessions where empty_scan_count <> 0`  
  
### <a name="determine-latency"></a>Determinar a latência  
 A exibição de gerenciamento sys.dm_cdc_log_scan_sessions inclui uma coluna que registra a latência de cada sessão de captura. Latência é definida como o tempo decorrido entre uma transação que está sendo confirmada em uma tabela de origem e a última transação capturada que está sendo confirmada na tabela de alteração. A coluna de latência só é preenchida para sessões ativas. Para sessões com um valor maior que 0 na coluna empty_scan_count, a coluna de latência é definida como 0. A seguinte consulta retorna a latência média das sessões mais recentes:  
  
 `SELECT latency FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
 Você pode usar dados de latência para determinar a velocidade com que o processo de captura está processando as transações. Esses dados são muito úteis quando o processo de captura é executado continuamente. Se o processo de captura for executado segundo uma agenda, a latência poderá ser alta devido ao atraso entre a confirmação das transações na tabela de origem e a execução do processo de captura no horário agendado.  
  
 Outra medida importante que avalia a eficiência do processo de captura é a taxa de transferência. Representa o número médio de comandos por segundo que são processados durante cada sessão. Para determinar a taxa de transferência de uma sessão, divida o valor da coluna command_count pelo valor da coluna de duração. A seguinte consulta retorna a taxa de transferência média das sessões mais recentes:  
  
 `SELECT command_count/duration AS [Throughput] FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
### <a name="use-data-collector-to-collect-sampling-data"></a>Usar o coletor de dados para coletar dados de amostragem  
 O coletor de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite coletar instantâneos de dados de qualquer tabela ou exibição de gerenciamento dinâmico e criar um data warehouse de desempenho. Quando a captura de dados de alteração está habilitada em um banco de dados, ela é útil para obter instantâneos das exibições sys.dm_cdc_log_scan_sessions e sys.dm_cdc_errors em intervalos regulares para análise posterior. O procedimento a seguir configura um coletor de dados para coletar dados de amostra da exibição de gerenciamento sys.dm_cdc_log_scan_sessions.  
  
 **Configuração a coleta de dados**  
  
1.  Habilite o coletor de dados e configure um data warehouse de gerenciamento. Para obter mais informações, consulte [Gerenciar coleta de dados](../data-collection/data-collection.md).  
  
2.  Execute o código a seguir para criar um coletor personalizado para captura de dados de alteração.  
  
    ```tsql  
    USE msdb;  
  
    DECLARE @schedule_uid uniqueidentifier;  
  
    -- Collect and upload data every 5 minutes  
    SELECT @schedule_uid = (  
    SELECT schedule_uid from sysschedules_localserver_view   
    WHERE name = N'CollectorSchedule_Every_5min')  
  
    DECLARE @collection_set_id int;  
  
    EXEC dbo.sp_syscollector_create_collection_set  
    @name = N' CDC Performance Data Collector',  
    @schedule_uid = @schedule_uid,          
    @collection_mode = 0,                   
    @days_until_expiration = 30,                
    @description = N'This collection set collects CDC metadata',  
    @collection_set_id = @collection_set_id output;  
  
    -- Create a collection item using statistics from   
    -- the change data capture dynamic management view.  
    DECLARE @paramters xml;  
    DECLARE @collection_item_id int;  
  
    SELECT @paramters = CONVERT(xml,   
        N'<TSQLQueryCollector>  
            <Query>  
              <Value>SELECT * FROM sys.dm_cdc_log_scan_sessions</Value>  
              <OutputTable>cdc_log_scan_data</OutputTable>  
            </Query>  
          </TSQLQueryCollector>');  
  
    EXEC dbo.sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = N'302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @name = ' CDC Performance Data Collector',  
    @frequency = 5,   
    @parameters = @paramters,  
    @collection_item_id = @collection_item_id output;  
  
    GO  
    ```  
  
3.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Gerenciamento**e, em seguida, **Coleta de Dados**. Clique com o botão direito do mouse em **Coletor de Dados de Desempenho de CDC**e clique em **Iniciar Conjunto de Coleta de Dados**.  
  
4.  No data warehouse configurado na etapa 1, localize a tabela custom_snapshots.cdc_log_scan_data. Essa tabela fornece um instantâneo histórico dos dados das sessões de verificação de log. Esses dados podem ser usados para analisar a latência, a taxa de transferência e outras medidas de desempenho ao longo do tempo.  
  
## <a name="see-also"></a>Consulte também  
 [Controle de alterações de dados &#40;SQL Server&#41;](track-data-changes-sql-server.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../track-changes/about-change-data-capture-sql-server.md)   
 [Habilitar e desabilitar a captura de dados de alterações &#40;SQL Server&#41;](enable-and-disable-change-data-capture-sql-server.md)   
 [Trabalhar com dados de alterações &#40;SQL Server&#41;](work-with-change-data-sql-server.md)  
  
  
