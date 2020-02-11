---
title: Função SQLGetPoolID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7daef4785a77df294a831d69089108cbb1d88489
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061480"
---
# <a name="sqlgetpoolid-function"></a>Função SQLGetPoolID
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,81: ODBC  
  
 **Resumo**  
 **SQLGetPoolID** recupera a ID do pool.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 Entrada Identificador de token que contém todas as informações de conexão.  
  
 *pPoolID*  
 Der A ID do pool, que é usada para identificar um conjunto de conexões que podem ser usadas de forma intercambiável (possivelmente exigindo uma redefinição adicional).  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetPoolID** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, o Gerenciador de driver usará um **handletype** de SQL_HANDLE_DBC_INFO_TOKEN e um **identificador** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 **SQLGetPoolID** é usado para obter a ID do pool de acordo com um conjunto de informações de conexão (de **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**e **SQLSetConnectInfo**). Essa ID de pool é usada para identificar um conjunto de conexões que podem ser usadas de forma intercambiável (possivelmente exigindo uma redefinição adicional). A ID do pool será usada para identificar o pool de conexões para esse grupo de conexões.  
  
 Sempre que um driver retorna SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de driver retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornar SQL_SUCCESS_WITH_INFO, o Gerenciador de driver obterá as informações de diagnóstico de *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexões com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi. h para o desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
