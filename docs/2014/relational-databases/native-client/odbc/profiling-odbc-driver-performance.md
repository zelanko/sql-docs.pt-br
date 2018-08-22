---
title: Criação de perfil de desempenho do Driver ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- profiling ODBC driver performance data [SQL Server Native Client]
- performance [ODBC]
- application statistics [ODBC]
- time statistics [ODBC]
- ODBC, performance data
- SQL Server Native Client ODBC driver, profiling performance data
- SQLPERF data structure
- statistical information [ODBC]
ms.assetid: 8f44e194-d556-4119-a759-4c9dec7ecead
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26dba5236a748dc4a35262f2bdfe05af994e282f
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395205"
---
# <a name="profiling-odbc-driver-performance"></a>Criando perfil de desempenho do driver ODBC
  O driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client driver pode criar perfil de dois tipos de dados de desempenho:  
  
-   Consultas de execução longa.  
  
     O driver pode gravar em um arquivo de log qualquer consulta que não obtenha uma resposta do servidor em um intervalo especificado de tempo. Programadores de aplicativo ou administradores de banco de dados podem pesquisar cada instrução SQL registrada para determinar como eles podem melhorar seu desempenho.  
  
-   Dados de desempenho do driver.  
  
     O driver pode registrar estatísticas de desempenho e gravá-las em um arquivo ou torná-las disponíveis para um aplicativo por meio de uma estrutura de dados específica do driver, denominada SQLPERF. O arquivo que contém as estatísticas de desempenho é um arquivo delimitado por tabulação que pode ser facilmente analisado com qualquer planilha que aceite arquivos delimitados por tabulação, como o Microsoft Excel.  
  
 Qualquer um dos tipos de criação de perfil pode ser ativado da seguinte forma:  
  
-   Conectando a uma fonte de dados que especifica o log.  
  
-   Chamando [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) para definir atributos específicos do driver desse controle de criação de perfil.  
  
 Cada processo de aplicativo obtém sua própria cópia do driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, e a criação de perfil é global para a combinação de uma cópia do driver e um processo do aplicativo. Quando tudo no aplicativo ativar a criação de perfil, esta registrará informações para todas as conexões ativas no driver desse aplicativo. Mesmo as conexões que não foram especificamente chamadas para a criação de perfil são incluídas.  
  
 Depois que o driver abriu um log de criação de perfil (o log de dados de desempenho ou de consulta de execução longa), o log não é fechado enquanto o driver não é descarregado pelo Gerenciador de Driver ODBC, quando um aplicativo libera todos os identificadores de ambiente que ele abriu no driver. Se o aplicativo abrir um novo identificador de ambiente, uma nova cópia do driver será carregada. Em seguida, se o aplicativo se conectar a uma fonte de dados que especifica o mesmo arquivo de log ou definir os atributos específicos do driver para serem registrados no mesmo arquivo, o driver substituirá o log antigo.  
  
 Se um aplicativo iniciar a criação de perfil para um arquivo de log e um segundo aplicativo tentar iniciar a criação de perfil para o mesmo arquivo de log, o segundo aplicativo não conseguirá registrar nenhum dado da criação de perfil. Se o segundo aplicativo iniciar a criação de perfil depois que o primeiro aplicativo tiver descarregado seu driver, o segundo aplicativo substituirá o arquivo de log do primeiro aplicativo.  
  
 Se um aplicativo se conecta a uma fonte de dados que tenha a criação de perfil habilitada, o driver retornará SQL_ERROR se o aplicativo chamar **SQLSetConnectOption** para iniciar o registro em log. Uma chamada para **SQLGetDiagRec** , em seguida, retorna o seguinte:  
  
```  
SQLState: 01000, pfNative = 0  
ErrorMsg: [Microsoft][SQL Server Native Client]  
   An error has occurred during the attempt to access  
   the log file, logging disabled.  
```  
  
 O driver para de coletar dados de desempenho quando um identificador de ambiente é fechado. Se um aplicativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tiver várias conexões, cada uma com seu próprio identificador de ambiente, o driver parará de coletar dados de desempenho quando qualquer um dos identificadores de ambiente associados for fechado.  
  
 Os dados de desempenho do driver podem ser armazenados na estrutura de dados SQLPERF ou registrados em um arquivo delimitado por tabulação. Os dados incluem as seguintes categorias de estatísticas:  
  
-   Perfil de aplicativo  
  
-   Conexão  
  
-   Rede  
  
-   Hora  
  
 Na tabela a seguir, as descrições dos campos na estrutura de dados SQLPERF também se aplicam às estatísticas registradas no arquivo de log de desempenho.  
  
### <a name="application-profile-statistics"></a>Estatísticas de perfil de aplicativo  
  
