---
title: Função SQLAsyncNotificationCallback | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78764e1dccb7118d43cc967f3b03838366d6eb0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758044"
---
# <a name="sqlasyncnotificationcallback-function"></a>Função SQLAsyncNotificationCallback
**Conformidade com**  
 Versão introduzida: ODBC 3.8  
  
 Conformidade com padrões: nenhum  
  
 **Resumo**  
 **SQLAsyncNotificationCallback** permite que um driver de retorno de chamada para o Gerenciador de Driver quando há algum progresso da operação assíncrona atual depois que o driver retornará SQL_STILL_EXECUTING. **SQLAsyncNotificationCallback** pode apenas chamado pelo driver.  
  
 Drivers não chamam **SQLAsyncNotificationCallback** com o nome da função **SQLAsyncNotificationCallback**. Em vez disso, o Gerenciador de Driver passa um ponteiro de função para um driver como o valor para o atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK do identificador de conexão correspondente ou identificador de instrução respectivamente. Identificadores diferentes podem ser atribuídos valores de ponteiro de função diferente. O tipo de ponteiro de função é definido como SQL_ASYNC_NOTIFICATION_CALLBACK.  
  
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
 Usado por um driver para indica que esta chamada de função de retorno de chamada é a última para a operação assíncrona atual. O driver retornará um código de retorno diferente de SQL_STILL_EXECUTING quando o Gerenciador de Driver chama a função novamente. O Gerenciador de Driver pode usar essas informações, por exemplo, para informar o aplicativo com antecedência que concluirá a operação assíncrona.  
  
 Se *manipular* não é um identificador válido do tipo especificado por *HandleType*, **SQLCancelHandle** retorne SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS ou SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnóstico  
 **SQLAsyncNotificationCallback** pode retornar SQL_ERROR para duas situações a seguir (eles indicam um problema de implementação no Gerenciador de Driver ou driver.  
  
|Erro|Description|  
|-----------|-----------------|  
|Conexão ou a instrução não solicitou a notificação.||  
|Inválido *manipular*|O driver passado um identificador inválido, o que falhou nos testes de validação interno do Gerenciador de Driver.|  
  
## <a name="see-also"></a>Consulte também  
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
