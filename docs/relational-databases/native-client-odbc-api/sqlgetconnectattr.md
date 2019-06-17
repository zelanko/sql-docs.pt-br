---
title: SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 153b5f73ea753639a7617f5de6d942dae40fadda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014451"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define atributos de conexão específicos de driver. Alguns dos atributos estão disponíveis a **SQLGetConnectAttr**, e a função é usada para informar as configurações atuais. Os valores informados em relação a esses atributos não são garantidos até que uma conexão seja estabelecida ou o atributo seja definido usando [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 Este tópico lista os atributos somente leitura. Para obter informações sobre os outros atributos de conexão específicos de driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
## <a name="sqlcoptssconnectiondead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 O atributo SQL_COPT_SS_CONNECTION_DEAD informa o estado de uma conexão com um servidor. O driver consulta a rede quanto ao estado atual da conexão.  
  
> [!NOTE]  
>  O atributo de conexão ODBC padrão SQL_ATTR_CONNECTION_DEAD retorna o estado mais recente da conexão. Esse talvez não seja o estado da conexão atual.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_CD_TRUE|A conexão com o servidor foi perdida.|  
|SQL_CD_FALSE|A conexão está aberta e disponível ao processamento de instrução.|  
  
## <a name="sqlcoptssclientconnectionid"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 O atributo SQL_COPT_SS_CLIENT_CONNECTION_ID recupera a ID de conexão de cliente, que pode ser usada para localizar:  
  
-   Informações de diagnóstico no log de XEvents, quando habilitado.  
  
-   As informações de erro de conexão no buffer de anéis de conexão.  
  
-   As informações de diagnóstico nos logs de rastreamento de acesso a dados, quando habilitado.  
  
 Para obter mais informações, consulte [acessando informações de diagnóstico no Log de eventos estendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_ERROR|Falha na conexão.|  
|SQL_SUCCESS|A conexão foi bem-sucedida. A ID de conexão de cliente será localizada no buffer de saída.|  
  
## <a name="sqlcoptssperfdata"></a>SQL_COPT_SS_PERF_DATA  
 O atributo SQL_COPT_SS_PERF_DATA retorna um ponteiro para uma estrutura SQLPERF que contém as estatísticas de desempenho do driver atuais. **SQLGetConnectAttr** retornará NULL se registro em log do desempenho não for habilitado. As estatísticas na estrutura SQLPERF não são atualizadas dinamicamente pelo driver. Chame **SQLGetConnectAttr** sempre que as estatísticas de desempenho precisarem ser atualizadas.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|NULL|O registro em log de desempenho não está habilitado.|  
|Qualquer outro valor|Um ponteiro para uma estrutura SQLPERF.|  
  
## <a name="sqlcoptssperfquery"></a>SQL_COPT_SS_PERF_QUERY  
 O atributo SQL_COPT_SS_PERF_QUERY retorna TRUE caso o registro em log das consultas demoradas em execução esteja habilitado. A solicitação retorna FALSE caso registro em log da consulta não esteja ativo.  
  
## <a name="sqlcoptssuserdata"></a>SQL_COPT_SS_USER_DATA  
 O atributo SQL_COPT_SS_USER_DATA recupera o ponteiro dos dados de usuário. Os dados de usuário são armazenados na memória do cliente e registrados por conexão. Caso o ponteiro de dados do usuário não seja definido, SQL_UD_NOTSET, um ponteiro NULL, é retornado.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_UD_NOTSET|Nenhum ponteiro de dados do usuário é definido.|  
|Qualquer outro valor|Um ponteiro para os dados do usuário.|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>Suporte do SQLGetConnectAttr a SPNs (Nomes da Entidade de Serviço)  
 SQLGetConnectAttr pode ser usado para consultar o valor dos novos atributos de conexão SQL_COPT_SS_SERVER_SPN, SQL_COPT_SS_FAILOVER_PARTNER_SPN, SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD. (SQLGetConnectOption também pode ser usado para consultar esses valores.)  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD só está disponível para conexões abertas que usam a Autenticação do Windows.  
  
 Caso SQL_COPT_SS_SERVER_SPN ou SQL_COPT_SS_FAILOVER_PARTNER não tenha sido definido, será retornado o valor padrão (uma cadeia de caracteres vazia).  
  
 Para obter mais informações sobre SPNs, consulte [nomes de entidade de serviço &#40;SPNs&#41; em conexões de cliente &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLGetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59347)   
 [Detalhes de implementação de API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
