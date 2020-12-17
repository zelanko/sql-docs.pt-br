---
title: Monitorar scripts com eventos estendidos
description: Saiba como usar eventos estendidos para monitorar e solucionar problemas de operações relacionadas aos scripts externos de trabalhos nos Serviços de Machine Learning do SQL Server, no SQL Server Launchpad, no Python ou no R.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/04/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: 2cd28eaa17a52e0e0ae525f5977dbd5f6a26bf64
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471357"
---
# <a name="monitor-python-and-r-scripts-with-extended-events-in-sql-server-machine-learning-services"></a>Monitorar scripts do Python e do R com eventos estendidos nos Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

Saiba como usar eventos estendidos para monitorar e solucionar problemas de operações relacionadas aos scripts externos de trabalhos nos Serviços de Machine Learning do SQL Server, no SQL Server Launchpad, no Python ou no R.

## <a name="extended-events-for-sql-server-machine-learning-services"></a>Eventos estendidos para os Serviços de Machine Learning do SQL Server

Para exibir uma lista de eventos relacionados aos Serviços de Machine Learning do SQL Server, execute a consulta a seguir no Azure Data Studio ou no SQL Server Management Studio.

```sql
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

Para saber mais sobre como usar eventos estendidos, confira [Ferramentas de eventos estendidos](../../relational-databases/extended-events/extended-events-tools.md).

## <a name="additional-events-specific-to-machine-learning-services"></a>Eventos adicionais específicos para os Serviços de Machine Learning

Os eventos estendidos adicionais estão disponíveis para os componentes relacionados e usados pelos Serviços de Machine Learning do SQL Server, como o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], o BXLServer e o processo de satélite que inicia o runtime do Python ou do R. Esses eventos estendidos adicionais são acionados nos processos externos. Portanto, eles devem ser capturados com um utilitário externo.

Para saber mais sobre como fazer isso, confira a seção [Coletar eventos de processos externos](#bkmk_externalevents).

<a name="bkmk_xeventtable"></a> 

## <a name="table-of-extended-events"></a>Tabela de eventos estendidos

|Evento|Descrição|Observações|  
|-----------|-----------------|---------|  
|connection_accept|Ocorre quando uma nova conexão é aceita. Este evento serve para registrar todas as tentativas de conexão.||  
|failed_launching|Falha na inicialização.|Indica um erro.|  
|satellite_abort_connection|Cancelar o registro da conexão||  
|satellite_abort_received|Acionado quando uma mensagem de cancelamento é recebida por meio de uma conexão por satélite.||  
|satellite_abort_sent|Acionado quando uma mensagem de cancelamento é enviada por meio de uma conexão por satélite.||  
|satellite_authentication_completion|Acionado quando uma autenticação é concluída para uma conexão via TCP ou pipe nomeado.||  
|satellite_authorization_completion|Acionado quando uma autorização é concluída para uma conexão via TCP ou pipe nomeado.||  
|satellite_cleanup|Acionado durante a limpeza das chamadas por satélite.|Acionado somente a partir de processo externo. Confira instruções sobre a coleta de eventos a partir de processos externos.|  
|satellite_data_chunk_sent|Acionado quando a conexão por satélite conclui o envio de uma única parte de dados.|O evento informa o número de linhas enviadas, o número de colunas, o número de pacotes SNI utilizados e o tempo decorrido durante o envio da parte, em milissegundos. As informações podem ajudá-lo a compreender quanto tempo é gasto para passar diferentes tipos de dados e quantos pacotes são usados.|  
|satellite_data_receive_completion|Acionado quando todos os dados necessários de uma consulta são recebidos por meio de uma conexão por satélite.|Acionado somente a partir de processo externo. Confira instruções sobre a coleta de eventos a partir de processos externos.|  
|satellite_data_send_completion|Acionado quando todos os dados necessários de uma sessão são enviados por meio de uma conexão por satélite.||  
|satellite_data_send_start|Dispara quando a transmissão de dados é iniciada.| A transmissão de dados começa logo antes da primeira parte dos dados ser enviada.|  
|satellite_error|Usado para rastreamento de erro de satélite do SQL||  
|satellite_invalid_sized_message|O tamanho da mensagem não é válido||  
|satellite_message_coalesced|Usado para rastreamento de união de mensagens em camada de rede||  
|satellite_message_ring_buffer_record|Registro de buffer de anéis de mensagem||  
|satellite_message_summary|Informações resumidas sobre mensagens||  
|satellite_message_version_mismatch|O campo de versão da mensagem não é correspondente||  
|satellite_messaging|Usado para evento de rastreamento de mensagens (associar, desassociar etc.)||  
|satellite_partial_message|Usado para rastreamento de mensagens parciais em camada de rede||  
|satellite_schema_received|Acionado quando o esquema de mensagens é recebido e lido pelo SQL.||  
|satellite_schema_sent|Acionado quando o esquema de mensagens é enviado pelo satélite.|Acionado somente a partir de processo externo. Confira instruções sobre a coleta de eventos a partir de processos externos.|  
|satellite_service_start_posted|Acionado quando a mensagem de início do serviço é postada no Launchpad.|Informa ao Launchpad que deve iniciar o processo externo e contém a ID da nova sessão.|  
|satellite_unexpected_message_received|Acionado quando uma mensagem inesperada é recebida.|Indica um erro.|  
|stack_trace|Ocorre quando o despejo de memória do processo é solicitado.|Indica um erro.|  
|trace_event|Usado para fins de rastreamento|Esses eventos podem incluir o SQL Server, o Launchpad e o rastreamento de processos externos. Isso inclui as saídas stdout e stderr de R.|  
|launchpad_launch_start|Acionado quando o Launchpad começa a inicializar um satélite.|Acionado somente a partir do Launchpad. Confira instruções sobre a coleta de eventos a partir do arquivo launchpad.exe.|  
|launchpad_resume_sent|Acionado quando o Launchpad inicializa o satélite e envia uma mensagem resumida para o SQL Server.|Acionado somente a partir do Launchpad. Confira instruções sobre a coleta de eventos a partir do arquivo launchpad.exe.|  
|satellite_data_chunk_sent|Acionado quando a conexão por satélite conclui o envio de uma única parte de dados.|Contém informações sobre o número de colunas, de linhas, de pacotes e o tempo decorrido com o envio das partes.|  
|satellite_sessionId_mismatch|A ID da sessão da mensagem não é esperada||  

<a name="bkmk_externalevents"></a>

### <a name="collecting-events-from-external-processes"></a>Coletar eventos de processos externos

Os Serviços de Machine Learning do SQL Server iniciam alguns serviços que são executados fora do processo do SQL Server. Para capturar eventos relacionados a esses processos externos, você deve criar um arquivo de configuração de rastreamento de eventos e colocá-lo no mesmo diretório do executável do processo.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
> [!IMPORTANT]
> A partir do SQL Server 2019, o mecanismo de isolamento foi alterado. Portanto, você precisa fornecer as permissões apropriadas para o diretório no qual o arquivo de configuração de rastreamento de eventos está armazenado. Para obter mais informações sobre como definir essas permissões, confira [a seção Permissões de arquivo em SQL Server 2019 no Windows: alterações de isolamento nos Serviços de Machine Learning](../install/sql-server-machine-learning-services-2019.md#file-permissions).
::: moniker-end

+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    Para capturar eventos relacionados ao Launchpad, coloque o arquivo *.xml* no diretório Binn da instância do SQL Server. Em uma instalação padrão, seria:

    `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`.  
  
+ O **BXLServer** é o processo de satélite compatível com a extensibilidade do SQL com linguagens de script externo, como R ou Python. Uma instância separada do BxlServer será iniciada para cada instância de linguagem externa.
  
    Para capturar eventos relacionados ao BXLServer, coloque o arquivo *.xml* no diretório de instalação do R ou do Python. Em uma instalação padrão, seria:
     
    **R:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  

    **Python:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\rxLibs`.

