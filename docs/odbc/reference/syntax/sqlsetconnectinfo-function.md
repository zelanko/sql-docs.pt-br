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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 448b0f5e34a6b7421c23a1267dd9cd68bd93ca6f
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537177"
---
# <a name="sqlsetconnectinfo-function"></a>Função SQLSetConnectInfo
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.81 ODBC: ODBC  
  
 **Resumo**  
 **SQLSetConnectInfo** é usado para definir a fonte de dados, ID de usuário e senha para o token de informações de conexão para um aplicativo [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) chamar.  
  
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
 [Entrada] Identificador de token.  
  
 *ServerName*  
 [Entrada] Nome da fonte de dados. Os dados podem ser localizados no mesmo computador que o programa, ou em outro computador em algum lugar em uma rede. Para obter informações sobre como um aplicativo escolhe uma fonte de dados, consulte [escolhendo uma fonte de dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Entrada] Comprimento de **ServerName* em caracteres.  
  
 *UserName*  
 [Entrada] Identificador de usuário.  
  
 *NameLength2*  
 [Entrada] Comprimento de **nome de usuário* em caracteres.  
  
 *Autenticação*  
 [Entrada] Cadeia de caracteres de autenticação (normalmente a senha).  
  
 *NameLength3*  
 [Entrada] Comprimento de **autenticação* em caracteres.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Mesmo que [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) para erros de validação de entrada, exceto que o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e uma **manipular** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 Sempre que um driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de Driver retorna o erro para o aplicativo (no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornará SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver obterá as informações de diagnóstico da *hDbcInfoToken*e retornar SQL_SUCCESS_WITH_INFO para o aplicativo em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexão de reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão de reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
