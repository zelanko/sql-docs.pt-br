---
title: Função SQLSetConnectInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b575e0d09f87ad21e1190b8081b6604349a98263
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301847"
---
# <a name="sqlsetconnectinfo-function"></a>Função SQLSetConnectInfo
**Conformidade**  
 Versão introduzida: ODBC 3.81 Normas De conformidade: ODBC  
  
 **Resumo**  
 **O SQLSetConnectInfo** é usado para definir a fonte de dados, o ID do usuário e a senha no token de informações de conexão para a chamada [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) de um aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>Argumentos  
 *TokenHandle*  
 [Entrada] Alça de token.  
  
 *Servername*  
 [Entrada] Nome da fonte dos dados. Os dados podem estar localizados no mesmo computador do programa, ou em outro computador em algum lugar em uma rede. Para obter informações sobre como um aplicativo escolhe uma fonte de dados, consulte [Escolher uma Fonte de Dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Entrada] Comprimento de **ServerName* em caracteres.  
  
 *Username*  
 [Entrada] Identificador de usuário.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento de **UserName* em caracteres.  
  
 *Autenticação*  
 [Entrada] Seqüência de autenticação (tipicamente a senha).  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento de **Autenticação* em caracteres.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 O mesmo que [o SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) para erros de validação de entrada, exceto que o Driver Manager usará um **HandleType** of SQL_HANDLE_DBC_INFO_TOKEN e uma **alça** do *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 Sempre que um driver retorna SQL_ERROR ou SQL_INVALID_HANDLE, o Driver Manager retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornar SQL_SUCCESS_WITH_INFO, o Driver Manager obterá as informações de diagnóstico do *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [no SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que suporta pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
