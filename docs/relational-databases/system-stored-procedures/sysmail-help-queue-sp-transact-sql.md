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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 40a6b569dc469f216d54e615fadd506e968db981
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807476"
---
# <a name="sysmail_help_queue_sp-transact-sql"></a>sysmail_help_queue_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Há duas filas no Database Mail: a fila de email e a fila de status. A fila de email armazena itens de email que estão esperando para serem enviados. A fila de status armazena o status de itens que já foram enviados. Este procedimento armazenado permite exibir o estado das filas de email ou de status. Se o parâmetro ** \@ queue_type** não for especificado, o procedimento armazenado retornará uma linha para cada uma das filas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @queue_type = ] 'queue_type'`O argumento opcional Exclui emails do tipo especificado como o *queue_type*. *queue_type* é **nvarchar (6)** sem padrão. As entradas válidas são **email** e **status**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar (6)**|O tipo de fila. Os valores possíveis são **email** e **status**.|  
|**length**|**int**|O número de itens de email na fila especificada.|  
|**state**|**nvarchar (64)**|Estado do monitor. Os valores possíveis são **INativos** (a fila está inativa), **notificado** (a fila foi notificada de que o recebimento deve ocorrer) e **RECEIVES_OCCURRING** (a fila está recebendo).|  
|**last_empty_rowset_time**|**HORÁRIO**|A data e a hora em que a fila estava vazia pela última vez. Em formato de hora militar e fuso horário GMT.|  
|**last_activated_time**|**HORÁRIO**|A data e a hora em que a fila foi ativada pela última vez. Em formato de hora militar e fuso horário GMT.|  
  
## <a name="remarks"></a>Comentários  
 Ao solucionar problemas de Database Mail, use **sysmail_help_queue_sp** para ver quantos itens estão na fila, o status da fila e quando ela foi ativada pela última vez.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, somente os membros da função de servidor fixa **sysadmin** podem acessar esse procedimento.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
