---
title: sp_replication_agent_checkup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b434d4bda50cf03442020ba2f0c029aaa1e09cd9
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771227"
---
# <a name="spreplicationagentcheckup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Verifica cada banco de dados de distribuição para os agentes de replicação em execução, mas não têm histórico registrado no intervalo de pulsação. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @heartbeat_interval = ] 'heartbeat_interval'`É o número máximo de minutos que um agente pode acessar sem registrar uma mensagem de progresso. *heartbeat_interval* é **int**, com um padrão de 10 minutos.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **sp_replication_agent_checkup** gera o erro 14151 para cada agente detectado como suspeito. Também registra uma mensagem de histórico de falha sobre os agentes.  
  
## <a name="remarks"></a>Comentários  
 **sp_replication_agent_checkup** é usado na replicação de instantâneo, na replicação transacional e na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_replication_agent_checkup**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
