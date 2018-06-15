---
title: sp_changesubscriptiondtsinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_changesubscriptiondtsinfo
- sp_changesubscriptiondtsinfo_TSQL
helpviewer_keywords:
- sp_changesubscriptiondtsinfo
ms.assetid: 64fc085f-f81b-493b-b59a-ee6192d9736d
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 55c43914d883ce5f704ad6c7648d473bd38611fb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32990981"
---
# <a name="spchangesubscriptiondtsinfo-transact-sql"></a>sp_changesubscriptiondtsinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades do pacote DTS (Data Transformation Services) de uma assinatura. Esse procedimento armazenado é executado no assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changesubscriptiondtsinfo [ [ @job_id = ] job_id ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id=**] *job_id*  
 É a ID do trabalho do Distribution Agent da assinatura push. *job_id* é **varbinary (16)**, sem padrão. Para localizar a ID do trabalho de distribuição, execute **sp_helpsubscription** ou **sp_helppullsubscription**.  
  
 [ **@dts_package_name**=] **'***dts_package_name***'**  
 Especifica o nome do pacote DTS. *dts_package_name* é um **sysname**, com um padrão NULL. Por exemplo especificar um pacote denominado **DTSPub_Package**, você especificaria `@dts_package_name = N'DTSPub_Package'`.  
  
 [ **@dts_package_password**=] **'***dts_package_password***'**  
 Especifica a senha no pacote. *dts_package_password* é **sysname** com um padrão NULL, que especifica que a propriedade de senha deve ser alterada.  
  
> [!NOTE]  
>  Um pacote DTS deve ter uma senha.  
  
 [ **@dts_package_location**=] **'***dts_package_location***'**  
 Especifica o local do pacote. *dts_package_location* é um **nvarchar (12)**, com um padrão NULL, que especifica que o local do pacote deve ser alterada. O local do pacote pode ser alterado para **distribuidor** ou **assinante**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_changesubscriptiondtsinfo** é usado para replicação de instantâneo e replicação transacional são somente assinaturas push.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor **db_owner** função fixa de banco de dados ou o criador da assinatura pode executar **sp_changesubscriptiondtsinfo**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
