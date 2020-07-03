---
title: sp_dropanonymousagent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: acf909be9ca1185ea441acf27a60409e1c868328
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85859979"
---
# <a name="sp_dropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Descarta um agente anônimo para monitoramento de replicação no distribuidor do Publicador. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @subid = ] sub_id`É o identificador global de uma assinatura anônima. *sub_id* é **uniqueidentifier**, sem padrão. Esse identificador pode ser recuperado no Assinante usando **sp_helppullsubscription**. O valor no campo **subid** do conjunto de resultados retornado é esse identificador global.  
  
`[ @type = ] type`É o tipo de assinatura. o *tipo* é **int**, sem padrão. Os valores válidos são **1** ou **2**. Especifique **1**, se a replicação de instantâneo ou a replicação transacional usando o agente de distribuição. Especifique **2**, se a replicação de mesclagem usar o agente de mesclagem.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropanonymousagent** é usado em todos os tipos de replicação.  
  
 Esse procedimento armazenado é usado para descartar agentes de assinatura anônimos e não pode ser usado para descartar assinaturas conhecidas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de banco de dados fixa **db_owner** no banco de dados de distribuição podem executar **sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
