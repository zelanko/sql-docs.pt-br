---
title: "Acessar informações de diagnóstico no Log de eventos estendidos | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95ba6393a69eca1c5e4c235bc205438262186b21
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Acessar informações de diagnóstico nos logs de eventos estendidos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  No [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], o rastreamento ([operação do Driver de rastreamento](../../connect/jdbc/tracing-driver-operation.md)) foi atualizado para facilitar para correlacionar eventos do cliente com informações de diagnóstico, tais como falhas de conexão, de anéis de conectividade do servidor informações de desempenho de aplicativo e o buffer no log de eventos estendidos. Para obter mais informações sobre como ler o log de eventos estendidos, consulte [View Event Session Data](http://msdn.microsoft.com/library/hh710068(SQL.110).aspx).  
  
## <a name="details"></a>Detalhes  
 Para operações de conexão, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enviará um cliente ID de conexão. Se a conexão falhar, você poderá acessar o buffer de anéis de conectividade ([Solução de problemas de conectividade no SQL Server 2008 com o Buffer de Anéis de Conectividade](http://go.microsoft.com/fwlink/?LinkId=207752)) e localizar o campo **ClientConnectionID** e poderá obter informações de diagnóstico sobre a falha de conexão. As IDs de conexão de cliente estarão registradas no buffer de anéis se um erro ocorrer. (Se uma conexão falhar antes de enviar o pacote anterior ao logon, uma ID conexão de cliente não será gerada.) A ID de conexão de cliente é um GUID de 16 bytes. Você também pode encontrar a conexão de cliente ID na saída de destino de eventos estendidos, se o **client_connection_id** ação for adicionada aos eventos em uma sessão de eventos estendidos. Você pode habilitar o rastreamento e execute novamente o comando de conexão e observar o **ClientConnectionID** campo no rastreamento, se você precisar de mais assistência de diagnóstico de driver do cliente.  
  
 Você pode obter o cliente ID de conexão programaticamente usando [ISQLServerConnection Interface](../../connect/jdbc/reference/isqlserverconnection-interface.md). A ID de conexão também estará presente em todas as exceções relacionadas à conexão.  
  
 Quando há um erro de conexão, a ID de conexão do cliente nas informações de rastreamento BID do servidor e no buffer de anéis de conectividade pode ajudar a correlacionar as conexões do cliente às conexões no servidor. Para obter mais informações sobre BID rastreamentos no servidor, consulte [Data Access Tracing](http://go.microsoft.com/fwlink/?LinkId=125805). Observe que o artigo de rastreamento de acesso de dados também contém informações sobre como executar um rastreamento de acesso de dados não é válido para o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]; consulte [operação do Driver de rastreamento](../../connect/jdbc/tracing-driver-operation.md) para obter informações sobre como fazer um rastreamento de acesso de dados usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 O JDBC Driver também envia uma ID de atividade específica do thread. A ID da atividade será capturada nas sessões de eventos estendidas se as sessões forem iniciadas com a opção de TRACK_CAUSAILITY habilitada. Para problemas de desempenho com uma conexão ativa, você pode obter a ID de atividade do rastreamento do cliente (campo ActivityID) e localizar a ID de atividade na saída dos eventos estendidos. A ID de atividade nos eventos estendidos é um GUID de 16 bytes (não é o mesmo que o GUID da ID de conexão do cliente) com um número sequencial de quatro bytes. O número sequencial representa a ordem de uma solicitação de um thread. O ActivityId é enviado para instruções SQL em lotes e solicitações RPC. Para habilitar o envio de ActivityId ao servidor, você precisa especificar primeiro o par de valores chaves a seguir no arquivo Logging.Properties:  
  
```  
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 Qualquer valor diferente de `on` (diferencia maiusculas de minúsculas) desabilitará o envio de ActivityId.  
  
 Para obter mais informações, consulte [a operação de rastreamento do Driver](../../connect/jdbc/tracing-driver-operation.md). Esse sinalizador de rastreamento é usado com os agentes de objeto do JDBC correspondentes para decidir se haverá ou não o rastreamento e envio de ActivityId no JDBC driver. Além disso, para atualizar o arquivo Logging.Properties, o agente com.microsoft.sqlserver.jdbc precisa ser habilitado para FINER ou posterior. Se você desejar enviar ActivityId ao servidor para solicitações feitas por uma determinada classe, o agente da classe correspondente precisa ser habilitado para FINER ou FINEST. Por exemplo, se a classe SQLServerStatement habilita o agente com.microsoft.sqlserver.jdbc.SQLServerStatement.  
  
 A seguir está um exemplo que usa [!INCLUDE[tsql](../../includes/tsql_md.md)] para iniciar uma sessão de eventos estendidos que será armazenada em um buffer de anel e registrará a ID de atividade enviada de um cliente em operações em lote e RPC:  
  
```  
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