O arquivo de configuração deve ter o mesmo nome do executável, usando o formato "[nome].xevents.xml". Em outras palavras, os arquivos devem ser nomeados da seguinte forma:

+ `Launchpad.xevents.xml`
+ `bxlserver.xevents.xml`

O arquivo de configuração tem o seguinte formato:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="[session name]" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="you">Xevent for launchpad or bxl server.</description>  
    <event package="SQLSatellite" name="[XEvent Name 1]" />  
    <event package="SQLSatellite" name="[XEvent Name 2]" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="[SessionName].xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Para configurar o rastreamento, edite o espaço reservado *nome da sessão*, o espaço reservado para o nome do arquivo (`[SessionName].xel`) e os nomes dos eventos que deseja capturar (como `[XEvent Name 1]`, `[XEvent Name 1]`).  
+ Várias marcas do pacote do evento podem ser exibidas e serão coletadas, desde que o atributo de nome esteja correto.

### <a name="example-capturing-launchpad-events"></a>Exemplo: Capturar eventos do Launchpad

O exemplo a seguir mostra a definição de um rastreamento de eventos para o serviço do Launchpad:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="launchpad_launch_start" />  
    <event package="SQLSatellite" name="launchpad_resume_sent" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="launchpad_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Coloque o arquivo *.xml* no diretório Binn da instância do SQL Server.
+ Esse arquivo deve ser nomeado `Launchpad.xevents.xml`.

### <a name="example-capturing-bxlserver-events"></a>Exemplo: Capturar eventos do BXLServer  

O exemplo a seguir mostra a definição de um rastreamento de eventos para o executável BXLServer.
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
 <event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="satellite_abort_received" />  
    <event package="SQLSatellite" name="satellite_authentication_completion" />  
    <event package="SQLSatellite" name="satellite_cleanup" />  
    <event package="SQLSatellite" name="satellite_data_receive_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_start" />  
    <event package="SQLSatellite" name="satellite_schema_sent" />   
    <event package="SQLSatellite" name="satellite_unexpected_message_received" />    
    <event package="SQLSatellite" name="satellite_data_chunk_sent" />   
    <target package="package0" name="event_file">  
      <parameter name="filename" value="satellite_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Coloque o arquivo *.xml* no mesmo diretório que o executável BXLServer.
+ Esse arquivo deve ser nomeado `bxlserver.xevents.xml`.

## <a name="next-steps"></a>Próximas etapas

- [Monitorar a execução de script do Python e do R usando relatórios personalizados no SQL Server Management Studio](../../machine-learning/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [Monitorar os Serviços de Machine Learning do SQL Server usando DMVs (exibições de gerenciamento dinâmico)](../../machine-learning/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)