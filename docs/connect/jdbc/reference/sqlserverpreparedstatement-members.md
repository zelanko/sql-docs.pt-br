---
title: Membros de SQLServerPreparedStatement | Microsoft Docs
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
ms.assetid: 2363902f-d4c6-4cd4-a5fc-86079eb9e418
caps.latest.revision: "38"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05f80d22f4eb968f6db9ce24a8c5e9808bd43356
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverpreparedstatement-members"></a>Membros de SQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pelo [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe.  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|Adiciona um conjunto de parâmetros ao lote de comandos para este objeto de instrução.|  
|[Cancelar](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Cancela a instrução SQL que está sendo executada por esse objeto de instrução.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|Esvazia a lista atual de comandos SQL para este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|Limpa os valores de parâmetros atuais imediatamente.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Limpa todos os avisos relatados neste objeto de instrução.|  
|[Fechar](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|Libera o banco de dados e os recursos do JDBC desse objeto de instrução imediatamente em vez de aguardar que eles sejam liberados automaticamente.|  
|[executar](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|Executa a instrução SQL no objeto instrução, que pode ser qualquer tipo de instrução SQL.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|Executa a consulta SQL neste objeto de instrução e retorna o [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto gerado pela consulta.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|Executa a instrução SQL no objeto instrução, que deve ser um SQL INSERT, UPDATE, MERGE ou DELETE instrução; ou uma instrução SQL que não retorne nada, como uma instrução DDL.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto que gerou este objeto de instrução.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a direção para buscar linhas de tabelas de banco de dados que é o padrão para conjuntos de resultados gerados do objeto de instrução.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número de linhas do conjunto de resultados que é o tamanho de busca padrão para resultado conjunto de objetos gerados do objeto de instrução.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera todas as chaves geradas automaticamente que são criadas como resultado da execução deste objeto de instrução.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número máximo de bytes que podem ser retornadas para caracteres e valores de coluna binária em um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto produzido por esse objeto de instrução.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número máximo de linhas que uma [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto produzido por esse objeto de instrução pode conter.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|Recupera um [classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) que contém informações sobre as colunas do objeto de [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto que será retornado quando esse objeto de instrução é executado.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Move para o próximo resultado deste objeto de instrução.|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|Recupera o número, tipos e propriedades dos parâmetros para este objeto de instrução.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a modo de buffer para esta resposta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número de segundos a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aguardará para este objeto de instrução para execução.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o resultado atual como um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o resultado da simultaneidade do conjunto de [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que são gerados por este objeto de instrução.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a suspensão do conjunto de resultado [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que são gerados por este objeto de instrução.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o conjunto de resultados tipo para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que são gerados por este objeto de instrução.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md),) recupera o resultado atual como uma contagem de atualização.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o primeiro aviso informado por chamadas no objeto de instrução.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Indica se este objeto de instrução foi fechado.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Retorna um valor que indica se uma instrução pode ser adicionada ao pool de instruções fornecido pelo usuário.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)|Indica se o objeto da instrução é um wrapper para a interface especificada.|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|Define o número do parâmetro designado como o objeto de matriz determinado.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)|Define o número do parâmetro designado como o objeto InputStream fornecido.|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlserverpreparedstatement.md)|Define o número do parâmetro designado como o objeto BigDecimal fornecido.|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o fluxo de entrada especificado.|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto de Blob especificado.|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **booliano** valor.|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **bytes** valor.|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como a matriz de bytes especificada.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto Reader especificado.|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto Clob fornecido.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o nome do cursor SQL como a Cadeia de Caracteres especificada, que será usada por métodos de execução subsequentes.|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor de data especificado.|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|Define o valor da coluna especificada para o [DateTimeOffset classe](../../../connect/jdbc/reference/datetimeoffset-class.md) valor.|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **duplo** valor.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o modo de processamento de escape.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Fornece ao driver JDBC uma dica sobre a direção em que as linhas do conjunto de resultados devem ser processadas.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Fornece ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas são necessárias.|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **float** valor.|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **int** valor.|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **longo** valor.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o limite para o número máximo de bytes em uma [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) coluna armazena caracteres ou valores binários, como o número de bytes fornecido.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o limite para o número máximo de linhas que qualquer [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto pode conter como o número fornecido.|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto Reader especificado.|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto especificado.|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como um valor nulo, considerando o tipo de parâmetro a ser definido.|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)|Define o parâmetro designado especificado **cadeia de caracteres** objeto.|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)|Define o valor do parâmetro designado usando o objeto fornecido.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Solicita que uma instrução seja colocada ou não em pool. Por padrão, um objeto SQLServerPreparedStatement está em um pool quando criado.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o número de segundos que o driver aguardará para um objeto de instrução executar até o número especificado de segundos.|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o objeto de referência especificado.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define a modo de buffer para esta resposta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto maiusculas de minúsculas **cadeia de caracteres completa** ou **adaptável**.|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **curto** valor.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **cadeia de caracteres** valor.|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlserverpreparedstatement.md)|Define o parâmetro designado especificado **SQLXML** objeto.|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor de hora especificado.|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor de carimbo de data/hora especificado.|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|Define o número do parâmetro designado como o fluxo de entrada especificado, que terá o número de bytes especificado.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverpreparedstatement.md)|Define o parâmetro designado como o valor de URL especificado.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)|Retorna um objeto que implementa a interface especificada para permitir acesso a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Statement|cancele, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte também  
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
