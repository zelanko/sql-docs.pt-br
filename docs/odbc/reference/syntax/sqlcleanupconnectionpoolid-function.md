---
title: SQLCleanupConnectionPoolID Function | Microsoft Docs
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
ms.openlocfilehash: a74a92cc05ecd41e99ff87642c7fe3ee527e0c98
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301316"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>Função SQLCleanupConnectionPoolID
**Conformidade**  
 Versão introduzida: ODBC 3.81 Normas De conformidade: ODBC  
  
 **Resumo**  
 **SQLCleanupConnectionPoolID** informa um driver que um ID do pool foi cronometrado. Um ID de pool pode ter tempo total sempre que todas as conexões em uma piscina associadas a esse ID de pool foram cronometradas. Consulte [Pooling nos Componentes de Acesso a Dados da Microsoft](https://msdn.microsoft.com/library/ms810829.aspx) para obter mais informações sobre o tempo de intervalo de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] O manuseie do ambiente da piscina.  
  
 *Poolid*  
 [Entrada] A piscina associada ao ID da piscina que foi cronometrado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 O Gerenciador de driver não processará informações de diagnóstico retornadas do **SQLCleanupConnectionPoolID**.  
  
 Um aplicativo não pode receber a mensagem de erro devolvida pelo motorista.  
  
## <a name="remarks"></a>Comentários  
 **SQLCleanupConnectionPoolID** pode ser chamado a qualquer momento, mas o Driver Manager garante que nenhum outro segmento está chamando simultaneamente **de SQLGetPoolID** e nenhum outro segmento está chamando simultaneamente **sQLRateConnection** e **SQLPoolConnect** com um token de informações de conexão atribuído com esse ID do pool. Portanto, o motorista deve certificar-se de que esta função é segura para rosca.  
  
 Um motorista pode limpar os recursos associados ao Pool ID.  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que suporta pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
