---
title: sp_update_operator (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38da9010e434570fbcd75e026f11c50450e10691
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="spupdateoperator-transact-sql"></a>sp_update_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza informações sobre um operador (recipiente de notificação) para ser usado com alertas e trabalhos.  
  
   ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]  
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]  
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]  
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @name=] '*nome*'  
 O nome do operador a ser modificado. *nome* é **sysname**, sem padrão.  
  
 [ @new_name=] '*novo_nome*'  
 O novo nome do operador. Esse nome deve ser exclusivo. *Novo_nome* é **sysname**, com um padrão NULL.  
  
 [ @enabled=] *habilitado*  
 Um número que indica o status atual do operador (**1** se habilitado, **0** se não estiver). *habilitado* é **tinyint**, com um padrão NULL. Se não estiver habilitado, um operador não receberá notificações de alerta.  
  
 [ @email_address=] '*email_address*'  
 O endereço de email do operador. Essa cadeia de caracteres é passada diretamente para o sistema de email. *endereço de email* é **nvarchar (100)**, com um padrão NULL.  
  
 [ @pager_address=] '*pager_number*'  
 O endereço de pager do operador. Essa cadeia de caracteres é passada diretamente para o sistema de email. *pager_number* é **nvarchar (100)**, com um padrão NULL.  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 Especifica a hora depois da qual uma notificação de pager pode ser enviada a esse operador, de segunda-feira a sexta-feira. *weekday_pager_start_time*é **int**, com um padrão NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 Especifica a hora depois da qual uma notificação de pager não pode ser enviada ao operador especificado, de segunda-feira a sexta-feira. *weekday_pager_end_time*é **int**, com um padrão NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 Especifica a hora depois da qual uma notificação de pager pode ser enviada ao operador aos sábados. *saturday_pager_start_time*é **int**, com um padrão NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 Especifica a hora depois da qual uma notificação de pager não pode ser enviada ao operador aos sábados. *saturday_pager_end_time*é **int**, com um padrão NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 Especifica a hora depois da qual uma notificação de pager pode ser enviada ao operador aos domingos. *sunday_pager_start_time*é **int**, com um padrão NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 Especifica a hora depois da qual uma notificação de pager não pode ser enviada ao operador aos domingos. *sunday_pager_end_time*é **int**, com um padrão NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @pager_days=] *pager_days*  
 Especifica os dias em que o operador está disponível para receber páginas (sujeitos aos horários de início/término especificados). *pager_days*é **tinyint**, com um padrão NULL, e deve ser um valor de **0** por meio de **127**. *pager_days* é calculado somando os valores individuais para os dias necessários. Por exemplo, de segunda-feira a sexta-feira é **2**+**4**+**8**+**16** + **32** = **64**.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Segunda-feira|  
|**4**|Terça-feira|  
|**8**|Quarta-feira|  
|**16**|Quinta-feira|  
|**32**|Sexta-feira|  
|**64**|Sábado|  
  
 [ @netsend_address=] '*netsend_address*'  
 O endereço de rede do operador para o qual a mensagem de rede é enviada. *netsend_address*é **nvarchar (100)**, com um padrão NULL.  
  
 [ @category_name=] '*categoria*'  
 O nome da categoria para este alerta. *categoria de* é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 sp_update_operator deve ser executado a partir do banco de dados msdb.  
  
## <a name="permissions"></a>Permissões  
 As permissões para executar este procedimento usam como padrão membros da função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir atualiza o status do operador como habilitado e define os dias (de segunda-feira a sexta-feira, das 8h às 17h) quando o operador pode ser notificado por pager.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
