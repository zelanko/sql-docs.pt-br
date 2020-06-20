---
title: SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
author: rothja
ms.author: jroth
ms.openlocfilehash: f82a0fb71103e811b36280f9722c160791023e44
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022365"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define atributos de conexão específicos de driver. Alguns dos atributos estão disponíveis para `SQLGetConnectAttr` o, e a função é usada para relatar suas configurações atuais. Os valores informados em relação a esses atributos não são garantidos até que uma conexão seja estabelecida ou o atributo seja definido usando [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
 Este tópico lista os atributos somente leitura. Para obter informações sobre os outros atributos de conexão específicos de driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
## <a name="sql_copt_ss_connection_dead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 O atributo SQL_COPT_SS_CONNECTION_DEAD informa o estado de uma conexão com um servidor. O driver consulta a rede quanto ao estado atual da conexão.  
  
> [!NOTE]  
>  O atributo de conexão ODBC padrão SQL_ATTR_CONNECTION_DEAD retorna o estado mais recente da conexão. Esse talvez não seja o estado da conexão atual.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_CD_TRUE|A conexão com o servidor foi perdida.|  
|SQL_CD_FALSE|A conexão está aberta e disponível ao processamento de instrução.|  
  
## <a name="sql_copt_ss_client_connection_id"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 O atributo SQL_COPT_SS_CLIENT_CONNECTION_ID recupera a ID de conexão de cliente, que pode ser usada para localizar:  
  
-   Informações de diagnóstico no log de XEvents, quando habilitado.  
  
-   As informações de erro de conexão no buffer de anéis de conexão.  
  
-   As informações de diagnóstico nos logs de rastreamento de acesso a dados, quando habilitado.  
  
 Para obter mais informações, consulte [Acessando informações de diagnóstico no log de eventos estendidos](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_ERROR|Falha na conexão.|  
|SQL_SUCCESS|A conexão foi bem-sucedida. A ID de conexão de cliente será localizada no buffer de saída.|  
  
## <a name="sql_copt_ss_perf_data"></a>SQL_COPT_SS_PERF_DATA  
 O atributo SQL_COPT_SS_PERF_DATA retorna um ponteiro para uma estrutura SQLPERF que contém as estatísticas de desempenho do driver atuais. `SQLGetConnectAttr`retornará NULL se o log de desempenho não estiver habilitado. As estatísticas na estrutura SQLPERF não são atualizadas dinamicamente pelo driver. Chame `SQLGetConnectAttr` cada vez que as estatísticas de desempenho precisam ser atualizadas.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|NULO|O registro em log de desempenho não está habilitado.|  
|Qualquer outro valor|Um ponteiro para uma estrutura SQLPERF.|  
  
## <a name="sql_copt_ss_perf_query"></a>SQL_COPT_SS_PERF_QUERY  
 O atributo SQL_COPT_SS_PERF_QUERY retorna TRUE caso o registro em log das consultas demoradas em execução esteja habilitado. A solicitação retorna FALSE caso registro em log da consulta não esteja ativo.  
  
## <a name="sql_copt_ss_user_data"></a>SQL_COPT_SS_USER_DATA  
 O atributo SQL_COPT_SS_USER_DATA recupera o ponteiro dos dados de usuário. Os dados de usuário são armazenados na memória do cliente e registrados por conexão. Caso o ponteiro de dados do usuário não seja definido, SQL_UD_NOTSET, um ponteiro NULL, é retornado.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_UD_NOTSET|Nenhum ponteiro de dados do usuário é definido.|  
|Qualquer outro valor|Um ponteiro para os dados do usuário.|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>Suporte do SQLGetConnectAttr a SPNs (Nomes da Entidade de Serviço)  
 SQLGetConnectAttr pode ser usado para consultar o valor dos novos atributos de conexão SQL_COPT_SS_SERVER_SPN, SQL_COPT_SS_FAILOVER_PARTNER_SPN, SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD. (SQLGetConnectOption também pode ser usado para consultar esses valores.)  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD só está disponível para conexões abertas que usam a Autenticação do Windows.  
  
 Caso SQL_COPT_SS_SERVER_SPN ou SQL_COPT_SS_FAILOVER_PARTNER não tenha sido definido, será retornado o valor padrão (uma cadeia de caracteres vazia).  
  
 Para obter mais informações sobre SPNs, consulte [nomes de entidade de serviço &#40;SPNs&#41; em conexões de cliente &#40;&#41;ODBC ](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLGetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59347)   
 [Detalhes de implementação da API ODBC](odbc-api-implementation-details.md)   
 [DEFINIR QUOTED_IDENTIFIER &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [DEFINIR ANSI_NULLS &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [DEFINIR ANSI_PADDING &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
