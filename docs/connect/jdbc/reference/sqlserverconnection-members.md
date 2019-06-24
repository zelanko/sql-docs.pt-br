---
title: Membros de SQLServerConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4612b0762d8a0d619a19b61b8bb10ef6a68d1ba0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803080"
---
# <a name="sqlserverconnection-members"></a>Membros de SQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|Usado para especificar o nível de isolamento da transação de instantâneo.|  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Classe herdada de:|Descrição|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE, TRANSACTION_READ_COMMITTED, TRANSACTION_READ_UNCOMMITTED, TRANSACTION_REPEATABLE_READ, TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|Limpa todos os avisos relatados para o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|Libera imediatamente o banco de dados do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão e os recursos do JDBC, em vez de aguardar que eles sejam liberados automaticamente.|  
|[closeUnreferencedPreparedStatementHandles](../../../connect/jdbc/reference/closeunreferencedpreparedstatementhandles-method-sqlserverconnection.md)|Força o un-preparar solicitações para quaisquer instruções preparadas com descartados pendentes a serem executadas.| 
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|Torna permanentes todas as alterações feitas desde a confirmação ou reversão anterior e libera todos os bloqueios de banco de dados atualmente mantidos pelo objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão.|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|Cria uma **Java** objeto sem dados.|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|Cria uma **CLOB** objeto sem dados.|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|Cria uma **NCLOB** objeto sem dados.|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|Cria um objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) para enviar instruções SQL ao banco de dados.|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|Cria uma **Java** objeto sem dados.|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|Recupera o modo de confirmação automática atual para o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|Recupera o nome do catálogo atual do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[Método getClientConnectionID &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|Obtém a ID de conexão da última tentativa de conexão, seja a tentativa bem-sucedida ou não.|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|Recupera informações relativas às propriedades de informações de cliente que têm o suporte do driver JDBC.|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverconnection.md)|Retorna o valor de **disableStatementPooling** propriedade de conexão. Essa configuração controla se o pooling de instrução está habilitado ou não para essa conexão.|
|[getDiscardedServerPreparedStatementCount](../../../connect/jdbc/reference/getdiscardedserverpreparedstatementcount-method-sqlserverconnection.md)|Retorna o número de pendente no momento preparada instrução unprepare ações.|
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection.md)|Retorna o valor de **enablePrepareOnFirstPreparedStatementCall** propriedade de conexão.|
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|Recupera a funcionalidade atual de suspensão de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) criados com o uso do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|Recupera um objeto [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) que contém metadados sobre o banco de dados para o qual o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) representa uma conexão.|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverconnection.md)|Retorna o valor de **serverPreparedStatementDiscardThreshold** propriedade de conexão.|  
|[getStatementHandleCacheEntryCount](../../../connect/jdbc/reference/getstatementhandlecacheentrycount-method-sqlserverconnection.md)|Retorna o número atual de identificadores de instrução preparada em pool.|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverconnection.md)|Retorna o tamanho do cache de instrução preparada para essa conexão.|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|Recupera o nível de isolamento de transação atual do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão.|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|Recupera o objeto Map associado ao objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|Recupera o primeiro aviso relatado por chamadas no objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|Indica se o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão foi fechado.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|Indica se o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) está no modo somente leitura.|  
|[isStatementPoolingEnabled](../../../connect/jdbc/reference/isstatementpoolingenabled-method-sqlserverconnection.md)|Retorna se o pooling de instrução está habilitado ou não para essa conexão.|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|Indica se o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) não foi fechado e ainda é válido.|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|Converte a instrução SQL fornecida na gramática SQL nativa do servidor de banco de dados.|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|Cria um objeto [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) para chamar procedimentos armazenados de bancos de dados.|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|Cria um objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) para enviar instruções SQL com parâmetros ao banco de dados.|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|Remove o objeto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) especificado da transação atual.|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|Desfaz todas as alterações feitas na transação atual e libera todos os bloqueios de banco de dados atualmente mantidos pelo objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|Define o modo de confirmação automática do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) como o estado fornecido.|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|Define o nome de catálogo especificado para selecionar um subespaço do banco de dados do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão no qual trabalhar.|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|Define o valor das propriedades de informações de cliente.|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverconnection.md)|Define o pooling de instrução como verdadeira ou falsa.|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection.md)|Especifica o novo valor de **enablePrepareOnFirstPreparedStatementCall** propriedade de conexão.|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|Altera a funcionalidade de suspensão de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) criados com o uso do objeto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) em questão para a capacidade de colocação em espera fornecida.|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|Coloca este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) no modo somente leitura como uma dica para o driver JDBC habilitar as otimizações de banco de dados.|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|Cria um ponto de salvamento sem nome na transação atual e retorna o novo objeto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) que o representa.|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverconnection.md)|Define o novo valor de **serverPreparedStatementDiscardThreshold** propriedade de conexão.|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverconnection.md)|Define o tamanho do cache de instrução preparada para essa conexão.|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|Tenta alterar o nível de isolamento de transação do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) para o nível fornecido.|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|Instala o objeto TypeMap fornecido como o mapa de tipo do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) em questão.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.lang.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
