---
title: sp_changedistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c462e73fd9a99d8645d752aaac86b5207e7c0722
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades do Publicador de distribuição. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@property=** ] **'***propriedade***'**  
 É uma propriedade a ser alterada para o publicador determinado. *propriedade* é **sysname** e pode ser um destes valores.  
  
 [ **@value=** ] **'***value***'**  
 É o valor da propriedade determinada. *valor* é **nvarchar (255)**, com um padrão NULL.  
  
 Esta tabela descreve as propriedades de Publicadores e os valores para essas propriedades.  
  
|Propriedade|Valores|Description|  
|--------------|------------|-----------------|  
|**ativo**|**true**|Ativa o Publicador.|  
||**false**|Desativa o Publicador.|  
|**distribution_db**||Nome do banco de dados de distribuição.|  
|**logon**||Nome de logon.|  
|**senha**||Senha forte para o logon fornecido.|  
|**security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Publicador. *Isso não pode ser alterado para não* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publicador.*|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador. *Isso não pode ser alterado para não* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publicador.*|  
|**working_directory**||Diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação.|  
|NULL (padrão)||Disponíveis *propriedade* opções são impressas.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changedistpublisher** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_changedistpublisher**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
