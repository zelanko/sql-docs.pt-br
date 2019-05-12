---
title: Função SQLCleanupConnectionPoolID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4d00fcff0b2fa1948f6b2f6f66b863501e12d97
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537694"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Função SQLCleanupConnectionPoolID
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.81 ODBC: ODBC  
  
 **Resumo**  
 **SQLCleanupConnectionPoolID** informa um driver que uma ID do pool foi atingida. Um pool de ID podem tempo limite sempre que todas as conexões em um pool associado com essa ID do pool estavam atingiu o tempo limite. Ver [Pooling no Microsoft Data Access Components](https://msdn.microsoft.com/library/ms810829.aspx) para obter mais informações sobre o tempo limite da conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
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
  
## <a name="diagnostics"></a>Diagnóstico  
 O Gerenciador de Driver não processará as informações de diagnóstico retornadas de **SQLCleanupConnectionPoolID**.  
  
 Um aplicativo não pode receber a mensagem de erro retornada pelo driver.  
  
## <a name="remarks"></a>Comentários  
 **SQLCleanupConnectionPoolID** pode ser chamado a qualquer momento, mas o Gerenciador de Driver garante que nenhum outro thread é chamando simultaneamente **SQLGetPoolID** e nenhum outro thread é chamando simultaneamente  **SQLRateConnection** e **SQLPoolConnect** com um token de informações de conexão atribuído com essa ID do pool. Portanto, o driver deve verificar que essa função é thread-safe.  
  
 Um driver pode limpar todos os recursos associados com a ID do pool.  
  
 Aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexão de reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão de reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
