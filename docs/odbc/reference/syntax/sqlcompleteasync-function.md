---
title: Função SQLCompleteAsync | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e09d61ef516e846798dd3af2d07dafa78af4605
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299650"
---
# <a name="sqlcompleteasync-function"></a>Função SQLCompleteAsync
**Conformidade**  
 Versão introduzida: ODBC 3.8  
  
 Conformidade com as normas: nenhuma  
  
 **Resumo**  
 **O SQLCompleteAsync** pode ser usado para determinar quando uma função assíncrona é concluída usando processamento baseado em notificação ou pesquisa. Para obter mais informações sobre operações assíncronas, consulte [Execução Assíncrona](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **O SQLCompleteAsync** só é implementado no Gerenciador de Driver scbc.  
  
 No modo de processamento assíncrono baseado em notificação, **o SQLCompleteAsync** deve ser chamado depois que o Driver Manager levantar o objeto de evento usado para notificação. **O SQLCompleteAsync** completa o processamento assíncrono e a função assíncrona gerará um código de retorno.  
  
 No modo de processamento assíncrono baseado em pesquisa, **o SQLCompleteAsync** é uma alternativa para chamar a função assíncrona original, sem precisar especificar os argumentos na chamada de função assíncrona original. **O SQLCompleteAsync** pode ser usado independentemente de a Biblioteca cursor do ODBC estar ativada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Handletype*  
 [Entrada] O tipo de alça sobre a qual completar o processamento assíncrono. Os valores válidos são SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] A alça sobre a qual completar o processamento assíncrono. Se *o Handle* não for uma alça válida do tipo especificado pelo *HandleType,* o **SQLCompleteAsync** retorna SQL_INVALID_HANDLE.  
  
 Se *o Handle* não for uma alça válida do tipo especificado pelo *HandleType,* o **SQLCompleteAsync** retorna SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 [Saída] Ponteiro para um buffer que conterá o código de retorno da API assíncrona. Se *o AsyncRetCodePtr* for NULL, **o SQLCompleteAsync** retorna SQL_ERROR.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Se **o SQLCompleteAsync** retornar SQL_SUCCESS, um aplicativo deve obter o código de retorno da função assíncrona a partir do buffer apontado pelo *AsyncRetCodePtr*. O SQLSTATE associado, se houver, pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma alça de declaração ou um *HandleType* de SQL_HANDLE_DBC e uma alça de conexão. Esses registros de diagnóstico estão associados à função assíncrona, não a esta função **SQLCompleteAsync.**  
  
 **SQLCompleteAsync** retorna um código diferente de SQL_SUCCESS para indicar que **o SQLCompleteAsync** não é chamado corretamente. **SQLCompleteAsync** não publicará nenhum registro de diagnóstico neste caso. Os possíveis códigos de devolução são:  
  
-   SQL_INVALID_HANDLE: A alça indicada pelo *HandleType* e *Handle* não é uma alça válida.  
  
-   SQL_ERROR: *AsyncRetCodePtr* é NULL ou o processamento assíncrono não está habilitado na alça.  
  
-   SQL_NO_DATA: No modo de notificação, uma operação assíncrona não está em andamento ou o Driver Manager não notificou o aplicativo. No modo de votação, uma operação assíncrona não está em andamento.  
  
## <a name="comments"></a>Comentários  
 No modo de processamento assíncrono baseado em pesquisa, *o AsyncRetCodePtr* pode ser SQL_STILL_EXECUTING quando **o SQLCompleteAsync** retornar SQL_SUCCESS. O aplicativo deve continuar votando até *que o AsyncRetCodePtr* não seja SQL_STILL_EXECUTING. No modo de processamento assíncrono baseado em notificação, *o AsyncRetCodePtr* nunca será SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução Assíncrona (Método de Votação)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
