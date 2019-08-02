---
title: Eventos estendidos para monitoramento de processos de R e Python
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8dc99a6f5ac1ff660f34f2248c844e5386bea5f0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715131"
---
# <a name="extended-events-for-sql-server-machine-learning-services"></a>Eventos estendidos para SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O SQL Server fornece um conjunto de eventos estendidos para usar em operações de solução de [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]problemas relacionadas ao, bem como aos trabalhos do Python [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou do R enviados ao.

**Aplica-se a:**  SQL Server serviços de 2016, SQL Server Serviços de Machine Learning

## <a name="sql-server-events-for-machine-learning"></a>SQL Server eventos para aprendizado de máquina

Para exibir uma lista de eventos relacionados ao SQL Server, execute a seguinte consulta no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```sql
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

Para obter informações gerais sobre como usar eventos estendidos, consulte [ferramentas de eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).

> [!TIP]
> Para o evento estendido gerado por SQL Server, experimente o novo [criador de perfil de XEvent do SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/use-the-ssms-xe-profiler). Esse novo recurso no Management Studio exibe um visualizador ao vivo para eventos estendidos e é menos invasivo para a SQL Server do que um rastreamento de criador de perfil semelhante.

## <a name="additional-events-specific-to-machine-learning-components"></a>Eventos adicionais específicos para componentes de aprendizado de máquina

Eventos estendidos adicionais estão disponíveis para os componentes relacionados ao e usados pelo SQL Server serviços de Machine Learning, como o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]e o BXLServer, o processo de satélite que inicia o tempo de execução de R. Esses eventos estendidos adicionais são acionados dos processos externos e, portanto, devem ser capturados usando um utilitário externo.

Para obter mais informações sobre como fazer isso, consulte a seção [coletando eventos de processos externos](#bkmk_externalevents).

##  <a name="bkmk_xeventtable"></a>Tabela de eventos estendidos

|evento|Descrição|Observações|  
|-----------|-----------------|---------|  
|connection_accept|Ocorre quando uma nova conexão é aceita. Este evento serve para registrar todas as tentativas de conexão.||  
|failed_launching|Falha na inicialização.|Indica um erro.|  
|satellite_abort_connection|Cancelar o registro da conexão||  
|satellite_abort_received|Acionado quando uma mensagem de cancelamento é recebida por meio de uma conexão por satélite.||  
|satellite_abort_sent|Acionado quando uma mensagem de cancelamento é enviada por meio de uma conexão por satélite.||  
|satellite_authentication_completion|Acionado quando uma autenticação é concluída para uma conexão sobre TCP ou Pipe nomeado.||  
|satellite_authorization_completion|Acionado quando uma autorização é concluída para uma conexão sobre TCP ou Pipe nomeado.||  
|satellite_cleanup|Acionado durante a limpeza das chamadas por satélite.|Acionado somente a partir de processo externo. Confira instruções sobre a coleta de eventos a partir de processos externos.|  
|satellite_data_chunk_sent|Acionado quando a conexão por satélite conclui o envio de uma única parte de dados.|O evento informa o número de linhas enviadas, o número de colunas, o número de pacotes SNI utilizados e o tempo decorrido durante o envio da parte, em milissegundos. As informações podem ajudá-lo a compreender quanto tempo é gasto para passar diferentes tipos de dados e quantos pacotes são usados.|  
|satellite_data_receive_completion|Acionado quando todos os dados necessários de uma consulta são recebidos por meio de uma conexão por satélite.|Acionado somente a partir de processo externo. Confira instruções sobre a coleta de eventos a partir de processos externos.|  
|satellite_data_send_completion|Acionado quando todos os dados necessários de uma sessão são enviados por meio de uma conexão por satélite.||  
|satellite_data_send_start|Dispara quando a transmissão de dados é iniciada.| A transmissão de dados começa logo antes da primeira parte de dados ser enviada.|  
|satellite_error|Usado para rastreamento de erro de satélite do SQL||  
|satellite_invalid_sized_message|O tamanho da mensagem não é válido||  
|satellite_message_coalesced|Usado para rastreamento de união de mensagens em camada de rede||  
|satellite_message_ring_buffer_record|Registro de buffer de anéis de mensagem||  
|satellite_message_summary|Informações resumidas sobre mensagens||  
|satellite_message_version_mismatch|O campo de versão da mensagem não é correspondente||  
|satellite_messaging|Usado para evento de rastreamento de mensagens (associar, desassociar, etc.)||  
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
|satellite_sessionId_mismatch|ID de sessão da mensagem não é esperada||  
  
###  <a name="bkmk_externalevents"></a>Coletando eventos de processos externos

SQL Server Serviços de Machine Learning inicia alguns serviços que são executados fora do processo de SQL Server. Para capturar eventos relacionados a esses processos externos, você deve criar um arquivo de configuração de rastreamento de eventos e colocá-lo no mesmo diretório que o executável para o processo.  
  
+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    Para capturar eventos relacionados ao Launchpad, coloque o arquivo *.config* no diretório Binn da instância do SQL Server.  Em uma instalação padrão, isso seria:

    `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`.  
  
+ **BXLServer** é o processo de satélite que dá suporte à EXTENSIBILIDADE do SQL com linguagens de script externas, como R ou Python. Uma instância separada de BxlServer é iniciada para cada instância de linguagem externa.
  
    Para capturar eventos relacionados ao BXLServer, coloque o arquivo *. config* no diretório de instalação do R ou do Python.  Em uma instalação padrão, isso seria:
     
    **R:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  

    **Python:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\library\RevoScaleR\rxLibs\x64`.

O arquivo de configuração deve ter o mesmo nome do executável, usando o formato "[name]. XEvents. xml". Em outras palavras, os arquivos devem ser nomeados da seguinte forma:

+ `Launchpad.xevents.xml`
+ `bxlserver.xevents.xml`

O arquivo de configuração tem o seguinte formato:

```xml
\<?xml version="1.0" encoding="utf-8"?>  
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

+ Para configurar o rastreamento, edite o espaço reservado do *nome da sessão* , o espaço`[SessionName].xel`reservado para o nome do arquivo () e os nomes dos eventos que você deseja `[XEvent Name 1]`capturar `[XEvent Name 1]`, por exemplo,,).  
+ Qualquer número de marcas de pacote de eventos pode aparecer e será coletado, desde que o atributo de nome esteja correto.

### <a name="example-capturing-launchpad-events"></a>Exemplo: Capturando eventos Launchpad

O exemplo a seguir mostra a definição de um rastreamento de eventos para o serviço Launchpad:

```xml
\<?xml version="1.0" encoding="utf-8"?>  
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

+ Coloque o arquivo *.config* no diretório Binn da instância do SQL Server.
+ Esse arquivo deve ser nomeado `Launchpad.xevents.xml`.

### <a name="example-capturing-bxlserver-events"></a>Exemplo: Capturando eventos BXLServer  

O exemplo a seguir mostra a definição de um rastreamento de eventos para o executável BXLServer.
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
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

+ Coloque o arquivo *.config* no mesmo diretório que o executável BXLServer.
+ Esse arquivo deve ser nomeado `bxlserver.xevents.xml`.

## <a name="see-also"></a>Confira também

[Relatórios de Management Studio personalizados para Serviços de Machine Learning](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
