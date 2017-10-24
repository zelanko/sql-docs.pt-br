---
title: Eventos estendidos para o SQL Server R Services | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 11/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4e90e057-aacb-4adc-8da6-64861f4e87df
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 814dacf2dbc7f3be05ad163c8c7162acf53fe404
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="extended-events-for-sql-server-r-services"></a>Eventos Estendidos do SQL Server R Services
  O[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece um conjunto de Eventos Estendidos para usar nas operações de solução de problemas relacionados aos trabalhos do [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] ou de R enviados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para exibir uma lista de eventos relacionados ao SQL Server, execute a seguinte consulta no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
```  
select o.name as event_name, o.description  
  from sys.dm_xe_objects o  
  join sys.dm_xe_packages p  
    on o.package_guid = p.guid  
 where o.object_type = 'event'  
   and p.name = 'SQLSatellite';  
```  
  
 No entanto, alguns Eventos Estendidos adicionais do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] são acionados somente a partir de processos externos, como o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]e o BXLServer, o processo de satélite que inicia o tempo de execução de R. Para saber mais sobre como captar esses eventos, confira o tópico [Collecting Events from External Processes](#bkmk_externalevents).  
  
 Para obter informações gerais sobre o uso de Eventos Estendidos, confira o artigo [SQL Server Extended Events Sessions](../../relational-databases/extended-events/sql-server-extended-events-sessions.md).  

  
##  <a name="bkmk_xeventtable"></a> Tabela de Eventos Estendidos  
  
|Evento|Descrição|Use|  
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
|satellite_data_send_start|Acionado quando a transmissão de dados é iniciada, logo após o envio da primeira parte de dados.||  
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
  
###  <a name="bkmk_externalevents"></a> Collecting Events from External Processes  
 O[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] inicia alguns serviços que são executados fora dos processos do SQL Server. Para captar eventos relacionados a esses processos externos, você deve criar um arquivo de configuração de rastreamento de eventos e colocá-lo no mesmo diretório do executável do processo.  
  
-   **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
     Para capturar eventos relacionados ao Launchpad, coloque o arquivo *.config* no diretório Binn da instância do SQL Server.  Em uma instalação padrão, seria: `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`.  
  
-   O **BXLServer** é o processo satélite que dá suporte à extensibilidade do SQL com o R e com outras linguagens de script externo.  
  
     Para capturar eventos relacionados ao BXLServer, coloque o arquivo *.config* no diretório de instalação do R.  Em uma instalação padrão, seria: `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  
  
> [!IMPORTANT]
>   O arquivo de configuração deve ter o mesmo nome do executável, usando o formato "[nome].xevents.xml". Em outras palavras, os arquivos devem ser nomeados da seguinte forma:  
>   
> - Launchpad.xevents.xml  
> - bxlserver.xevents.xml  
  
 O arquivo de configuração tem o seguinte formato:  
  
```  
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
  
 **Observações:**  
  
-   Para configurar o rastreamento, edite o espaço reservado *nome da sessão*, o espaço reservado para o nome do arquivo (`[SessionName].xel`) e os nomes dos eventos que deseja capturar (como `[XEvent Name 1]`, `[XEvent Name 1]`).  
  
-   Várias marcas `event package` podem ser exibidas e serão coletadas, desde que o atributo de nome esteja correto.  
  
### <a name="example-capturing-launchpad-events"></a>Exemplo: captando eventos do Launchpad  
 O exemplo a seguir mostra a definição de um rastreamento de eventos para o serviço do Launchpad.  
  
```  
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
  
 **Observações:**  
  
-   Coloque o arquivo *.config* no diretório Binn da instância do SQL Server.  
  
-   Este arquivo deve ser nomeado como *Launchpad.xevents.xml*.  
  
### <a name="example-capturing-bxlserver-events"></a>Exemplo: captando eventos do BXLServer  
 O exemplo a seguir mostra a definição de um rastreamento de eventos para o executável BXLServer.  
  
```  
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
  
 **Observações:**  
  
-   Coloque o arquivo *.config* no mesmo diretório que o executável BXLServer.  
  
-   Este arquivo deve ser nomeado como *bxlserver.xevents.xml*.  
  
## <a name="see-also"></a>Consulte também
[Relatórios personalizados do Management Studio para o R Services](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Gerenciando e monitorando soluções de R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
  

