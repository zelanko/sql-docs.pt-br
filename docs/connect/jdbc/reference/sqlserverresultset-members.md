---
title: Membros de SQLServerResultSet | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2a438d5d-2d6a-46a0-a2ae-f35fbae4a472
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf318137b6d3f23a2161de97999df29b7f29ed8b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverresultset-members"></a>Membros de SQLServerResultSet
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pelo [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) classe.  
  
## <a name="constructors"></a>Construtores  
 Nenhuma.  
  
## <a name="fields"></a>Campos  
  
|Nome|Description|  
|----------|-----------------|  
|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|Usado para especificar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de simultaneidade otimista com nenhuma bloqueios de leitura/gravação.|  
|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|Usado para especificar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de simultaneidade otimista com nenhuma bloqueios de leitura/gravação.|  
|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|Usado para especificar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de simultaneidade otimista com bloqueios de leitura/gravação.|  
|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|Usado para especificar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor de somente avanço, somente leitura.|  
|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|Usado para especificar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor dinâmico.|  
|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|Usado para especificar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor de conjunto de chaves.|  
|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|Usado para especificar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor estático.|  
|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|Usado para especificar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor de somente avanço, somente leitura.|  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Classe herdada de:|Description|  
|---------------------------|-----------------|  
|java.sql.ResultSet|CLOSE_CURSORS_AT_COMMIT, CONCUR_READ_ONLY, CONCUR_UPDATABLE, FETCH_FORWARD, FETCH_REVERSE, FETCH_UNKNOWN, HOLD_CURSORS_OVER_COMMIT, TYPE_FORWARD_ONLY, TYPE_SCROLL_INSENSITIVE, TYPE_SCROLL_SENSITIVE|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|[Absoluto](../../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)|Move o cursor para a linha especificada neste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[afterLast](../../../connect/jdbc/reference/afterlast-method-sqlserverresultset.md)|Move o cursor para depois da última linha deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[beforeFirst](../../../connect/jdbc/reference/beforefirst-method-sqlserverresultset.md)|Move o cursor para antes da primeira linha desse [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[cancelRowUpdates](../../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)|Cancela as atualizações feitas na linha atual nesta [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverresultset.md)|Limpa todos os avisos relatados sobre isso [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverresultset.md)|Libera isso [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) do objeto banco de dados e recursos do JDBC imediatamente em vez de aguardar que isso aconteça quando ele é fechado automaticamente.|  
|[deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)|Exclui a linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) e do banco de dados subjacente.|  
|[Finalizar](../../../connect/jdbc/reference/finalize-method-sqlserverresultset.md)|Fecha explicitamente isso [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[findColumn](../../../connect/jdbc/reference/findcolumn-method-sqlserverresultset.md)|Recupera o índice da primeira coluna correspondente para o nome de coluna especificado neste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[first](../../../connect/jdbc/reference/first-method-sqlserverresultset.md)|Move o cursor para a primeira linha desse [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto de matriz.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) em questão como um fluxo de caracteres ASCII.|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)|Recupera o valor do índice de coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um BigDecimal.|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um fluxo binário de bytes não interpretados.|  
|[GetBlob](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto de Blob na linguagem de programação Java.|  
|[GetBoolean](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **booliano** na linguagem de programação Java.|  
|[GetByte](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **bytes** na linguagem de programação Java.|  
|[GetBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **bytes** matriz na linguagem de programação Java.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto Java.IO. Reader.|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto Clob na linguagem de programação Java.|  
|[getConcurrency](../../../connect/jdbc/reference/getconcurrency-method-sqlserverresultset.md)|Recupera o modo de simultaneidade deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getCursorName](../../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)|Recupera o nome do cursor SQL usado por este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto Java.SQL. Date na linguagem de programação Java.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)|Recupera o valor da coluna especificada como um[DateTimeOffset classe](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto.|  
|[GetDouble](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **duplo** na linguagem de programação Java.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverresultset.md)|Recupera a direção de busca para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)|Recupera o tamanho da busca para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[GetFloat](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **float** na linguagem de programação Java.|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverresultset.md)|Recupera a colocação em espera desse [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **int** na linguagem de programação Java.|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **longo** na linguagem de programação Java.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)|Recupera o número, tipos e propriedades desse [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) colunas do objeto.|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual do [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto do leitor.|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual do [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)de objeto como um **NClob** objeto na linguagem de programação Java.|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual do [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como uma cadeia de caracteres no Java linguagem de programação.|  
|[GetObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)|Obtém o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto na linguagem de programação Java.|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto de referência na linguagem de programação Java.|  
|[getRow](../../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)|Recupera o número da linha atual.|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **curto** na linguagem de programação Java.|  
|[getStatement](../../../connect/jdbc/reference/getstatement-method-sqlserverresultset.md)|Recupera o [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que gerou esse [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[GetString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **cadeia de caracteres** na linguagem de programação Java.|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual do [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **SQLXML** objeto.|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto Java.SQL. time na linguagem de programação Java.|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto Java.SQL. timestamp na linguagem de programação Java.|  
|[GetType](../../../connect/jdbc/reference/gettype-method-sqlserverresultset.md)|Recupera o tipo de cursor deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getUnicodeStream](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um fluxo de caracteres Unicode.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)|Recupera o valor da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto de URL.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverresultset.md)|Recupera o primeiro aviso relatado por chamadas nisso [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)|Insere o conteúdo da linha de inserção nisso [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto e no banco de dados.|  
|[isAfterLast](../../../connect/jdbc/reference/isafterlast-method-sqlserverresultset.md)|Recupera se o cursor estiver após a última linha na [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[isBeforeFirst](../../../connect/jdbc/reference/isbeforefirst-method-sqlserverresultset.md)|Recupera se o cursor estiver antes da primeira linha neste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverresultset.md)|Indica se este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) o objeto foi fechado.|  
|[isFirst](../../../connect/jdbc/reference/isfirst-method-sqlserverresultset.md)|Recupera se o cursor estiver na primeira linha desse [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[isLast](../../../connect/jdbc/reference/islast-method-sqlserverresultset.md)|Recupera se o cursor estiver na última linha deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[last](../../../connect/jdbc/reference/last-method-sqlserverresultset.md)|Move o cursor para a última linha na [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[moveToCurrentRow](../../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)|Move o cursor para a posição do cursor lembrada, geralmente a linha atual.|  
|[moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)|Move o cursor para a linha de inserção.|  
|[Avançar](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)|Move o cursor uma linha para baixo a partir da posição atual.|  
|[Anterior](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)|Move o cursor para a linha anterior neste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[refreshRow](../../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)|Atualiza a linha atual com seu valor mais recente no banco de dados.|  
|[relative](../../../connect/jdbc/reference/relative-method-sqlserverresultset.md)|Move o cursor determinada quantidade de linhas, em relação à linha atual, em um positivo ou em uma direção negativa.|  
|[RowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)|Recupera se uma linha foi excluída.|  
|[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)|Recupera se a linha atual teve uma inserção.|  
|[RowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)|Recupera se a linha atual foi atualizada.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)|Fornece uma dica sobre a direção na qual as linhas na [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto será processado.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)|Dá ao driver JDBC uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas forem necessárias para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[updateArray](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)|Atualiza a coluna designada com um objeto de matriz.|  
|[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor de fluxo ASCII.|  
|[updateBigDecimal](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)|Atualiza a coluna designada com um objeto BigDecimal.|  
|[updateBinaryStream](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor de fluxo binário.|  
|[updateBlob](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor java.sql.Blob.|  
|[updateBoolean](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)|Atualiza a coluna designada com um **booliano** valor.|  
|[updateByte](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)|Atualiza a coluna designada com um **bytes** valor.|  
|[updateBytes](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)|Atualiza a coluna designada com uma matriz de **bytes** valores.|  
|[updateCharacterStream](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor de fluxo de caracteres.|  
|[updateClob](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor java.sql.Clob.|  
|[updateDate](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor de data.|  
|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)|Atualizações de um [DateTimeOffset classe](../../../connect/jdbc/reference/datetimeoffset-class.md) coluna.|  
|[updateDouble](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)|Atualiza a coluna designada com um **duplo** valor.|  
|[updateFloat](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)|Atualiza a coluna designada com um **float** valor.|  
|[updateInt](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)|Atualiza a coluna designada com um **int** valor.|  
|[updateLong](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)|Atualiza a coluna designada com um **longo** valor.|  
|[updateNCharacterStream](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor de fluxo de caracteres.|  
|[updateNClob](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)|Atualiza a coluna designada com o valor do objeto especificado.|  
|[updateNString](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)|Atualiza a coluna designada com um **cadeia de caracteres** valor.|  
|[updateNull](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor nulo.|  
|[updateObject](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)|Atualiza a coluna designada com um **objeto** valor.|  
|[updateRef](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor de java.sql.Ref.|  
|[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)|Atualiza o banco de dados subjacente com o novo conteúdo da linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[updateShort](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)|Atualiza a coluna designada com um **curto** valor.|  
|[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)|Atualiza a coluna designada com um **cadeia de caracteres** valor.|  
|[updateSQLXML](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)|Atualiza a coluna designada com um **SQLXML** valor.|  
|[updateTime](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor de hora.|  
|[updateTimestamp](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)|Atualiza a coluna designada com um valor de carimbo de data/hora.|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlserverresultset.md)|Verifica se o último valor lido era um valor nulo.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte também  
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
