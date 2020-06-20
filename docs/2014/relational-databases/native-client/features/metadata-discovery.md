---
title: Descoberta de metadados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: ec3c0f4f-f838-43ce-85f2-cf2761e2aac5
author: rothja
ms.author: jroth
ms.openlocfilehash: 0397d7f5588be7543f71819c93827819bd8d073f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047939"
---
# <a name="metadata-discovery"></a>Descoberta de metadados
  A melhoria na descoberta de metadados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permite que aplicativos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client assegurem que os metadados de colunas ou parâmetros retornados da execução de uma consulta sejam idênticos ou compatíveis com o formato de metadados especificado antes da execução da consulta. Você receberá um erro se os metadados retornados depois da execução da consulta não forem compatíveis com o formato de metadados especificado antes da execução da consulta.  
  
 Em funções bcp e ODBC, e em interfaces IBCPSession e IBCPSession2, agora você pode especificar uma leitura atrasada (descoberta de metadados atrasada) para evitar a descoberta de metadados para operações de saída de consulta. Isso melhora o desempenho e elimina falhas de descoberta de metadados.  
  
 Se você desenvolver um aplicativo usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] , mas se conectar a uma versão de servidor anterior ao [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], a funcionalidade de descoberta de metadados corresponderá à versão do servidor.  
  
## <a name="remarks"></a>Comentários  
 As funções bcp a seguir foram aperfeiçoadas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para fornecer descoberta de metadados aprimorada:  
  
-   [bcp_columns](../../native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 Você também verá uma melhoria no desempenho ao especificar o formato de metadados usando [bcp_setbulkmode](../../native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md).  
  
 [bcp_control](../../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) tem um novo *eOption* para controlar o comportamento de bcp_readfmt: `BCPDELAYREADFMT` .  
  
 As funções ODBC a seguir foram aperfeiçoadas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para fornecer descoberta de metadados aprimorada:  
  
-   [SQLNumResultCols](../../native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLNumParams](../../native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)  
  
 As funções de membros OLE DB a seguir foram aperfeiçoadas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para fornecer descoberta de metadados aprimorada:  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters::GetParameterInfo (confira [ICommandWithParameters](../../native-client-ole-db-interfaces/icommandwithparameters.md) para obter mais informações)  
  
 Você também verá uma melhoria no desempenho ao especificar o formato de metadados usando IBCPSession::BCPSetBulkMode  
  
 A descoberta de metadados aprimorada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é possível devido à adição de dois procedimentos armazenados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  
