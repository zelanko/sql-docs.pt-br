---
title: "Função SQLGetPoolID | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec2da5abd62e659529eb364c7673317c86f4c97e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetpoolid-function"></a>Função SQLGetPoolID
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.81 ODBC: ODBC  
  
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
 [Saída] A ID do pool, que é usada para identificar um conjunto de conexões que podem ser usadas intercambiavelmente (possivelmente exigir uma reinicialização adicional).  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetPoolID** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e um **tratar** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Remarks  
 **SQLGetPoolID** é usada para obter a ID do pool dada um conjunto de informações de conexão (de **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**, e  **SQLSetConnectInfo**). Esse pool de ID é usada para identificar um conjunto de conexões que podem ser usadas intercambiavelmente (possivelmente exigir uma reinicialização adicional). A ID do pool usará para identificar o pool de conexão para esse grupo de conexões.  
  
 Sempre que um driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de Driver retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retorna SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver obterá as informações de diagnóstico de *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO para o aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Aplicativos não devem chamar esta função diretamente. Um driver ODBC que oferece suporte ao pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
