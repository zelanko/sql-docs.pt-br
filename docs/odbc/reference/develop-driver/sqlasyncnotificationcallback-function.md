---
title: "Função SQLAsyncNotificationCallback | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 615792da52bcdc2dd12775d2c62450f95364b115
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlasyncnotificationcallback-function"></a>Função SQLAsyncNotificationCallback
**Conformidade**  
 Versão introduzidas: ODBC 3.8  
  
 Conformidade com padrões: nenhum  
  
 **Resumo**  
 **SQLAsyncNotificationCallback** permite que um driver de retorno de chamada para o Gerenciador de Driver quando há algum progresso da operação assíncrona atual depois que o driver retornará SQL_STILL_EXECUTING. **SQLAsyncNotificationCallback** apenas chamado pelo driver.  
  
 Drivers não chamam **SQLAsyncNotificationCallback** com o nome de função **SQLAsyncNotificationCallback**. Em vez disso, o Gerenciador de Driver passa um ponteiro de função para um driver como o valor para o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK do identificador de conexão correspondente ou identificador de instrução respectivamente. Identificadores diferentes podem ser atribuídos valores de ponteiro de função diferente. O tipo de ponteiro de função é definido como SQL_ASYNC_NOTIFICATION_CALLBACK.  
  
 **SQLAsyncNotificationCallback** é thread-safe. Um driver pode optar por usar vários threads chamando **SQLAsyncNotificationCallback** em diferentes manipula simultaneamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pContex*  
 Ponteiro para uma estrutura de dados definido pelo Gerenciador de Driver. O valor é passado para o driver por meio de SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) ou SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT).  O driver não tem acesso ao valor.  
  
 *fLast*  
 Usado por um driver para indica que esta chamada de função de retorno de chamada é o último para a operação assíncrona atual. O driver retornará um código de retorno diferente de SQL_STILL_EXECUTING quando o Gerenciador de Driver chama a função novamente. O Gerenciador de Driver pode usar essas informações, por exemplo, para informar ao aplicativo antes que a operação assíncrona será concluída.  
  
 Se *tratar* não é um identificador válido do tipo especificado pelo *HandleType*, **SQLCancelHandle** retorne SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS ou SQL_ERROR.  
  
## <a name="diagnostics"></a>diagnóstico  
 **SQLAsyncNotificationCallback** pode retornar SQL_ERROR para duas situações a seguir (eles indicam um problema de implementação no driver ou o Gerenciador de Driver.  
  
|Erro|Description|  
|-----------|-----------------|  
|Conexão ou instrução não solicitou a notificação.||  
|Inválido *tratar*|O driver passado um identificador inválido, o que falhou nos testes de validação interno do Gerenciador de Driver.|  
  
## <a name="see-also"></a>Consulte também  
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
