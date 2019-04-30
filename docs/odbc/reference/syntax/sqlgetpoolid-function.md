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
manager: craigg
ms.openlocfilehash: 39b3d3d1ecdc21acee8b238f56cede0a59146bd2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132700"
---
# <a name="sqlgetpoolid-function"></a>Função SQLGetPoolID
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.81 ODBC: ODBC  
  
 **Resumo**  
 **SQLGetPoolID** recupera a ID do pool.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 [Entrada] Identificador de token que contém todas as informações de conexão.  
  
 *pPoolID*  
 [Saída] A ID do pool, que é usada para identificar um conjunto de conexões que podem ser usados alternadamente (possivelmente exigindo uma reinicialização adicional).  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetPoolID** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e uma **manipular** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 **SQLGetPoolID** é usado para obter a ID do pool dada um conjunto de informações de conexão (do **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**, e  **SQLSetConnectInfo**). Esse pool ID é usada para identificar um conjunto de conexões que podem ser usados alternadamente (possivelmente exigindo uma reinicialização adicional). A ID do pool será ser usada para identificar o pool de conexão para esse grupo de conexões.  
  
 Sempre que um driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de Driver retorna o erro para o aplicativo (no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornará SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver obterá as informações de diagnóstico da *hDbcInfoToken*e retornar SQL_SUCCESS_WITH_INFO para o aplicativo em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexão de reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão de reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
