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
manager: craigg
ms.openlocfilehash: 1c344315764eac32e2e63663f07b7f797571a0e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233434"
---
# <a name="sqlsetdriverconnectinfo-function"></a>Função SQLSetDriverConnectInfo
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.81 ODBC: ODBC  
  
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
 [Entrada] Uma cadeia de caracteres de conexão completa (consulte a sintaxe em "Comentários" em [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)), uma cadeia de caracteres de conexão parcial ou uma cadeia de caracteres vazia.  
  
 *StringLength1*  
 [Entrada] Comprimento de **InConnectionString*, em caracteres, se a cadeia de caracteres for Unicode ou bytes se a cadeia de caracteres é o ANSI ou DBCS.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Mesmo que [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) relacionados a qualquer erro de validação de entrada, exceto que o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e uma **manipular** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 Sempre que um driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de Driver retorna o erro para o aplicativo (no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornará SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver obterá as informações de diagnóstico da *hDbcInfoToken*e retornar SQL_SUCCESS_WITH_INFO para o aplicativo em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexão de reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão de reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
