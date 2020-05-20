---
title: sp_refresh_log_shipping_monitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b375c1861d532445cd39d42f59f0a8d753e53b85
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828820"
---
# <a name="sp_refresh_log_shipping_monitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este procedimento armazenado atualiza as tabelas de monitor remoto com as últimas informações de um determinado servidor primário ou secundário para o agente de envio de logs especificado. O procedimento é invocado no servidor primário ou secundário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @agent_id = ] 'agent_id'`A ID primária para backup ou a ID secundária para cópia ou restauração. *agent_id* é **uniqueidentifier** e não pode ser NULL.  
  
`[ @agent_type = ] 'agent_type'`O tipo de trabalho de envio de logs.  
  
 0 = Backup.  
  
 1 = Cópia.  
  
 2 = restaurar.  
  
 *agent_type* é **tinyint** e não pode ser nulo.  
  
`[ @database = ] 'database'`O banco de dados primário ou secundário usado pelo registro em log por agentes de backup ou restauração.  
  
`[ @mode ] n`Especifica se os dados do monitor devem ser atualizados ou limpos. O tipo de dados de *m* é tinyint e os valores com suporte são:  
  
 1 = atualização (Este é o valor padrão).  
  
 2 = excluir  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 **sp_refresh_log_shipping_monitor** atualiza as tabelas **log_shipping_monitor_primary**, **log_shipping_monitor_secondary**, **log_shipping_monitor_history_detail**e **log_shipping_monitor_error_detail** com todas as informações de sessão que ainda não foram transferidas. Isto lhe permite sincronizar o servidor monitor com o servidor primário ou um secundário quando o monitor sair de sincronia por algum tempo. Além disso, permite-lhe limpar as informações de monitor no servidor monitor, se necessário.  
  
 **sp_refresh_log_shipping_monitor** deve ser executado do banco de dados **mestre** no servidor primário ou secundário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
