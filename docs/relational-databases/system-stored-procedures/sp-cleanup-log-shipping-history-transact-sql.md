---
title: sp_cleanup_log_shipping_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cleanup_log_shipping_history_TSQL
- sp_cleanup_log_shipping_history
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cleanup_log_shipping_history
ms.assetid: 96d236a9-1d0e-4f83-a4d3-f825b7381e46
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7470baabb9a35a923995d8306b314f9272de0b5c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070376"
---
# <a name="sp_cleanup_log_shipping_history-transact-sql"></a>sp_cleanup_log_shipping_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este procedimento armazenado limpa o histórico localmente e no servidor monitor com base no período de retenção.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cleanup_log_shipping_history  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @agent_id = ] 'agent_id',`A ID primária para backup ou a ID secundária para cópia ou restauração. *agent_id* é **uniqueidentifier** e não pode ser NULL.  
  
`[ @agent_type = ] 'agent_type'`O tipo de trabalho de envio de logs. 0 = Backup, 1 = Copiar, 2 = Restaurar. *agent_type* é **tinyint** e não pode ser nulo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 **sp_cleanup_log_shipping_history** deve ser executado do banco de dados **mestre** em qualquer servidor de envio de logs. Esse procedimento armazenado limpa cópias locais e remotas de **log_shipping_monitor_history_detail** e **log_shipping_monitor_error_detail** com base no período de retenção do histórico.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
