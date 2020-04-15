---
title: Função SqlSetDriverConnectInfo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10336475e39598161126c13771ad822de0d5f7d8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298791"
---
# <a name="sqlsetdriverconnectinfo-function"></a>Função SQLSetDriverConnectInfo
**Conformidade**  
 Versão introduzida: ODBC 3.81 Normas De conformidade: ODBC  
  
 **Resumo**  
 **SQLSetDriverConnectInfo** é usado para definir a seqüência de conexões no token de informações de conexão para a chamada **SQLDriverConnect** de um aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>Argumentos  
 *TokenHandle*  
 [Entrada] Alça de token.  
  
 *String de inconexão*  
 [Entrada] Uma seqüência de conexão completa (veja a sintaxe em "Comentários" no [SQLDriverConnect),](../../../odbc/reference/syntax/sqldriverconnect-function.md)uma seqüência de conexão parcial ou uma seqüência de string vazia.  
  
 *Comprimento da corda1*  
 [Entrada] Comprimento de **InConnectionString*, em caracteres se a seqüência é Unicode, ou bytes se string é ANSI ou DBCS.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 O mesmo que [o SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) relacionado a qualquer erro de validação de entrada, exceto que o Driver Manager usará um **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e uma **alça** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 Sempre que um driver retorna SQL_ERROR ou SQL_INVALID_HANDLE, o Driver Manager retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornar SQL_SUCCESS_WITH_INFO, o Driver Manager obterá as informações de diagnóstico do *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [no SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que suporta pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
