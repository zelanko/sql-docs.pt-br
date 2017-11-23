---
title: Membros SQLServerStatement | Microsoft Docs
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
ms.assetid: 828cbaa9-ea7a-4986-95c3-5ba0d7d01d83
caps.latest.revision: "28"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cdce6c1ac993fc36b861e9ec6d87926e1a7661a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverstatement-members"></a>Membros SQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pelo [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) classe.  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Nome|Description|  
|----------|-----------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverstatement.md)|Adiciona o comando SQL fornecido à lista atual de comandos para este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[Cancelar](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|Cancela a instrução SQL que está sendo executada por esse [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverstatement.md)|Esvazia a lista atual de comandos SQL para este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|Limpa todos os avisos relatados isso [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[Fechar](../../../connect/jdbc/reference/close-method-sqlserverstatement.md)|Libera isso [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) do objeto banco de dados e recursos do JDBC imediatamente em vez de aguardar que eles sejam liberados automaticamente.|  
|[executar](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)|Executa a instrução SQL fornecida que pode retornar vários resultados.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)|Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)|Executa a instrução SQL fornecida e retorna um único [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)|Executa a instrução SQL fornecida, que pode ser INSERT, UPDATE, MERGE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução SQL DDL.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|Recupera o [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto que gerou esse [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|Recupera a direção para buscar linhas de tabelas de banco de dados que é o padrão para conjuntos de resultados gerados a partir dessa [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|Recupera o número de resultado de conjunto de linhas que é o tamanho da busca padrão para objetos gerado neste conjunto de resultados [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|Recupera todas as chaves geradas automaticamente que são criadas como resultado da execução isso [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|Recupera o número máximo de bytes que podem ser retornadas para caracteres e valores de coluna binária em um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto que é produzido por esse [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|Recupera o número máximo de linhas que uma [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto que é produzido por esse [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto pode conter.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|Move para o próximo resultado deste [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|Recupera o número de segundos a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aguardará para este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto a ser executado.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|Recupera a modo de buffer para esta resposta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|Recupera o resultado atual como um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|Recupera o resultado da simultaneidade do conjunto de [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que são gerados por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|Recupera a suspensão do conjunto de resultado [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que são gerados por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|Recupera o conjunto de resultados tipo para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que são gerados por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|Recupera o resultado atual como uma contagem de atualização.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|Recupera o primeiro aviso informado por chamadas neste [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|Indica se este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) o objeto foi fechado.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|Retorna um valor que indica se uma instrução pode ser adicionada ao pool de instruções fornecido pelo usuário.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)|Indica se o objeto da instrução é um wrapper para a interface especificada.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|Define o nome do cursor SQL como a cadeia de caracteres especificada, que será usada por métodos de execução subsequentes.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|Define o modo de processamento de escape.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|Fornece ao driver JDBC uma dica sobre a direção em que as linhas do conjunto de resultados devem ser processadas.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|Fornece ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas são necessárias.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|Define o limite para o número máximo de bytes em uma [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) coluna armazena caracteres ou valores binários, como o número de bytes fornecido.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|Define o limite para o número máximo de linhas que qualquer [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto pode conter como o número fornecido.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|Solicita que uma instrução seja colocada ou não em pool.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|Define o número de segundos que o driver aguardará um [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto como o número de segundos especificado.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|Define a modo de buffer para esta resposta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto maiusculas de minúsculas **cadeia de caracteres completa** ou **adaptável**.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)|Retorna um objeto que implementa a interface especificada para permitir acesso a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte também  
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
