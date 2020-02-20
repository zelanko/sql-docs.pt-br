---
title: Membros de SQLServerStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 828cbaa9-ea7a-4986-95c3-5ba0d7d01d83
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72eededd01cd61d6845cc92bbdfbfd073668dd76
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67970357"
---
# <a name="sqlserverstatement-members"></a>Membros SQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Nome|Descrição|  
|----------|-----------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverstatement.md)|Adiciona o comando SQL fornecido à lista atual de comandos do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|Cancela a instrução SQL que está sendo executada pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) em questão.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverstatement.md)|Esvazia a lista atual de comandos SQL do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|Limpa todos os avisos que são relatados no objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverstatement.md)|Libera imediatamente o banco de dados e os recursos do JDBC do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), em vez de aguardar que eles sejam liberados automaticamente.|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)|Executa a instrução SQL fornecida que pode retornar vários resultados.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)|Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)|Executa a instrução SQL fornecida e retorna um único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)|Executa a instrução SQL fornecida, que pode ser INSERT, UPDATE, MERGE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução SQL DDL.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|Recupera o objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) que produziu o objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) em questão.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|Recupera a direção para efetuar fetch em linhas de tabelas de banco de dados que é o padrão para conjuntos de resultados gerados com base neste objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|Recupera o número de linhas do conjunto de resultados que é o tamanho de fetch padrão para objetos do conjunto de resultados gerados do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|Recupera todas as chaves geradas automaticamente criadas como resultado da execução do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|Recupera o número máximo de bytes que podem ser retornados para valores de caractere e de coluna binária em um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerado pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|Recupera o número máximo de linhas que um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) produzido pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) pode conter.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|Move para o próximo resultado do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|Recupera o número de segundos que o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aguardará pela execução deste objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|Recupera o modo de buffer de resposta do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|Recupera o resultado atual como um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|Recupera a simultaneidade do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|Recupera a suspensão do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|Recupera o tipo do conjunto de resultados de objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) gerados pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|Recupera o resultado atual como uma contagem de atualização.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|Recupera o primeiro aviso informado por chamadas no objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) em questão.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|Indica se o objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) foi fechado.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|Retorna um valor que indica se uma instrução pode ser adicionada ao pool de instruções fornecido pelo usuário.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)|Indica se o objeto da instrução é um wrapper para a interface especificada.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|Define o nome do cursor SQL como a cadeia de caracteres especificada, que será usada por métodos de execução subsequentes.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|Define o modo de processamento de escape.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|Fornece ao driver JDBC uma dica sobre a direção em que as linhas do conjunto de resultados devem ser processadas.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|Fornece ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas são necessárias.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|Define o limite para o número máximo de bytes em uma coluna [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que armazena caracteres ou valores binários, como o número de bytes fornecido.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|Define o limite para o número máximo de linhas que qualquer objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) pode conter como o número fornecido.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|Solicita que uma instrução seja colocada ou não em pool.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|Define o número de segundos que o driver aguardará pela execução de um objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) como o número de segundos fornecido.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|Define o modo de buffer de resposta do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) como **String full** ou **adaptive** que não diferencia maiúsculas de minúsculas.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)|Retorna um objeto que implementa a interface especificada para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
