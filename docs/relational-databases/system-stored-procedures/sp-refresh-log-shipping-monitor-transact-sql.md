---
title: sp_refresh_log_shipping_monitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f2f0bf6df228f7a0948b0c5d295ae6d2cdf4a9b9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sprefreshlogshippingmonitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este procedimento armazenado atualiza as tabelas de monitor remoto com as últimas informações de um determinado servidor primário ou secundário para o agente de envio de logs especificado. O procedimento é invocado no servidor primário ou secundário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@agent_id=** ] **'***agent_id***'**  
 A ID primária para backup ou ID secundária para cópia ou restauração. *agent_id* é **uniqueidentifier** e não pode ser NULL.  
  
 [ **@agent_type=** ] **'***agent_type***'**  
 O tipo de trabalho de envio de log.  
  
 0 = Backup.  
  
 1 = Cópia.  
  
 2 = restaurar.  
  
 *agent_type* é **tinyint** e não pode ser NULL.  
  
 [  **@database=** ] **'***banco de dados***'**  
 O banco de dados primário ou secundário utilizado no log por backup ou agentes de restauração.  
  
 [ **@mode** ] *n*  
 Especifica se os dados de monitor devem ser atualizados ou limpos. O tipo de dados *m* é tinyint e os valores suportados são:  
  
 1 = atualização (Este é o valor padrão).  
  
 2 = excluir  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma.  
  
## <a name="remarks"></a>Remarks  
 **sp_refresh_log_shipping_monitor** atualiza o **log_shipping_monitor_primary**, **log_shipping_monitor_secondary**, **log_shipping_monitor_history_detail** , e **log_shipping_monitor_error_detail** tabelas com quaisquer informações de sessão que já não foi transferido. Isto lhe permite sincronizar o servidor monitor com o servidor primário ou um secundário quando o monitor sair de sincronia por algum tempo. Além disso, permite-lhe limpar as informações de monitor no servidor monitor, se necessário.  
  
 **sp_refresh_log_shipping_monitor** deve ser executado a partir de **mestre** banco de dados no servidor primário ou secundário.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor pode executar esse procedimento.  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
