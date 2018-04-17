---
title: sp_getmergedeletetype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_getmergedeletetype
- sp_getmergedeletetype_TSQL
helpviewer_keywords:
- sp_getmergedeletetype
ms.assetid: 64450e4d-844d-4176-874e-f3845536f7d2
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aedd86069b3a80170a86f14463c02769141b1b79
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spgetmergedeletetype-transact-sql"></a>sp_getmergedeletetype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o tipo de exclusão de mesclagem. Esse procedimento armazenado é executado no publicador do banco de dados de publicação ou no assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_getmergedeletetype [ @source_object = ] 'source_object', [ @rowguid =] 'rowguid', [ @delete_type=] delete_type OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@source_object =**] **'***source_object***'**  
 É o nome do objeto de origem. *source_object* é **nvarchar (386)**, sem padrão.  
  
 [  **@rowguid=**] **'***rowguid***'**  
 É o identificador de linha do tipo de exclusão. *ROWGUID* é **uniqueidentifier**, sem padrão.  
  
 [  **@delete_type=**] *delete_type* **saída**  
 É o código que indica o tipo de exclusão. *delete_type* é **int**, sem padrão. *delete_type* também é um parâmetro de saída, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**1**|Exclusão de usuário|  
|**5**|Exclusão parcial|  
|**6**|Exclusão de sistema|  
  
## <a name="remarks"></a>Remarks  
 **sp_getmergedeletetype** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_getmergedeletetype**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
