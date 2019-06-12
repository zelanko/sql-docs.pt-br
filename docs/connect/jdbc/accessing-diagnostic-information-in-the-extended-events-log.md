---
title: Acessando informações de diagnóstico no log de eventos estendidos | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0b13f081338e26aaa33306998d3e562088609a6a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770517"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Acessar informações de diagnóstico nos logs de eventos estendidos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  No [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], o rastreamento ([Operação de rastreamento de driver](../../connect/jdbc/tracing-driver-operation.md)) foi atualizado para facilitar a correlação de eventos do cliente com as informações de diagnóstico, como falhas na conexão, do buffer de anéis de conectividade do servidor e informações de desempenho do aplicativo no log de eventos estendido. Para obter mais informações sobre como ler o log de eventos estendidos, consulte [View Event Session Data](https://msdn.microsoft.com/library/hh710068(SQL.110).aspx).  
  
## <a name="details"></a>Detalhes  
 Para operações de conexão, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enviará uma ID de conexão do cliente. Se a conexão falhar, você poderá acessar o buffer de anéis de conectividade ([Solução de problemas de conectividade no SQL Server 2008 com o Buffer de Anéis de Conectividade](https://go.microsoft.com/fwlink/?LinkId=207752)) e localizar o campo **ClientConnectionID** e poderá obter informações de diagnóstico sobre a falha de conexão. As IDs de conexão de cliente estarão registradas no buffer de anéis se um erro ocorrer. (Se uma conexão falhar antes de enviar o pacote pré-logon, uma ID conexão do cliente não será gerada.) A ID de conexão de cliente é um GUID de 16 bytes. Você também poderá localizar a ID de conexão do cliente na saída do destino de eventos estendidos se a ação de **client_connection_id** for adicionada a eventos em uma sessão de eventos estendidos. Caso precise de assistência adicional com o diagnóstico do driver do cliente, habilite o rastreamento e reexecute o comando de execução para observar o campo **ClientConnectionID** no rastreamento.  
  
 Você pode obter o cliente do ID de conexão programaticamente, usando [ISQLServerConnection Interface](../../connect/jdbc/reference/isqlserverconnection-interface.md). A ID de conexão também estará presente em todas as exceções relacionadas à conexão.  
  
 Quando há um erro de conexão, a ID de conexão do cliente nas informações de rastreamento BID (Diagnóstico Interno) do servidor e no buffer de anéis de conectividade pode ajudar a correlacionar as conexões do cliente às conexões no servidor. Para obter mais informações sobre rastreamentos BID no servidor, confira [Rastreamento de acesso a dados](https://go.microsoft.com/fwlink/?LinkId=125805). Observe que o artigo sobre rastreamento de acesso a dados também traz informações sobre o rastreamento de acesso a dados que não se aplica ao [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]; confira [Operação de rastreamento de driver](../../connect/jdbc/tracing-driver-operation.md) para obter informações sobre como fazer um rastreamento de acesso a dados usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 O JDBC Driver também envia uma ID de atividade específica do thread. A ID da atividade será capturada nas sessões de eventos estendidas se as sessões forem iniciadas com a opção de TRACK_CAUSAILITY habilitada. Para problemas de desempenho com uma conexão ativa, você pode obter a ID de atividade do rastreamento do cliente (campo ActivityID) e localizar a ID de atividade na saída dos eventos estendidos. A ID de atividade nos eventos estendidos é um GUID de 16 bytes (não é o mesmo que o GUID da ID de conexão do cliente) com o acréscimo de um número de sequência de 4 bytes. O número sequencial representa a ordem de uma solicitação de um thread. O ActivityId é enviado para instruções SQL em lotes e solicitações RPC. Para habilitar o envio de ActivityId ao servidor, você precisa especificar primeiro o par de valores chaves a seguir no arquivo Logging.Properties:  
  
```
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 Qualquer valor diferente de `on` (diferencia maiúsculas de minúsculas) desabilitará o envio da ActivityId.  
  
 Para obter mais informações, veja [Rastreamento de operação do driver](../../connect/jdbc/tracing-driver-operation.md). Esse sinalizador de rastreamento é usado com os agentes de objeto do JDBC correspondentes para decidir se haverá ou não o rastreamento e envio de ActivityId no JDBC driver. Além disso, para atualizar o arquivo Logging.Properties, o agente com.microsoft.sqlserver.jdbc precisa ser habilitado para FINER ou posterior. Caso você deseje enviar ActivityId ao servidor para solicitações feitas por determinada classe, o agente da classe correspondente precisará ser habilitado para FINER ou FINEST. Por exemplo, se a classe SQLServerStatement habilita o agente com.microsoft.sqlserver.jdbc.SQLServerStatement.  
  
 A seguinte amostra usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] para iniciar uma sessão de eventos estendidos que será armazenada em um buffer de anéis e gravará a ID de atividade enviada de um cliente no RPC e em operações em lote:  
  
```sql
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
