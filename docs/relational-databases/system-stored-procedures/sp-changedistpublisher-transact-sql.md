---
title: sp_changedistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 302d807b70e4cceb7cf25bffd0af637df7c4ad8c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120164"
---
# <a name="spchangedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades do Publicador de distribuição. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do publicador. *Publisher* está **sysname**, sem padrão.  
  
`[ @property = ] 'property'` É uma propriedade para alterar para o publicador determinado. *propriedade* está **sysname** e pode ser um destes valores.  
  
`[ @value = ] 'value'` É o valor para a propriedade especificada. *valor* está **nvarchar (255)** , com um padrão NULL.  
  
`[ @storage_connection_string = ] 'storage_connection_string'` É necessário para a instância gerenciada do banco de dados SQL, deve coincidir com a chave de acesso para o volume de armazenamento do banco de dados SQL. 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 Esta tabela descreve as propriedades de Publicadores e os valores para essas propriedades.  
  
|Propriedade|Valores|Descrição|  
|--------------|------------|-----------------|  
|**Active Directory**|**true**|Ativa o Publicador.|  
||**false**|Desativa o Publicador.|  
|**distribution_db**||Nome do banco de dados de distribuição.|  
|**login**||Nome de logon.|  
|**password**||Senha forte para o logon fornecido.|  
|**security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Publicador. *Isso não pode ser alterado para um não -* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publicador.*|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador. *Isso não pode ser alterado para um não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publicador.*|  
|**working_directory**||Diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação.|  
|NULL (padrão)||Todos disponíveis *propriedade* opções são impressos.| 
|**storage_connection_string**| Chave de acesso | A chave de acesso para o diretório de trabalho quando o banco de dados banco de dados de instância gerenciada do SQL. 
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changedistpublisher** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_changedistpublisher**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
