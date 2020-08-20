---
description: sp_helplogins (Transact-SQL)
title: sp_helplogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68a90477996c9782722e1a9c0b50f82fd5cf408e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489321"
---
# <a name="sp_helplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Fornece informações sobre logons e os usuários associados com eles em cada banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @LoginNamePattern = ] 'login'` É um nome de logon. *login* é **sysname**, com um padrão de NULL. o *logon* deve existir se especificado. Se o *logon* não for especificado, serão retornadas informações sobre todos os logons.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O primeiro relatório contém informações sobre cada logon especificado, como mostrado na tabela a seguir.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Nome de logon.|  
|**SIDs**|**varbinary (85)**|Identificador de segurança de Logon (SID).|  
|**DefDBName**|**sysname**|Banco de dados padrão que o **LoginName** usa ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**DefLangName**|**sysname**|Idioma padrão usado por **LoginName**.|  
|**Auser**|**Char (5)**|Sim = **LoginName** tem um nome de usuário associado em um banco de dados.<br /><br /> Não = **LoginName** não tem um nome de usuário associado.|  
|**ARemote**|**Char (7)**|Sim = **LoginName** tem um logon remoto associado.<br /><br /> Não = **LoginName** não tem um logon associado.|  
  
 O segundo relatório contém informações sobre usuários mapeados para cada logon, e as associações de função do logon, conforme mostrado na tabela a seguir.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Nome de logon.|  
|**NomeDoBancoDeDados**|**sysname**|Banco de dados padrão que o **LoginName** usa ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**UserName**|**sysname**|A conta de usuário para a qual **LoginName** está mapeado em **dbname**e as funções das quais **LoginName** é membro em **dbname**.|  
|**UserOrAlias**|**Char (8)**|MemberOf = **username** é uma função.<br /><br /> User = **username** é uma conta de usuário.|  
  
## <a name="remarks"></a>Comentários  
 Antes de remover um logon, use **sp_helplogins** para identificar as contas de usuário que são mapeadas para o logon.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **securityadmin** .  
  
 Para identificar todas as contas de usuário mapeadas para um determinado logon, **sp_helplogins** deve verificar todos os bancos de dados no servidor. Portanto, para cada banco de dados no servidor, pelo menos uma das seguintes condições deve ser verdadeira:  
  
-   O usuário que está executando **sp_helplogins** tem permissão para acessar o banco de dados.  
  
-   A conta de usuário **convidado** está habilitada no banco de dados.  
  
 Se **sp_helplogins** não puder acessar um banco de dados, **sp_helplogins** retornará o máximo de informações possível e exibirá a mensagem de erro 15622.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdb ](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpuser ](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
