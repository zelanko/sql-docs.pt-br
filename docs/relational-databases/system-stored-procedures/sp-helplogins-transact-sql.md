---
title: sp_helplogins (Transact-SQL) | Microsoft Docs
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
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 40a25164c12e9a1c886a7cba6b8f9b0277daf0ed
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sphelplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre logons e os usuários associados com eles em cada banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@LoginNamePattern =** ] **'***login***'**  
 É o nome de um logon. *login* é **sysname**, com um padrão de NULL. *logon* deve existir se especificado. Se *login* não é especificado, serão retornadas informações sobre todos os logons.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O primeiro relatório contém informações sobre cada logon especificado, como mostrado na tabela a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Nome de logon.|  
|**SID**|**varbinary(85)**|Identificador de segurança de Logon (SID).|  
|**DefDBName**|**sysname**|Banco de dados padrão que **LoginName** usa ao se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**DefLangName**|**sysname**|Idioma padrão usado pelo **LoginName**.|  
|**Auser**|**char (5)**|Sim = **LoginName** tem um nome de usuário associado em um banco de dados.<br /><br /> Não = **LoginName** não tem um nome de usuário associado.|  
|**ARemote**|**CARACT (7)**|Sim = **LoginName** tem um logon remoto associado.<br /><br /> Não = **LoginName** não tem um logon associado.|  
  
 O segundo relatório contém informações sobre usuários mapeados para cada logon, e as associações de função do logon, conforme mostrado na tabela a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Nome de logon.|  
|**DBName**|**sysname**|Banco de dados padrão que **LoginName** usa ao se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**UserName**|**sysname**|Conta de usuário **LoginName** é mapeado na **DBName**e as funções que **LoginName** é um membro no **DBName**.|  
|**UserOrAlias**|**char (8)**|MemberOf = **UserName** é uma função.<br /><br /> Usuário = **UserName** é uma conta de usuário.|  
  
## <a name="remarks"></a>Remarks  
 Antes de remover um logon, use **sp_helplogins** para identificar contas de usuário que são mapeadas para o logon.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **securityadmin** função de servidor fixa.  
  
 Para identificar todas as contas de usuário mapeadas para um determinado logon, **sp_helplogins** deve verificar todos os bancos de dados no servidor. Portanto, para cada banco de dados no servidor, pelo menos uma das seguintes condições deve ser verdadeira:  
  
-   O usuário que está executando **sp_helplogins** tem permissão para acessar o banco de dados.  
  
-   O **convidado** conta de usuário está habilitada no banco de dados.  
  
 Se **sp_helplogins** não é possível acessar um banco de dados, **sp_helplogins** retornará tanta informação quanto possível e exibirá a mensagem de erro 15622.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir relata informações sobre o logon `John`.  
  
```  
EXEC sp_helplogins 'John';  
GO  
  
LoginName SID                        DefDBName DefLangName AUser ARemote   
--------- -------------------------- --------- ----------- ----- -------   
John      0x23B348613497D11190C100C  master    us_english  yes   no  
  
(1 row(s) affected)  
  
LoginName   DBName   UserName   UserOrAlias   
---------   ------   --------   -----------   
John        pubs     John       User          
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
