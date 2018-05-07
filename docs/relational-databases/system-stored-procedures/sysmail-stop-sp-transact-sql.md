---
title: sysmail_stop_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_stop_sp_TSQL
- sysmail_stop_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_stop_sp
ms.assetid: 045ee36f-5bf0-4626-b5ee-e84db06ce16f
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8f304337470d0117b6f44d03bf7e459c6b9f51d5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysmailstopsp-transact-sql"></a>sysmail_stop_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Para o Database Mail parando os objetos do [!INCLUDE[ssSB](../../includes/sssb-md.md)] que o programa externo usa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_stop_sp  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhuma  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Esse procedimento armazenado está no **msdb** banco de dados.  
  
 Este procedimento armazenado para a fila do Database Mail que contém pedidos de mensagens de saída e desliga a ativação do [!INCLUDE[ssSB](../../includes/sssb-md.md)] para o programa externo.  
  
 Quando as filas são paradas, o programa externo do Database Mail não processa mensagens. Este procedimento armazenado permite parar o Database Mail com propósitos de solução de problemas ou manutenção.  
  
 Para iniciar o Database Mail, use **sysmail_start_sp**. Observe que **sp_send_dbmail** ainda aceita email quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] objetos são interrompidos.  
  
> [!NOTE]  
>  Este procedimento armazenado para apenas as filas do Database Mail. Este procedimento armazenado não desativa a entrega de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] no banco de dados. Este procedimento armazenado não desabilita os procedimentos armazenados estendidos do Database Mail para reduzir a área da superfície. Para desabilitar os procedimentos armazenados estendidos, consulte o [opção Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) do **sp_configure** procedimento armazenado do sistema.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a parada do Database Mail a **msdb** banco de dados. O exemplo supõe que o Database Mail foi habilitado.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_stop_sp ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_start_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
