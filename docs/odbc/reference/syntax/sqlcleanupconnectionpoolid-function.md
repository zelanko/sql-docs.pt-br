---
title: Função SQLCleanupConnectionPoolID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4131ad3555a0206f500b28fc8df7b16a0f4ee707
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Função SQLCleanupConnectionPoolID
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.81 ODBC: ODBC  
  
 **Resumo**  
 **SQLCleanupConnectionPoolID** informa um driver que uma ID do pool foi atingida. Um pool de ID pode tempo limite sempre que todas as conexões em um pool associado a essa ID do pool foram atingido. Consulte [pool no Microsoft Data Access Components](http://msdn.microsoft.com/library/ms810829.aspx) para obter mais informações sobre o tempo limite de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] O identificador de ambiente do pool.  
  
 *PoolID*  
 [Entrada] O pool associado à ID do pool foi atingido.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 O Gerenciador de Driver não processará as informações de diagnóstico retornadas de **SQLCleanupConnectionPoolID**.  
  
 Um aplicativo não pode receber a mensagem de erro retornada pelo driver.  
  
## <a name="remarks"></a>Remarks  
 **SQLCleanupConnectionPoolID** pode ser chamado a qualquer momento, mas o Gerenciador de Driver garante que nenhum outro thread está chamando simultaneamente **SQLGetPoolID** e nenhum outro thread está chamando simultaneamente  **SQLRateConnection** e **SQLPoolConnect** com um token de informações de conexão atribuído com essa ID do pool. Portanto, o driver deve verificar se que essa função é thread-safe.  
  
 Um driver pode limpar os recursos associados com a ID do pool.  
  
 Aplicativos não devem chamar esta função diretamente. Um driver ODBC que oferece suporte ao pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
