---
title: Membros de SQLServerResultSetMetaData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 37587981-2979-49a3-a6ab-df4bfb9b8748
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcee6e3b072315538dd6fa05b248cc2104e4ab1a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverresultsetmetadata-members"></a>Membros de SQLServerResultSetMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pelo [SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) classe.  
  
## <a name="constructors"></a>Construtores  
 Nenhuma.  
  
## <a name="fields"></a>Campos  
 Nenhuma.  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Nome|Description|  
|----------|-----------------|  
|java.sql.ResultSetMetaData|columnNoNulls, columnNullable, columnNullableUnknown|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|[getCatalogName](../../../connect/jdbc/reference/getcatalogname-method-sqlserverresultsetmetadata.md)|Obtém o nome do catálogo da tabela que inclui a coluna designada.|  
|[getColumnClassName](../../../connect/jdbc/reference/getcolumnclassname-method-sqlserverresultsetmetadata.md)|Retorna o nome totalmente qualificado da classe Java cujas instâncias são fabricadas, se o [getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md) método o [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) classe é chamada para recuperar um valor da coluna.|  
|[getColumnCount](../../../connect/jdbc/reference/getcolumncount-method-sqlserverresultsetmetadata.md)|Retorna o número de colunas no conjunto de resultados.|  
|[getColumnDisplaySize](../../../connect/jdbc/reference/getcolumndisplaysize-method-sqlserverresultsetmetadata.md)|Retorna a largura máxima normal, em caracteres, da coluna designada.|  
|[getColumnLabel](../../../connect/jdbc/reference/getcolumnlabel-method-sqlserverresultsetmetadata.md)|Obtém o título sugerido para uso em cópias impressas e exibições da coluna designada.|  
|[getColumnName](../../../connect/jdbc/reference/getcolumnname-method-sqlserverresultsetmetadata.md)|Obter o nome da coluna designada.|  
|[getColumnType](../../../connect/jdbc/reference/getcolumntype-method-sqlserverresultsetmetadata.md)|Recupera o tipo de SQL da coluna designada.|  
|[getColumnTypeName](../../../connect/jdbc/reference/getcolumntypename-method-sqlserverresultsetmetadata.md)|Recupera o nome de tipo específico do banco de dados da coluna designada.|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverresultsetmetadata.md)|Obtém o número de dígitos decimais da coluna designada.|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverresultsetmetadata.md)|Obtém o número de dígitos à direita da vírgula decimal da coluna designada.|  
|[getSchemaName](../../../connect/jdbc/reference/getschemaname-method-sqlserverresultsetmetadata.md)|Obtém o nome de esquema de tabela da coluna designada.|  
|[getTableName](../../../connect/jdbc/reference/gettablename-method-sqlserverresultsetmetadata.md)|Obtém o nome de tabela da coluna designada.|  
|[IsAutoIncrement](../../../connect/jdbc/reference/isautoincrement-method-sqlserverresultsetmetadata.md)|Indica se a coluna designada é numerada automaticamente, o que a torna somente leitura.|  
|[IsCaseSensitive](../../../connect/jdbc/reference/iscasesensitive-method-sqlserverresultsetmetadata.md)|Indica se uma coluna diferencia maiusculas de minúsculas.|  
|[isCurrency](../../../connect/jdbc/reference/iscurrency-method-sqlserverresultsetmetadata.md)|Indica se a coluna designada é um valor monetário.|  
|[isDefinitelyWritable](../../../connect/jdbc/reference/isdefinitelywritable-method-sqlserverresultsetmetadata.md)|Indica se uma gravação na coluna designada terá sucesso definitivamente.|  
|[IsNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverresultsetmetadata.md)|Indica a nulidade de valores na coluna designada.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverresultsetmetadata.md)|Indica se a coluna designada é definitivamente não gravável.|  
|[IsSearchable](../../../connect/jdbc/reference/issearchable-method-sqlserverresultsetmetadata.md)|Indica se a coluna designada pode ser usada em uma cláusula SQL WHERE.|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverresultsetmetadata.md)|Indica se os valores da coluna designada são números com sinal.|  
|[isSparseColumnSet](../../../connect/jdbc/reference/issparsecolumnset-method-sqlserverresultsetmetadata.md)|Indica se uma coluna em um conjunto de resultados é um conjunto de colunas esparsas.|  
|[isWritable](../../../connect/jdbc/reference/iswritable-method-sqlserverresultsetmetadata.md)|Indica se é possível que uma gravação na coluna designada seja bem-sucedida.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte também  
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
