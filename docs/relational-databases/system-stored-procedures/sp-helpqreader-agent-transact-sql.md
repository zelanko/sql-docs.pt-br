---
description: sp_helpqreader_agent (Transact-SQL)
title: sp_helpqreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c638e7895d95518f59627643deb0b0070a19fa70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489273"
---
# <a name="sp_helpqreader_agent-transact-sql"></a>sp_helpqreader_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Retorna propriedades do Queue Reader Agent. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição, ou no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @frompublisher = ] frompublisher` Especifica se o procedimento armazenado é chamado no Publicador ou no distribuidor. *frompublisher* é bit, com um valor padrão de 0. **1** significa que o procedimento armazenado é chamado do Publicador e **0** significa que o procedimento armazenado é chamado a partir do distribuidor.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do agente.|  
|**name**|**nvarchar (100)**|O nome do agente.|  
|**job_id**|**uniqueidentifier**|ID exclusiva do trabalho de agente.|  
|**job_login**|**nvarchar(512)**|É a conta do Windows na qual o Distribution Agent é executado, que é retornado no formato *domínio* \\ *nome de usuário*.|  
|**job_password**|**sysname**|Por motivos de segurança, um valor de **\*\*\*\*\*\*\*\*\*\*** é sempre retornado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpqreader_agent** é usado na replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Quando o valor de *frompublisher* é **1**, somente os membros da função de servidor fixa **sysadmin** no Publicador ou membros da função de banco de dados fixa **db_owner** no banco de dados de publicação podem ser executados **sp_helpqreader_agent**. Caso contrário, somente os membros da função de servidor fixa **sysadmin** no distribuidor ou membros da função de banco de dados fixa **db_owner** no banco de dados de distribuição poderão executar **sp_helpqreader_agent**.  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar atualização de assinaturas para publicações transacionais](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
