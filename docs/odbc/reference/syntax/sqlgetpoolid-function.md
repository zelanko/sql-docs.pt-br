---
title: Função SQLGetpoolID | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32cc973f4dab5bde7bcedade0365d233987dda72
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303313"
---
# <a name="sqlgetpoolid-function"></a>Função SQLGetPoolID
**Conformidade**  
 Versão introduzida: ODBC 3.81 Normas De conformidade: ODBC  
  
 **Resumo**  
 **SQLGetPoolID** recupera o ID do pool.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 [Entrada] Cabo de token que contém todas as informações de conexão.  
  
 *pPoolID*  
 [Saída] O ID do pool, que é usado para identificar um conjunto de conexões que podem ser usadas de forma intercambiável (possivelmente exigindo um reset adicional).  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetPoolID** retornar SQL_ERROR ou SQL_SUCCESS_WITH_INFO, o Gerenciador de driver usará um **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e uma **alça** do *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 **O SQLGetPoolID** é usado para obter o ID do pool dado um conjunto de informações de conexão (de **SQLSetConnectAttrForDbcInfo,** **SQLSetDriverConnectInfo**e **SQLSetConnectInfo**). Este ID do pool é usado para identificar um conjunto de conexões que podem ser usadas de forma intercambiável (possivelmente exigindo um reset adicional). O ID do pool será usado para identificar o pool de conexões para esse grupo de conexões.  
  
 Sempre que um driver retorna SQL_ERROR ou SQL_INVALID_HANDLE, o Driver Manager retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornar SQL_SUCCESS_WITH_INFO, o Driver Manager obterá as informações de diagnóstico do *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [no SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que suporta pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
