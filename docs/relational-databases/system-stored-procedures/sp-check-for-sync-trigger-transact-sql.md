---
title: sp_check_for_sync_trigger (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- filter_TSQL
- sp_check_for_sync_trigger
helpviewer_keywords:
- sp_check_for_sync_trigger
ms.assetid: 54a1e2fd-c40a-43d4-ac64-baed28ae4637
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed3cd29b694e0e87f207376ad54b06fc0827b45b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43020255"
---
# <a name="spcheckforsynctrigger-transact-sql"></a>sp_check_for_sync_trigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Determina se um gatilho definido pelo usuário ou procedimento armazenado está sendo chamado no contexto de um gatilho de replicação usado para assinaturas de atualização imediata. Esse procedimento armazenado é executado no publicador do banco de dados de publicação ou no assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_check_for_sync_trigger [ @tabid = ] 'tabid'   
    [ , [ @trigger_op = ] 'trigger_output_parameters' OUTPUT ]  
    [ , [ @fonpublisher = ] fonpublisher ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@tabid =** ] '*tabid*'  
 É a ID de objeto da tabela onde gatilhos de atualização imediata estão sendo verificados. *tabid* está **int** sem nenhum padrão.  
  
 [ **@trigger_op =** ] '*trigger_output_parameters*' saída  
 Especifica se o parâmetro de saída deve retornar o tipo de gatilho de onde ele está sendo chamado. *trigger_output_parameters* está **char(10)** e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Ins**|Gatilho INSERT|  
|**UPD**|Gatilho UPDATE|  
|**/DEL**|Gatilho DELETE|  
|NULL (padrão)||  
  
 [  **@fonpublisher =** ] *fonpublisher*  
 Especifica o local onde o procedimento armazenado é executado. *fonpublisher* está **bit**, com um valor padrão de 0. Se for 0 a execução será no Assinante e se for 1 a execução será no Editor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 indica que o procedimento armazenado não está sendo chamado dentro do contexto de um gatilho da atualização imediata. 1 indica que ele está sendo chamado dentro do contexto de um gatilho de atualização imediata e é o tipo de gatilho que está sendo retornado em *@trigger_op*.  
  
## <a name="remarks"></a>Remarks  
 **sp_check_for_sync_trigger** é usado em replicação de instantâneo e replicação transacional.  
  
 **sp_check_for_sync_trigger** é usado para coordenar entre a replicação e gatilhos definidos pelo usuário. Esse procedimento armazenado determina se ele está sendo chamado dentro do contexto de um gatilho de replicação. Por exemplo, você pode chamar o procedimento **sp_check_for_sync_trigger** no corpo de um gatilho definido pelo usuário. Se **sp_check_for_sync_trigger** retorna **0**, o gatilho definido pelo usuário continua o processamento. Se **sp_check_for_sync_trigger** retorna **1**, o gatilho definido pelo usuário é encerrada. Isso assegura que o gatilho definido pelo usuário não seja disparado quando o gatilho de replicação atualizar a tabela.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra código que pode ser usado em um gatilho, em uma tabela de Assinante.  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int  
SELECT @table_id = object_id('tablename')  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT  
IF @retcode = 1  
RETURN  
```  
  
## <a name="example"></a>Exemplo  
 O código também pode ser adicionado a um gatilho em uma tabela no publicador; o código é semelhante, mas a chamada para **sp_check_for_sync_trigger** inclui um parâmetro adicional.  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int, @fonpublisher int  
SELECT @table_id = object_id('tablename')  
SELECT @fonpublisher = 1  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT, @fonpublisher  
IF @retcode = 1  
RETURN  
```  
  
## <a name="permissions"></a>Permissões  
 **sp_check_for_sync_trigger** procedimento armazenado pode ser executado por qualquer usuário com permissões SELECT em de [sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) exibição do sistema.  
  
## <a name="see-also"></a>Consulte também  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
