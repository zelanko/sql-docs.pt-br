---
title: Suporte a colunas esparsas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a832a05d977cebfae8742ac75b7c88516919172d
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420215"
---
# <a name="sparse-columns-support-odbc"></a>Suporte a colunas esparsas (ODBC)
  Este tópico descreve o suporte a ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para colunas esparsas. Para obter um exemplo que demonstra o suporte ODBC para colunas esparsas, consulte [chamar SQLColumns em uma tabela com colunas esparsas](../../native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md). Para obter mais informações sobre colunas esparsas, consulte [Sparse Columns Support in SQL Server Native Client](../features/sparse-columns-support-in-sql-server-native-client.md).  
  
## <a name="statement-metadata"></a>Metadados de instrução  
 O campo do descritor APD (descritor de parâmetro de aplicativo) e o atributo da instrução SQL_SOPT_SS_NAME_SCOPE aceitam os valores adicionais SQL_SS_NAME_SCOPE_EXTENDED e SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET. Esses valores especificam quais colunas são incluídas no conjunto de resultados retornado por [SQLColumns](../../native-client-odbc-api/sqlcolumns.md). Para obter mais informações sobre SQL_SOPT_SS_NAME_SCOPE, consulte [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md).  
  
 Um novo IRD (descritor de linha de implementação), um campo SQLSMALLINT somente leitura chamado SQL_CA_SS_IS_COLUMN_SET, pode ser usado para determinar se uma coluna é um valor XML `column_set`. SQL_CA_SS_IS_COLUMN_SET usa os valores SQL_TRUE e SQL_FALSE.  
  
## <a name="catalog-metadata"></a>Metadados de catálogo  
 Duas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] colunas específicas (SS_IS_SPARSE e SS_IS_COLUMN_SET) foram adicionadas ao conjunto de resultados de [SQLColumns](../../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="odbc-function-support-for-sparse-columns"></a>Suporte da função de ODBC para colunas esparsas  
 As seguintes funções de ODBC foram atualizadas para oferecer suporte a colunas esparsas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
