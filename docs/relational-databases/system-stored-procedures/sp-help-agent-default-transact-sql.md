---
description: sp_help_agent_default (Transact-SQL)
title: sp_help_agent_default (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_default
- sp_help_agent_default_TSQL
helpviewer_keywords:
- sp_help_agent_default
ms.assetid: 7ba55e39-05dd-43c7-b5da-b268ed8426dd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9df854b8199d265dff29277baf6ed9fe443bc46b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538869"
---
# <a name="sp_help_agent_default-transact-sql"></a>sp_help_agent_default (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Recupera a ID da configuração padrão para o tipo de agente passado como parâmetro. Esse procedimento armazenado é executado no Distribuidor, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_agent_default [ @profile_id= ] profile_id OUTPUT   
        , [ @agent_type = ] agent_type  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] _profile_idOUTPUT` É a ID da configuração padrão para o tipo de agente. *profile_id* é **int**, sem padrão. *profile_id* também é um parâmetro de saída e retorna a ID da configuração padrão para o tipo de agente.  
  
`[ @agent_type = ] 'agent_type'` É o tipo de agente. *agent_type* é **int**, sem padrão, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Snapshot Agent.|  
|**2**|Log Reader Agent.|  
|**3**|Distribution Agent.|  
|**4**|Merge Agent.|  
|**9**|Queue Reader Agent|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_help_agent_default** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **replmonitor** podem executar **sp_help_agent_default**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
