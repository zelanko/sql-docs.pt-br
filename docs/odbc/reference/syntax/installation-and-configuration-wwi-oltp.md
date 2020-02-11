---
title: Função SQLSetDriverConnectInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54e37940062427008e9b90f6cda4cec825a721ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915295"
---
# <a name="sqlsetdriverconnectinfo-function"></a>Função SQLSetDriverConnectInfo
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,81: ODBC  
  
 **Resumo**  
 **SQLSetDriverConnectInfo** é usado para definir a cadeia de conexão no token de informações de conexão para a chamada **SQLDriverConnect** de um aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>Argumentos  
 *TokenHandle*  
 Entrada Identificador de token.  
  
 *Inconnectionstring*  
 Entrada Uma cadeia de conexão completa (consulte a sintaxe em "Comentários" em [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)), uma cadeia de conexão parcial ou uma cadeia de caracteres vazia.  
  
 *StringLength1*  
 Entrada Comprimento de **Inconnectionstring*, em caracteres, se a cadeia de caracteres for Unicode, ou bytes se a cadeia de caracteres for ANSI ou DBCS.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 O mesmo que [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) relacionado a qualquer erro de validação de entrada, exceto pelo fato de o Gerenciador de driver usar um **handletype** de SQL_HANDLE_DBC_INFO_TOKEN e um **identificador** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 Sempre que um driver retorna SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de driver retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornar SQL_SUCCESS_WITH_INFO, o Gerenciador de driver obterá as informações de diagnóstico de *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexões com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi. h para o desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
