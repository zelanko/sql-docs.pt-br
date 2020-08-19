---
description: Função SQLAsyncNotificationCallback
title: Função SQLAsyncNotificationCallback | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9d03e8a3fa7e62c19dd09a210dca3a56348c692
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476225"
---
# <a name="sqlasyncnotificationcallback-function"></a>Função SQLAsyncNotificationCallback
**Conformidade**  
 Versão introduzida: ODBC 3,8  
  
 Conformidade com padrões: nenhuma  
  
 **Resumo**  
 O **SQLAsyncNotificationCallback** permite que um driver chame de volta para o Gerenciador de driver quando há algum progresso para a operação assíncrona atual depois que o driver retorna SQL_STILL_EXECUTING. **SQLAsyncNotificationCallback** só pode ser chamado pelo driver.  
  
 Os drivers não chamam **SQLAsyncNotificationCallback** com o nome de função **SQLAsyncNotificationCallback**. Em vez disso, o Gerenciador de driver passa um ponteiro de função para um driver como o valor para o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK do identificador de conexão ou identificador de instrução correspondente, respectivamente. Diferentes identificadores podem ser atribuídos a diferentes valores de ponteiro de função. O tipo do ponteiro de função é definido como SQL_ASYNC_NOTIFICATION_CALLBACK.  
  
 **SQLAsyncNotificationCallback** é thread-safe. Um driver pode optar por usar vários threads chamando **SQLAsyncNotificationCallback** em identificadores diferentes simultaneamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pContex*  
 Ponteiro para uma estrutura de dados definida pelo Gerenciador de driver. O valor é passado para o driver via SQLSetConnectAttr (SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) ou SQLSetStmtAttr (SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT).  O driver não tem acesso ao valor.  
  
 *fLast*  
 Usado por um driver para indicar que essa invocação de função de retorno de chamada é a última para a operação assíncrona atual. O driver retornará um código de retorno diferente de SQL_STILL_EXECUTING quando o Gerenciador de driver chamar a função novamente. O Gerenciador de driver pode usar essas informações, por exemplo, para informar ao aplicativo com antecedência que a operação assíncrona será concluída.  
  
 Se o *identificador* não for um identificador válido do tipo especificado por *HandleType*, **SQLCancelHandle** retornará SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS ou SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLAsyncNotificationCallback** pode retornar SQL_ERROR para as duas situações a seguir (elas indicam um problema de implementação no driver ou no Gerenciador de driver.  
  
|Erro|Descrição|  
|-----------|-----------------|  
|A conexão ou instrução não solicitou notificação.||  
|*Identificador* inválido|O driver passou em um identificador inválido, que falhou nos testes de validação internos do Gerenciador de driver.|  
  
## <a name="see-also"></a>Consulte Também  
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
