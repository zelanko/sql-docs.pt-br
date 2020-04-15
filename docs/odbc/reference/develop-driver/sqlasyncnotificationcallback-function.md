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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6c182c48b8e5ddb70204ddd3a94d9651f97595d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294533"
---
# <a name="sqlasyncnotificationcallback-function"></a>Função SQLAsyncNotificationCallback
**Conformidade**  
 Versão introduzida: ODBC 3.8  
  
 Conformidade com as normas: nenhuma  
  
 **Resumo**  
 **SQLAsyncNotificationCallback** permite que um driver ligue de volta para o Driver Manager quando houver algum progresso para a operação assíncrona atual após o retorno do driver SQL_STILL_EXECUTING. **SQLAsyncNotificationCallback** só pode ser chamado pelo driver.  
  
 Os drivers não chamam **SQLAsyncNotificationCallback** com o nome da função **SQLAsyncNotificationCallback**. Em vez disso, o Driver Manager passa um ponteiro de função para um driver como o valor para o SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK ou SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK atributo da alça de conexão correspondente ou alça de instrução, respectivamente. Diferentes alças podem ser atribuídas diferentes valores de ponteiro de função. O tipo de ponteiro de função é definido como SQL_ASYNC_NOTIFICATION_CALLBACK.  
  
 **SQLAsyncNotificationCallback** é seguro para rosca. Um driver pode optar por usar vários threads chamando **SQLAsyncNotificationCallback** em diferentes alças simultaneamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pContex*  
 Ponteiro para uma estrutura de dados definida pelo Driver Manager. O valor é passado para o driver via SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) ou SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT).  O motorista não tem acesso ao valor.  
  
 *fLast*  
 Usado por um driver para indicar que essa invocação da função de retorno de chamada é a última para a operação assíncrona atual. O motorista retornará um código de retorno diferente SQL_STILL_EXECUTING quando o Gerenciador de Driver chamar a função novamente. O Driver Manager pode usar essas informações, por exemplo, para informar o aplicativo com antecedência que a operação assíncrona será concluída.  
  
 Se *o Handle* não for uma alça válida do tipo especificado pelo *HandleType,* **o SQLCancelHandle** retorna SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS ou SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLAsyncNotificationCallback** pode retornar SQL_ERROR para as duas situações seguintes (estas indicam um problema de implementação no driver ou driver manager.  
  
|Erro|Descrição|  
|-----------|-----------------|  
|A conexão ou declaração não solicitou notificação.||  
|Alça *inválida*|O motorista passou em uma alça inválida, que falhou nos testes internos de validação do Driver Manager.|  
  
## <a name="see-also"></a>Consulte Também  
 [Execução Assíncrona (Método de Votação)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
