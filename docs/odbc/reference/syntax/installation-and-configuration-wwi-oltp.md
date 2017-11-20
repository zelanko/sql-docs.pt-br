---
title: "Função SQLSetDriverConnectInfo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 970fec5219fed803439fc05c3f6fe56a300617f0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetdriverconnectinfo-function"></a>Função SQLSetDriverConnectInfo
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.81 ODBC: ODBC  
  
 **Resumo**  
 **SQLSetDriverConnectInfo** é usado para definir a cadeia de caracteres de conexão para o token de informações de conexão para um aplicativo **SQLDriverConnect** chamar.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>Argumentos  
 *TokenHandle*  
 [Entrada] Identificador de token.  
  
 *InConnectionString*  
 [Entrada] Uma cadeia de caracteres de conexão completa (consulte a sintaxe "Comentários" em [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)), uma cadeia de caracteres de conexão parcial ou uma cadeia de caracteres vazia.  
  
 *StringLength1*  
 [Entrada] Comprimento de **InConnectionString*, em caracteres, se a cadeia de caracteres for Unicode ou bytes se cadeia de caracteres ANSI ou DBCS.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Mesmo que [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) relacionados a qualquer erro de validação de entrada, exceto que o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e um **tratar** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 Sempre que um driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de Driver retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retorna SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver obterá as informações de diagnóstico de *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO para o aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Aplicativos não devem chamar esta função diretamente. Um driver ODBC que oferece suporte ao pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

