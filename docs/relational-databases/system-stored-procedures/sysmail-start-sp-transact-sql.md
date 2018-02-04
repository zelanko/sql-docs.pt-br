---
title: sysmail_start_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sysmail_start_sp
- sysmail_start_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_start_sp
ms.assetid: 25fd7bb6-cfdd-463f-bea8-c6fcb805d3f5
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b4bc8f6fda47c152127f4f3ae289a8d4f4b07a56
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailstartsp-transact-sql"></a>sysmail_start_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia o Database Mail ao iniciar os objetos do [!INCLUDE[ssSB](../../includes/sssb-md.md)] que o programa externo usa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_start_sp  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhuma  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 O Database Mail não está habilitado ou instalado na[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação. Use o Assistente para Configuração do Database Mail para habilitar e instalar objetos do Database Mail.  
  
 Esse procedimento armazenado está no **msdb** banco de dados. Esse procedimento armazenado inicia a fila do Database Mail que contém solicitações de mensagens de saída e habilita a ativação do [!INCLUDE[ssSB](../../includes/sssb-md.md)] para o programa externo.  
  
 Quando as filas são iniciadas, o programa externo do Database Mail pode processar mensagens. Esse procedimento permite reiniciar as filas depois que as filas foram interrompidas com o **sysmail_stop_sp** procedimento armazenado.  
  
> [!NOTE]  
>  Este procedimento armazenado inicia apenas as filas do Database Mail. Esse procedimento armazenado não ativa a entrega de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] no banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a partir do Database Mail a **msdb** banco de dados. O exemplo supõe que o Database Mail foi habilitado.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_start_sp ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Opção de configuração do servidor do Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)   
 [sysmail_stop_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)   
 [Armazenados do Database Mail procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
