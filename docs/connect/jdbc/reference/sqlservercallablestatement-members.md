---
description: Membros SQLServerCallableStatement
title: Membros de SQLServerCallableStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: Assembly
ms.assetid: 5ebdc186-e50f-4d14-bbf4-95af5051e4a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e80e86c04716e8e305e15c1d49f3852e77b318e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478596"
---
# <a name="sqlservercallablestatement-members"></a>Membros SQLServerCallableStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="inherited-fields"></a>Campos herdados  
 Nenhum.  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Adiciona um conjunto de parâmetros ao lote de comandos deste objeto CallableStatement.|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Cancela a instrução SQL que está sendo executada pelo objeto CallableStatement em questão.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Esvazia a lista atual de comandos SQL do objeto CallableStatement.|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Limpa os valores de parâmetros atuais imediatamente.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Limpa todos os avisos que são relatados no objeto CallableStatement.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Libera imediatamente o banco de dados e os recursos do JDBC do objeto CallableStatement, em vez de aguardar que eles sejam liberados automaticamente.|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Executa a instrução SQL no objeto CallableStatement, que pode ser qualquer tipo de instrução SQL.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Executa a consulta SQL no objeto CallableStatement e retorna o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) em questão gerado pela consulta.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Executa a instrução SQL no objeto CallableStatement, que deve ser uma instrução SQL INSERT, UPDATE, MERGE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução DDL.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) que produziu o objeto CallableStatement em questão.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|Recupera o valor da coluna especificada como um objeto [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md).|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a direção para buscar linhas de tabelas de banco de dados que é o padrão para conjuntos de resultados gerados a partir do objeto CallableStatement.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número de linhas do conjunto de resultados que é o tamanho de busca padrão para objetos do conjunto de resultados gerados do objeto CallableStatement.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera todas as chaves geradas automaticamente criadas como resultado da execução do objeto CallableStatement.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número máximo de bytes que podem ser retornados para valores de caractere e de coluna binária em um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) produzido pelo objeto CallableStatement.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número máximo de linhas que um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerado pelo objeto CallableStatement pode conter.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Recupera um objeto [SQLServerResultSetMetaData Class](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) que contém informações sobre as colunas do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que será retornado quando o objeto CallableStatement for executado.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Move para o próximo resultado do objeto CallableStatement.|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Recupera o número, os tipos e as propriedades dos parâmetros do objeto CallableStatement em questão.|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto Array.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um fluxo de caracteres **ASCII**.|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como java.math.BigDecimal.|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um fluxo binário de bytes ininterruptos.|  
