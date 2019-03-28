---
title: sysmail_help_queue_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73ca766827c1b6149bcb40cec8adefe86e944890
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531698"
---
# <a name="sysmailhelpqueuesp-transact-sql"></a>sysmail_help_queue_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Há duas filas no Database Mail: a fila de email e a fila de status. A fila de email armazena itens de email que estão esperando para serem enviados. A fila de status armazena o status de itens que já foram enviados. Este procedimento armazenado permite exibir o estado das filas de email ou de status. Se o parâmetro **@queue_type** não for especificado, o procedimento armazenado retorna uma linha para cada uma das filas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @queue_type = ] 'queue_type'` Argumento opcional exclui emails do tipo especificado como o *queue_type*. *QUEUE_TYPE* está **nvarchar(6)** sem nenhum padrão. As entradas válidas são **mail** e **status**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar(6)**|O tipo de fila. Os valores possíveis são **mail** e **status**.|  
|**Comprimento**|**int**|O número de itens de email na fila especificada.|  
|**state**|**nvarchar(64)**|Estado do monitor. Os valores possíveis são **INACTIVE** (a fila é inativa), **NOTIFIED** (fila foi notificada recebimento ocorra), e **RECEIVES_OCCURRING** (a fila está recebendo).|  
|**last_empty_rowset_time**|**DATETIME**|A data e a hora em que a fila estava vazia pela última vez. Em formato de hora militar e fuso horário GMT.|  
|**last_activated_time**|**DATETIME**|A data e a hora em que a fila foi ativada pela última vez. Em formato de hora militar e fuso horário GMT.|  
  
## <a name="remarks"></a>Comentários  
 Ao solucionar problemas de Database Mail, use **sysmail_help_queue_sp** para ver quantos itens estão na fila, o status da fila e quando ele foi ativado.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, somente os membros dos **sysadmin** função de servidor fixa pode acessar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna as filas de email e de status.  
  
```  
EXECUTE msdb.dbo.sysmail_help_queue_sp ;  
GO  
```  
  
 Este conjunto de resultados de amostra foi editado para comprimento.  
  
```  
queue_type length      state              last_empty_rowset_time  last_activated_time  
---------- -------- ------------------ ----------------------- -----------------------  
mail       0        RECEIVES_OCCURRING 2005-10-07 21:14:47.010 2005-10-10 20:52:51.517  
status     0        INACTIVE           2005-10-07 21:04:47.003 2005-10-10 21:04:47.003  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
