---
description: Função SQLCleanupConnectionPoolID
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20ad05559aa172ff7e8937359bad93f85347a92a
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193441"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Função SQLCleanupConnectionPoolID
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,81: ODBC  
  
 **Resumo**  
 **SQLCleanupConnectionPoolID** informa um driver de que a ID do pool atingiu o tempo limite. Uma ID de pool pode expirar sempre que todas as conexões em um pool associado a essa ID de pool esgotaram o tempo limite. Consulte [pooling nos componentes de acesso a dados da Microsoft](/previous-versions/ms810829(v=msdn.10)) para obter mais informações sobre o tempo limite de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 Entrada O identificador de ambiente do pool.  
  
 *Poolid*  
 Entrada O pool associado à ID do pool que atingiu o tempo limite.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 O Gerenciador de driver não processará as informações de diagnóstico retornadas de **SQLCleanupConnectionPoolID**.  
  
 Um aplicativo não pode receber a mensagem de erro retornada pelo driver.  
  
## <a name="remarks"></a>Comentários  
 **SQLCleanupConnectionPoolID** pode ser chamado a qualquer momento, mas o Gerenciador de driver garante que nenhum outro thread esteja chamando **SQLGetPoolID** simultaneamente e nenhum outro thread esteja chamando simultaneamente **SQLRateConnection** e **SQLPoolConnect** com um token de informações de conexão atribuído com a ID do pool. Portanto, o driver deve verificar se essa função é thread-safe.  
  
 Um driver pode limpar os recursos associados à ID do pool.  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexões com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi. h para o desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)