|[getBlob](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro JDBC Blob designado como um objeto Blob na linguagem de programação Java.|  
|[getboolean](../../../connect/jdbc/reference/getboolean-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um valor **booliano**.|  
|[getByte](../../../connect/jdbc/reference/getbyte-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um valor **byte**.|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como uma matriz de bytes.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto java.io.Reader.|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro JDBC Blob designado como um objeto Clob na linguagem de programação Java.|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto java.sql.Date na linguagem de programação Java.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|Recupera o valor da coluna especificada como um objeto [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md).|  
|[getDouble](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um **double** na linguagem de programação Java.|  
|[getFloat](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um **float** na linguagem de programação Java.|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um **int** na linguagem de programação Java.|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um **long** na linguagem de programação Java.|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto Reader.|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro **NCLOB** do JDBC designado como um objeto **NClob** na linguagem de programação Java.|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro **NCHAR**, **NVARCHAR** ou **LONGNVARCHAR** designado como um objeto String na linguagem de programação Java.|  
|[getObject](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto na linguagem de programação Java.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o número de segundos que o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aguardará pela execução do objeto CallableStatement.|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto Ref na linguagem de programação Java.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o modo de buffer de resposta do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o resultado atual como um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a simultaneidade do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto CallableStatement.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera a suspensão do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto CallableStatement.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o tipo do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto CallableStatement.|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um **short** na linguagem de programação Java.|  
|[getString](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto **String** na linguagem de programação Java.|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto java.sql.SQLXML.|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto java.sql.Time na linguagem de programação Java.|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto java.sql.Timestamp na linguagem de programação Java.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o resultado atual como uma contagem de atualização.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)|Recupera o valor do parâmetro designado como um objeto URL na linguagem de programação Java.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera o primeiro aviso informado por chamadas no objeto CallableStatement em questão.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Indica se o objeto Statement foi fechado.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Retorna um valor que indica se uma instrução pode ser adicionada ao pool de instruções fornecido pelo usuário.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)|Indica se o objeto da instrução é um wrapper para a interface especificada.|  
|[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)|Registra o parâmetro OUT.|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Define o número do parâmetro designado como o objeto Array fornecido.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)|Define o parâmetro designado como o fluxo de entrada fornecido.|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlservercallablestatement.md)|Define o número do parâmetro designado como o objeto BigDecimal fornecido.|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)|Define o parâmetro designado como o fluxo de entrada especificado.|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Define o parâmetro designado como o objeto Blob fornecido.|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor **Boolean** fornecido.|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor **byte** fornecido.|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlservercallablestatement.md)|Define o parâmetro designado como a matriz de **bytes** fornecida.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)|Define o parâmetro designado como o objeto Reader fornecido.|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Define o parâmetro designado como o objeto especificado.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o nome do cursor SQL como a cadeia de caracteres especificada, que será usada por métodos de execução subsequentes.|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor de data fornecido.|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)|Define o valor da coluna especificada para o valor da [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md).|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor **double** fornecido.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o modo de processamento de escape.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Fornece ao driver JDBC uma dica sobre a direção em que as linhas do conjunto de resultados devem ser processadas.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Fornece ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas são necessárias.|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor **float** especificado.|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor **int** especificado.|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor **long** especificado.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o limite para o número máximo de bytes em uma coluna [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que armazena caracteres ou valores binários, como o número de bytes especificado.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o limite para o número máximo de linhas que qualquer objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) pode conter como o número especificado.|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)|Define o parâmetro designado como o objeto Reader especificado.|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)|Define o parâmetro designado como o objeto especificado.|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)|Define o parâmetro designado como o objeto String especificado.|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)|Define o parâmetro designado como um valor nulo, considerando o tipo de parâmetro a ser definido.|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)|Define o valor do parâmetro designado usando o objeto fornecido.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Solicita que uma instrução seja colocada ou não em pool. Por padrão, um objeto SQLServerCallableStatement pode ser colocado em pool quando criado.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o número de segundos que o driver aguardará pela execução de um objeto CallableStatement como o número de segundos especificado.|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Define o parâmetro designado como o objeto Ref especificado.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(Herdado de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Define o modo de buffer de resposta do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) como **String full** ou **adaptive** que não diferencia maiúsculas de minúsculas.|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor **short** especificado.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor **String** de Java especificado.|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlservercallablestatement.md)|Define o parâmetro designado como o objeto **SQLXML** especificado.|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor de hora especificado.|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor de carimbo de data/hora especificado.|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|(Herdado de [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)). Define o número do parâmetro designado como o fluxo de entrada fornecido, que terá o número de bytes especificado.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlservercallablestatement.md)|Define o parâmetro designado como o valor de URL especificado.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)|Retorna um objeto que implementa a interface especificada para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlservercallablestatement.md)|Recupera se o último parâmetro OUT lido teve o valor de SQL NULL.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement|addBatch, clearBatch, clearParameters, close, execute, executeBatch, executeQuery, executeUpdate, getMetaData, getParameterMetaData, setArray, setAsciiStream, setBigDecimal, setBinaryStream, setBlob, setboolean, setByte, setBytes, setCharacterStream, setClob, setDate, setDouble, setFloat, setInt, setLong, setNull, setObject, setRef, setShort, setString, setTime, setTimestamp, setUnicodeStream, setURL|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|class java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait,|  
|java.sql.PreparedStatement|addBatch, clearParameters, execute, executeQuery, executeUpdate, getMetaData, getParameterMetaData, getSQLXML, setArray, setAsciiStream, setBigDecimal, setBinaryStream, setBlob, setboolean, setByte, setBytes, setCharacterStream, setClob, setDate, setDate, setDouble, setFloat, setInt, setLong, setNull, setObject, setRef, setShort, setString, setSQLXML, setTime, setTimestamp, setUnicodeStream, setURL|  
|java.sql.Statement|addBatch, cancel, clearBatch, clearWarnings, close, execute, executeBatch, executeQuery, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