|Campo de SQLPERF|Description|  
|-------------------|-----------------|  
|TimerResolution|Resolução mínima da hora de relógio do servidor em milissegundos. Isto será relatado normalmente como 0 (zero) e deverá ser considerado somente se o número relatado for maior. Se a resolução mínima do relógio do servidor for maior que o intervalo provável para algumas das estatísticas baseadas em temporizador, estas estatísticas poderão ser aumentadas.|  
|SQLidu|Número de instruções INSERT, DELETE ou UPDATE depois de SQL_PERF_START.|  
|SQLiduRows|Número de instruções INSERT, DELETE ou UPDATE depois de SQL_PERF_START.|  
|SQLSelects|Número de instruções SELECT processadas depois de SQL_PERF_START.|  
|SQLSelectRows|Número de linhas selecionadas depois de SQL_PERF_START.|  
|Transactions|Número de transações de usuário depois de SQL_PERF_START, incluindo reversões. Quando um aplicativo ODBC estiver sendo executado com SQL_AUTOCOMMIT_ON, cada comando será considerado uma transação.|  
|SQLPrepares|Número de [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360) chamadas depois de SQL_PERF_START.|  
|ExecDirects|Número de **SQLExecDirect** chamadas depois de SQL_PERF_START.|  
|SQLExecutes|Número de **SQLExecute** chamadas depois de SQL_PERF_START.|  
|CursorOpens|Número de horas que o driver abriu um cursor de servidor depois de SQL_PERF_START.|  
|CursorSize|Número de linhas nos conjuntos de resultados abertos por cursores depois de SQL_PERF_START.|  
|CursorUsed|Número de linhas realmente recuperadas pelo driver de cursores depois de SQL_PERF_START.|  
|PercentCursorUsed|Iguala CursorUsed/CursorSize. Por exemplo, se um aplicativo fizer com que o driver abra um cursor de servidor para fazer "SELECT COUNT(*) FROM Authors", 23 linhas serão apresentadas no conjunto de resultados para a instrução SELECT. Se, em seguida, o aplicativo buscar apenas três dessas linhas, CursorUsed/CursorSize será 3/23, assim PercentCursorUsed será 13,043478.|  
|AvgFetchTime|Iguala SQLFetchTime/SQLFetchCount.|  
|AvgCursorSize|Iguala CursorSize/CursorOpens.|  
|AvgCursorUsed|Iguala CursorUsed/CursorOpens.|  
|SQLFetchTime|Quantidade cumulativa de horas que a busca de cursores de servidor levou para ser concluída.|  
|SQLFetchCount|Número de buscas feitas em relação aos cursores de servidor depois de SQL_PERF_START.|  
|CurrentStmtCount|Número de identificadores de instrução abertos atualmente em todas as conexões abertas no driver.|  
|MaxOpenStmt|Número máximo de identificadores de instrução abertos simultaneamente depois de SQL_PERF_START.|  
|SumOpenStmt|Número de identificadores de instrução que foram abertos depois de SQL_PERF_START.|  
|**Estatísticas de Conexão:**||  
|CurrentConnectionCount|Número atual de identificadores de conexões ativas que o aplicativo abriu para o servidor.|  
|MaxConnectionsOpened|Número máximo de identificadores de conexões simultâneas abertos depois de SQL_PERF_START.|  
|SumConnectionsOpened|Soma do número de identificadores de conexões que foram abertos depois de SQL_PERF_START.|  
|SumConnectionTime|Soma da quantidade de horas que todas as conexões foram abertas depois de SQL_PERF_START. Por exemplo, se um aplicativo tiver aberto 10 conexões e tiver mantido cada conexão durante 5 segundos, SumConnectionTime será 50 segundos.|  
|AvgTimeOpened|Iguala SumConnectionsOpened/ SumConnectionTime.|  
|**Estatísticas de rede:**||  
|ServerRndTrips|O número de horas que o driver enviou comandos ao servidor e obteve uma resposta.|  
|BuffersSent|Número de pacotes de protocolo TDS enviados ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pelo driver depois de SQL_PERF_START. Os comandos grandes podem obter vários buffers, portanto, se um comando grande for enviado ao servidor e preencher seis pacotes, ServerRndTrips será incrementado em um e BuffersSent será incrementado em seis.|  
|BuffersRec|Número de pacotes de protocolo TDS recebidos pelo driver do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depois que o aplicativo começou a usar o driver.|  
|BytesSent|Número de bytes de dados enviados ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em pacotes de protocolo TDS depois que o aplicativo começou a usar o driver.|  
|BytesRec|Número de bytes de dados em pacotes de protocolo TDS recebidos pelo driver do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depois que o aplicativo começou a usar o driver.|  
  
### <a name="time-statistics"></a>Time Statistics  
  
|Campo SQLPERF|Description|  
|-------------------|-----------------|  
|msExecutionTime|Quantidade cumulativa de horas que o driver gastou processando depois de SQL_PERF_START, incluindo o tempo gasto esperando respostas do servidor.|  
|msNetworkServerTime|Quantidade cumulativa de horas que o driver gastou esperando respostas do servidor.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)   
 [Os tópicos de instruções de desempenho de Driver ODBC de criação de perfil &#40;ODBC&#41;](../../native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)  
  
  
